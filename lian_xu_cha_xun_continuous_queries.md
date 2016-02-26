# 连续查询（Continuous Queries）
当数据超过保存策略里指定的时间之后，就会被删除。  
如果我们不想完全删除掉，比如做一个数据统计采样：把原先每秒的数据，存为每小时的数据，让数据占用的空间大大减少（以降低精度为代价）。  

这就需要InfluxDB提供的：连续查询（Continuous Queries）。

## 当前数据库的Continuous Queries
```bash
# 这条命令得在命令行下输入，在web管理界面不能显示。
SHOW CONTINUOUS QUERIES
```

## 创建新的Continuous Queries
```bash
> CREATE CONTINUOUS QUERY cq_30m ON testDB BEGIN SELECT mean(temperature) INTO weather30m FROM weather GROUP BY time(30m) END
```
其中：   
1. cq_30m：连续查询的名字
2. testDB：具体的数据库名
3. mean(temperature): 算平均温度
4. weather： 当前表名
5. weather30m： 存新数据的表名
6. 30m：时间间隔为30分钟


**当我们插入新数据之后，可以发现数据库中多了一张名为weather30m(里面已经存着计算好的数据了)。这一切都是通过Continuous Queries自动完成的。**

```bash
> SHOW MEASUREMENTS
name: measurements
------------------
name
weather
weather30m
```

## 删除Continuous Queries
```bash
DROP CONTINUOUS QUERY <cq_name> ON <database_name>
```

**具体效果，大家可以直接自己在测试数据库上试验**
