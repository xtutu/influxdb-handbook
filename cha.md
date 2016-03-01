# 查

本节将演示下查询数据的一些常用方法。

## 通过命令行
```bash
use testDB
# 查询最新的三条数据
SELECT * FROM weather ORDER BY time DESC LIMIT 3
```


## 通过Http接口
```bash
curl -G 'http://localhost:8086/query?pretty=true' --data-urlencode "db=testDB" --data-urlencode "q=SELECT * FROM weather ORDER BY time DESC LIMIT 3"
```

--------

**InfluxDB是支持类SQL语句的，具体的查询语法都差不多，就不再详细描述了。**