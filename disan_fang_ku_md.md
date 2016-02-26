# 第三方库API接口
InfluxDB提供了各种语言的Http API接口的封装。具体可以看这里：  
[https://docs.influxdata.com/influxdb/v0.10/clients/api/](https://docs.influxdata.com/influxdb/v0.10/clients/api/)

同时，官方也提供了Telegraf插件来收集数据，除此之外还有collectd等比较常用的第三方数据收集工具。   

我并不推荐一开始就用各种工具，这样会淡化对InfluxDB的理解。  
*当然，如果你本身对这些工具很熟悉，那么就直接使用吧！*

所以本章节主要介绍各语言对InfluxDB Http API接口的封装。

