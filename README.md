# xray-script

Xray 一键安装脚本，基于网络跳跃原版魔改，支持IPv4/IPv6 VPS，支持与宝塔面板共存

```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/Felix-zf/Xray-install/main/xray.sh && bash xray.sh
```

## vps常用脚本合集
- Debian更新系统
```
apt update -y
```
- CentOS更新系统
```
yum install epel-release -y
```
```
yum update -y
```
- CentOS更新系统
```
yum update -y
```
```
yum install -y curl
```
- BBR2
```
wget --no-check-certificate -q -O bbr2.sh "https://github.com/yeyingorg/bbr2.sh/raw/master/bbr2.sh" && chmod +x bbr2.sh && bash bbr2.sh auto
```
- 查看开启状态
```
sysctl -p
```
##bbrplus加速##

wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
##查看开启状态##

sysctl -p
##安装curl##

Ubuntu/Debian 系统安装 Curl 方法
apt-get update -y && apt-get install curl -y
Centos 系统安装 Curl 方法
yum update -y && yum install curl -y
##Linux中有个ntp包可以自动校准时间，并且非常好用##
##Debian系统安装NTP校时包##

apt-get install ntpdate
##CentOS系统安装NTP校时包##

yum install ntp
##安装BBR加速##
CentOS 8 / Debian ≥ 9 开启自带 BBR 加速 ，复制全部粘贴

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
lsmod | grep bbr
##校时命令##

ntpdate cn.pool.ntp.org
##如果想每隔一定时间自动校时，只需将上面的命令加入至Cron就行了##

00 12 * * * /sbin/ntpdate cn.pool.ntp.org
* cn.pool.ntp.org是ntp网络授时组织的中国授时源

方法二

快速校对linux服务器时间至北京时间

服务器采用ntp更新时间，经常牵扯到UTC是否开启的问题，开启了时间就会快8个小时 前段时间朋友给我了下面的命令，一条命令解决之前的所有问题。

rdate -t 60 -s stdtime.gov.hk
使用rdate将stdtime.gov.hk服务器的时间抓取回来，然后写入硬件

hwclock -w
下面是rdate的命令使用方法介绍
功能说明：显示其他主机的日期与时间。
语　　法：rdate [-ps][主机名称或IP地址…]
补充说明：执行rdate指令，向其他主机询问系统时间并显示出来。
参　　数：
-p 　显示远端主机的日期与时间。
-s 　把从远端主机收到的日期和时间，回存到本地主机的系统时间。
