基于muduo网络库实现的高性能集群聊天服务器和客户端，支持nginx TCP负载均衡。

## 技术栈

- **网络库**：muduo（C++高性能网络库）
- **数据库**：MySQL（用户信息存储）
- **缓存**：Redis（消息队列、发布订阅）
- **构建工具**：CMake
- **第三方库**：json.hpp（JSON序列化/反序列化）

## 目录结构

```
chatserver/
├── autobuild.sh        # 自动构建脚本
├── bin/                # 编译后的可执行文件
│   ├── ChatClient      # 客户端可执行文件
│   └── ChatServer      # 服务器可执行文件
├── build/              # 构建目录
├── CMakeLists.txt      # 顶层CMake配置文件
├── include/            # 头文件目录
│   ├── public.hpp      # 公共头文件
│   └── server/         # 服务器头文件
├── README.md           # 项目说明文档
├── src/                # 源代码目录
│   ├── CMakeLists.txt  # 源代码CMake配置
│   ├── client/         # 客户端源代码
│   └── server/         # 服务器源代码
│       ├── db/         # 数据库操作模块
│       ├── model/      # 数据模型
│       └── redis/      # Redis操作模块
├── test/               # 测试目录
└── thirdparty/         # 第三方依赖
    └── json.hpp        # JSON库
```

## 功能特性

### 服务器功能
- 基于muduo网络库实现高性能TCP网络通信
- 支持多客户端并发连接
- 实现用户注册、登录功能
- 支持私聊和群聊功能
- 基于Redis的发布订阅机制实现消息广播
- 支持nginx TCP负载均衡的集群部署
- 用户在线状态管理

### 客户端功能
- 命令行界面，简单易用
- 支持用户注册和登录
- 支持查看在线用户列表
- 支持一对一私聊
- 支持创建和加入群组聊天
- 实时消息提醒

## 环境依赖

- C++11及以上编译器
- CMake 3.0及以上
- muduo网络库
- MySQL 5.7及以上
- Redis 3.0及以上

## 构建与运行

### 1. 安装依赖

确保已安装所需的依赖库：

```bash
# 安装CMake
sudo apt-get install cmake

# 安装MySQL
sudo apt-get install mysql-server mysql-client libmysqlclient-dev

# 安装Redis
sudo apt-get install redis-server

# 安装muduo网络库
# 请参考muduo官方文档进行安装
```

### 2. 编译项目

使用自动构建脚本：

```bash
cd /chatserver_path/chatserver
chmod +x autobuild.sh
./autobuild.sh
```

或手动构建：

```bash
cd /chatserver_path/chatserver
mkdir -p build
cd build
cmake ..
make
```

### 3. 配置数据库

1. 创建数据库和表结构
2. 修改服务器代码中的数据库连接参数

### 4. 运行服务器

```bash
cd /chatserver_path/chatserver/bin
./ChatServer
```

### 5. 运行客户端

```bash
cd /chatserver_path/chatserver/bin
./ChatClient
```

## 集群部署

1. 启动多个ChatServer实例，监听不同端口
2. 配置nginx TCP负载均衡：

```nginx
stream {
    upstream chat_servers {
        server 127.0.0.1:6000 weight=1;
        server 127.0.0.1:6001 weight=1;
        server 127.0.0.1:6002 weight=1;
    }

    server {
        listen 8000;
        proxy_pass chat_servers;
    }
}
```

3. 客户端连接到nginx的8000端口

## 注意事项

1. 确保MySQL和Redis服务已正确启动
2. 首次运行需要配置数据库连接参数
3. 集群部署时需要确保各节点能访问相同的MySQL和Redis服务
4. 客户端连接服务器时需要指定正确的IP地址和端口



        