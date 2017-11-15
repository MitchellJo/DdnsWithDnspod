# DdnsWithDnspod
* DDNS with dnspod.cn in LEDE(Openwrt).
* 这是我写的一个脚本，目的是为了在LEDE路由上使用dnspod.cn的DDNS服务

## 特点说明
* 使用官方API
* 没有使用curl，转而使用wget（因为我的路由器性能比较低，没有多余空间再安装curl）
* 需要使用cron
* 理论上Openwrt也可以使用

## 使用方法
### 更新wget，因为LEDE自带wget不完整，无法使用https
```bash
opkg install wget
reboot
```
### 下载 DdnsWithDnspod.sh
把DdnsWithDnspod.sh放到LEDE的根用户的home目录

### 替换下面账号信息为自己的
```bash
LOGIN_TOKEN="xxxxx,yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy"
DOMAIN="youdomain.xx"
```
其中LOGIN_TOKEN可用从[这里](https://www.dnspod.cn/console/user/security)的“API Token”获取

### 添加任务到cron
可以在luci页面的Scheduled Tasks中添加下面这样的信息
```bash
*/10 * * * * sh /root/DdnsWithDnspod.sh >> /root/DdnsWithDnspod.log
```

### 最后重启一下路由器
如果每隔10min可以看到/root/DdnsWithDnspod.log有更新，说明DDNS已经正常运行。
