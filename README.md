## 聊天室服务器和客户端

server_chat.go 是服务器代码
client_chat.go 是客户端代码

并发聊天室需求：

1. 支持多个客户端
2. 广播或私信
3. 上线通知
4. 下线通知
5. 设置昵称

分析所涉及到的技术：

1. 网络编程 net + goroutine
2. 广播： 客户端自己发给其他客户端吗？流程：客户端A发给服务器端，服务器端广播给其他客户端 ，服务器端必须记录 连接列表
3. 同步机制，多个goroutine需要传递消息 channel 设置
4. 消息的类型： 广播或私信 消息结构体体现 设计一个channel

编译并运行

`go build`再执行
或者`go run` 直接编译执行

客户端聊天功能(可进行的操作),运行客户端代码后进入一个交互式解析器:
支持三种指令

1. 设置昵称
```
golang's chat>set:mayun
golang's chat>set:mahuaten
//指令二需要在另一台客户端输入新建昵称mahuaten
```

2. 广播消息
```
golang's chat>all:I'm not interested in money
```

3. 私聊(在mahuaten客户端发给mayun)
```
golang's chat>mayun:I'm a normal family
```