<!--
 * @Description: 
 * @Author: your name
 * @version: 
 * @Date: 2023-10-27 12:19:48
 * @LastEditors: your name
 * @LastEditTime: 2023-10-27 15:01:04
-->
# configparser 详解

* configparser.RawConfigParser() 是 Python 标准库 configparser 模块中的一个函数，用于读取配置文件（通常是 INI 格式的文件）。这个模块允许你写一个配置文件，然后在 Python 程序中读取这些配置。

## 配置文件对象的组成

1. Sections
配置文件由多个“section”组成，每个section由方括号包裹的标题表示，例如 `[Section1]`。

2. Options
每个section下面可以有一个或多个options（配置项）。这些配置项通常以键值对的形式出现，例如 key = value。

3. Comments
配置文件中可以包含注释，通常用 # 或 ; 开头。

## 如何构造、读取和使用

1. 构造
你可以通过调用 configparser.RawConfigParser() 来创建一个配置文件解析器的实例。

2. 读取
使用这个实例的 .read() 方法来读取配置文件。你可以传递一个文件名或文件名的列表。

3. 使用
一旦文件被读取，你可以使用 .get(section, option) 方法来获取特定section下option的值。还有其他方法，如 .sections() 返回所有section的列表，.options(section) 返回给定section下所有option的列表。

## 应用示例
假设你有以下配置文件 settings.ini:
```ini
[Database]
host = localhost
user = root
password = rootpassword
database = mydatabase

[Server]
port = 8080
debug = True
```
下面是如何使用 configparser.RawConfigParser() 来读取和使用这个配置文件的示例:
```python
import configparser

# 创建配置解析器实例
config = configparser.RawConfigParser()

# 读取配置文件
config.read('settings.ini')

# 获取数据库配置
db_host = config.get('Database', 'host')
db_user = config.get('Database', 'user')
db_password = config.get('Database', 'password')
db_database = config.get('Database', 'database')

# 获取服务器配置
server_port = config.getint('Server', 'port')  # 使用 getint 读取整数值
server_debug = config.getboolean('Server', 'debug')  # 使用 getboolean 读取布尔值

# 打印获取的配置
print(f"Database Host: {db_host}")
print(f"Database User: {db_user}")
print(f"Database Password: {db_password}")
print(f"Database Name: {db_database}")
print(f"Server Port: {server_port}")
print(f"Server Debug: {server_debug}")
```