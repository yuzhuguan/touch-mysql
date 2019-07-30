# touch-mysql

## 数据库表---> t_profile

```
*************************** 1. row ***************************
  id: 1
data: {"openId":"xxx","nickname":"哈哈","sex":"1","birthday":xxx,"grade":14,"relationship":"女主人","lockpwd":"000000","emergencyNumber":"xxxx","headerImg":"xxxx"}
imei: xxxxxx
*************************** 2. row ***************************
  id: 2
data: {"openId":"xxx","nickname":"亲亲","sex":"0","birthday":xxx,"relationship":"父亲","lockpwd":"123456","emergencyNumber":"xxx"}
imei: xxxxxxxxx
*************************** 3. row ***************************
  id: 3
data: {"openId":"sdfassdfsdf","nickname":"wer","sex":1,"birthday":"2019-06-25T16:00:00.000Z","grade":"6","relationship":"温热无","lockpwd":"123456","emergencyNumber":"sdafdsafsa"}
imei: fsadfsadfsadf
*************************** 4. row ***************************
  id: 4
data: {"openId":"dsfsadfsadf","nickname":"dasfdfasdf","sex":0,"birthday":"2019-06-25T16:00:00.000Z","relationship":"","lockpwd":"777772","emergencyNumber":"adsfsadfsa","headerImg":""}
imei: asdfasfsa
*************************** 5. row ***************************
  id: 5
data: {"openId":"ow8eE589nLE-adsfasdf","nickname":"哈哈哈","sex":"0","birthday":1468281600000,"grade":12,"relationship":"发挥1斤了","lockpwd":"123455","emergencyNumber":"31","headerImg":"asdfsafsadf"}
imei: qweqweqw
```

## JSON条件查询

上述的字段data是json格式，mysql5.7支持json查询： 比如查询emergencyNumber为某几个值，示例如下：

```
SELECT id  FROM t_profile where JSON_CONTAINS(JSON_ARRAY("xxxx","ad","dadad"),data->'$.emergencyNumber');
```

删除满足上述条件的记录：
```
delete from t_profile where id IN (select tmp.id from (SELECT id  FROM t_profile where JSON_CONTAINS(JSON_ARRAY("xxxx","ad","dadad"),data->'$.emergencyNumber'))tmp);
```
