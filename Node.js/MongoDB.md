# Node.js 连接MongoDB

## Windows 安装MongoDB

1. 进入MongoDB官网[下载页面](https://www.mongodb.com/download-center),选择 `Community Server` 页，下载程序。

2. 运行安装程序，按照指引进行安装。

3. 安装完成后可以在 `C:\Program Files\MongoDB\Server\3.4\bin` 找到MongoDB的程序。

4. 将 `C:\Program Files\MongoDB\Server\3.4\bin` 添加到 `Path` 中。

## 指定存储目录并启动服务

1. 创建数据库存放的目录，如：`D:\Datebase\MongoDB` 。

2. 运行命令：`mongod --dbpath D:\Datebase\MongoDB`

3. 使用配置文件 `mongod --config D:\Datebase\mongod.cfg`

```
# 配置文件参考
systemLog:
    destination: file
    path: D:\Datebase\MongoDB\log\mongod.log
storage:
    dbPath: D:\Datebase\MongoDB\data
```

## 将MongoDB安装为系统服务

参数 | 描述
---|---
--bind_ip | 绑定服务IP，若绑定127.0.0.1，则只能本机访问，不指定默认本地所有IP
--logpath | 定MongoDB日志文件，注意是指定文件不是目录
--logappend | 使用追加的方式写日志
--dbpath | 指定数据库路径
--port | 指定服务端口号，默认端口27017
--serviceName | 指定服务名称
--serviceDisplayName | 指定服务名称，有多个mongodb服务时执行。
--install | 指定作为一个Windows服务安装。

```
mongod.exe --bind_ip [yourIPadress] --logpath ["D:\Datebase\MongoDB\mongodb.log"] --logappend --dbpath ["D:\Datebase\MongoDB"] --port [yourPortNumber] --serviceName ["YourServiceName"] --serviceDisplayName ["YourServiceName"] --install

```

示例：

```
mongod.exe --logpath "D:\Datebase\MongoDB\log\mongodb.log" --logappend --dbpath "D:\Datebase\MongoDB\data" --port 27017 --serviceName "MongoDB" --serviceDisplayName "MongoDB" --install


# 使用sc进行安装

sc.exe create MongoDB binPath= "\"C:\Program Files\MongoDB\Server\3.4\bin\mongod.exe\" --service --config=\"D:\Datebase\MongoDB\config\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
```

## 启动服务

```
net start MongoDB
```
## 停止服务，并删除

```
net stop MongoDB
sc.exe delete MongoDB
```

## 使用mongoose

### 安装 mongoose

```bash
npm install mongoose --save
```

### 