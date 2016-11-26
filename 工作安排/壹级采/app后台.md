### git地址：http://git.oschina.net/0703/yijicai-platform
### 服务器路径: /data/web/platform
### 测试服务器路径：/data/p/web/platform
    账号/密码： zhengji/zhengji123
    第三方后台: third/123456
### xshell链接后台服务器
- 用户名：root  密码：123456

```shell

memcached -d -p 11211 -u root -m 64 -c 1024 -P /var/run/memcached_yjc.pid

ps -ef | grep mem

cd /data/platform/apache/bin

./startup.sh


```
