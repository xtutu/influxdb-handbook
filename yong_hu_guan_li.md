# 用户管理

**以下语句都可以直接在InfluxDB的Web管理界面中调用**

```bash
# 显示用户
SHOW USERS
# 创建用户
CREATE USER "username" WITH PASSWORD 'password'
# 创建管理员权限的用户
CREATE USER "username" WITH PASSWORD 'password' WITH ALL PRIVILEGES

# 删除用户
DROP USER "username"

```