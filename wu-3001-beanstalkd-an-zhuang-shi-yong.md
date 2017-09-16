# Beanstalkd的安装使用

---

以OS x 为例

```
brew install beanstalkd
```

其他相关系统可以参考官方教程：[http://kr.github.io/beanstalkd/download.html](http://kr.github.io/beanstalkd/download.html)

### 开启服务

```
beanstalkd -l 10.0.1.5 -p 11300
```

* `-b DIR`  输出 binlog 保持任务不丢失, DIR 指定路径
* `-l ADDR`绑定的地址, 默认为 \(0.0.0.0\)
* `-p PORT`绑定的端口, 默认为 \(11300\)
* `-z BYTES`每一个 job 消息的最大大小, 默认 65535 bytes \(64kb, 足够了吧\)
* `-s BYTES`设置单个 binlog 文件的最大大小, 超过会自动切分文件, 默认 10485760 \(10mb\)
* `-V`查看输出的日志. \(我简单 debug 用\)



