# 名词解析

# 名词解释
这里先将以下场景:  
我们有一个数据库名为testDB，里面有一张表weather用于记录：多个地区在几组海拔下的一天的温度变化，所以表中有以下字段：
1. 时间 time
2. 温度 temperature
3. 湿度 humidity
3. 地区 area
4. 海拔 altitude

## 数据库、表、数据

| influxDB中的名词  | 传统数据库中的概念   | 
| :----:   | :----: | 
| database     | 数据库            | 
| measurement  | 数据库中的表     |
| points        | 表里面的一行数据　|

## InfluxDB中独有的一些概念



| influxDB中的其它名词  | 传统数据库中的概念   | 
| :----:   | :----: | 
| time     	| 每个数据记录时间，是数据库中的主索引(会自动生成) | 
| tags   	| 各种有索引的属性：地区，海拔|
| fields    | 各种记录值（没有索引的属性）也就是记录的值：温度， 湿度|

这里不得不提另一个名字：series。


所有在数据库中的数据，都需要通过图表来展示，而这个series表示这个表里面的数据，可以在图表上画成几条线：**通过tags排列组合算出来。**

比如有如下数据：

```js
> select* from weather
name: weather
-------------
time                    altitude        area    humidity        temperature
1456386985094000000     1000            北      18              17
1456386985094000000     5000            上      20              47
1456386985094000000     5000            北      26              68
1456386985094000000     1000            广      17              83
1456387267668000000     1000            上      12              77
1456387267668000000     1000            北      16              20
1456387267668000000     5000            广      -3              66
1456387267668000000     5000            上      19              60
```

它的series为：
```js
> show series from  weather
name: weather
-------------
_key                            altitude        area
weather,altitude=1000,area=北   1000            北
weather,altitude=5000,area=北   5000            北
weather,altitude=5000,area=上   5000            上
weather,altitude=1000,area=广   1000            广
weather,altitude=1000,area=上   1000            上
weather,altitude=5000,area=广   5000            广
```