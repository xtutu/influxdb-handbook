# 增

在名词解释这一章节中，我们看到在weather中的有不少数据。   
本节将演示下如何为数据库插入数据。

## 通过命令行
```bash
use testDB
insert weather,altitude=1000,area=北 temperature=11,humidity=-4
```
这样，我们就向数据库中添加了一条数据。

## 通过Http接口
InfluxDB提供了Http的API接口，所以我们也可以通过下面的方式来插入数据。  
```bash
curl -i -XPOST 'http://localhost:8086/write?db=testDB' --data-binary 'weather,altitude=1000,area=北 temperature=11,humidity=-4'
```


## Line Protocol格式
插入数据的格式似乎比较奇怪，这是因为influxDB储存数据所采用的是Line Protocol格式。  

在上面两个插入数据的方法中，都有一样的部分。  
>weather,altitude=1000,area=北 temperature=11,humidity=-4


其中:     
1. weather ： 表名
2. altitude=1000,area=北 ： tag
3. temperature=11,humidity=-4 ：field

具体的格式介绍可以看[官方的文档](https://docs.influxdata.com/influxdb/v0.10/write_protocols/line/)　  

