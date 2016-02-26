# 数据库与表的操作

**以下语句都可以直接在InfluxDB的Web管理界面中调用**

```bash
# 创建数据库
CREATE DATABASE "db_name"
# 显示所有数据库
SHOW DATABASES
# 删除数据库
DROP DATABASE "db_name"

# 使用数据库
USE mydb

# 显示该数据库中的表
SHOW MEASUREMENTS

# 创建表
# 直接在插入数据的时候指定表名（weather就是表名）
insert weather,altitude=1000,area=北 temperature=11,humidity=-4

# 删除表
DROP MEASUREMENT "measurementName"

```