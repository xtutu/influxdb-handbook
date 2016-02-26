# NodeJS

截至2016年2月26日，官方的列表中，并没有提供NodeJS的Http API接口的封装。 - -！

好在我们有Github，在上面搜索到一个:  
[https://github.com/node-influx/node-influx](https://github.com/node-influx/node-influx)

项目介绍写着的是支持0.9x版本的InfluxDB，我在0.10上试了下，基本可用。  
因为是纯Http API接口，如果某些接口有问题的话，可以直接给他 pull request。

附上使用代码： 
```js
/**@type InfluxDB*/
var influx = require('influx')
var async = require("async")
var ut = require("./../../util/util.js")
var dbName = "testDB"
var tableName = "weather"
var client = influx({
    host : '192.168.0.196',
    port : 8086, // optional, default 8086
    protocol : 'http', // optional, default 'http'
    username : '',
    password : '',
    database : dbName
})
var altitudes = [1000, 5000]
var areas = ["北", "上", "广", "深"]
async.waterfall([
        function(cb){ // 创建数据库
            client.createDatabase(dbName, function(err,result){
                ut.log("createDatabase", result)
                cb(err, null)
            } )
        },
        function(result, cb){ // 获取数据库名字
            client.getDatabaseNames( function(err, result){
                ut.log("getDatabaseNames", result)
                cb(err, null)
            } )
        },
        function(result, cb){ // 写入数据
            var points = [
                [
                    {
                        temperature: ut.RandByRange(0, 100), humidity : ut.RandByRange(-15, 30)
                    },
                    {
                        altitude: altitudes[ut.RandByRange(0, altitudes.length)], area : areas[0]
                    },
                ],
                [
                    {
                        temperature: ut.RandByRange(0, 100), humidity : ut.RandByRange(-15, 30)
                    },
                    {
                        altitude: altitudes[ut.RandByRange(0, altitudes.length)], area : areas[1]
                    },
                ],
            ]
            client.writePoints(tableName, points, function(err, result){
                ut.log("writePoint", result)
                cb(err, null)
            } )
        },
        function(result, cb){ // 查询数据
            client.query( 'SELECT * FROM weather ORDER BY time DESC LIMIT 3', function(err,result){
                ut.log("query", result)
                cb(err, null)
            } )
        },
        function(result, cb){
            client.getMeasurements( function(err,result){
                ut.log("getMeasurements", JSON.stringify(result))
                cb(err, null)
            })
        }
    ]
    , function(err, result){
        ut.log("finish...", err, result)
    }
)

```