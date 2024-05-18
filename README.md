# xray-script

Xray 一键安装脚本，基于网络跳跃原版魔改，支持IPv4/IPv6 VPS，支持与宝塔面板共存

```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/Felix-zf/Xray-install/main/xray.sh && bash xray.sh
```

---

## VPS常用脚本合集  

- VPS性能检测
```
wget -qO- bench.sh | bash
```
- VPS回程路由
```
wget -qO- oldking.net/supertrace.sh | bash
```
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
- 安装BBR加速  
1. CentOS 8 / Debian ≥ 9 开启自带 BBR 加速 ，复制全部粘贴
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
lsmod | grep bbr
```
2. BBR2
```
wget --no-check-certificate -q -O bbr2.sh "https://github.com/yeyingorg/bbr2.sh/raw/master/bbr2.sh" && chmod +x bbr2.sh && bash bbr2.sh auto
```
3. BBR Plus
```
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
*查看开启状态*
```
sysctl -p
```
- 安装curl
Ubuntu/Debian 系统安装 Curl 方法
```
apt-get update -y && apt-get install curl -y
```
Centos 系统安装 Curl 方法
```
yum update -y && yum install curl -y
```
##Linux中有个ntp包可以自动校准时间，并且非常好用##
- Debian系统安装NTP校时包
```
apt-get install ntpdate
```
- CentOS系统安装NTP校时包##
```
yum install ntp
```
- 校时命令

方法一
```
ntpdate cn.pool.ntp.org
```
##如果想每隔一定时间自动校时，只需将上面的命令加入至Cron就行了##
```
00 12 * * * /sbin/ntpdate cn.pool.ntp.org
```
Tips: cn.pool.ntp.org是ntp网络授时组织的中国授时源  

方法二    
*快速校对linux服务器时间至北京时间* 
服务器采用ntp更新时间，经常牵扯到UTC是否开启的问题，开启了时间就会快8个小时 前段时间朋友给我了下面的命令，一条命令解决之前的所有问题。
```
rdate -t 60 -s stdtime.gov.hk
```
使用rdate将stdtime.gov.hk服务器的时间抓取回来，然后写入硬件
```
hwclock -w
```
下面是rdate的命令使用方法介绍    
功能说明：显示其他主机的日期与时间。    
语　　法：rdate [-ps][主机名称或IP地址…]    
补充说明：执行rdate指令，向其他主机询问系统时间并显示出来。  

参　　数：    
-p 　显示远端主机的日期与时间。    
-s 　把从远端主机收到的日期和时间，回存到本地主机的系统时间。

---

# V2rayN设置 
- 路由规则(Whitelist)
```
[
  {
    "port": "",
    "outboundTag": "proxy",
    "ip": [],
    "domain": [
      "#以下三行是GitHub网站，为了不影响下载速度走代理",
      "github.com",
      "githubassets.com",
      "githubusercontent.com"
    ],
    "protocol": []
  },
  {
    "type": "field",
    "outboundTag": "block",
    "domain": [
      "#阻止CrxMouse鼠标手势收集上网数据",
      "mousegesturesapi.com",
      "#下一行广告管理平台网址，在ProductivityTab（原iChrome）浏览器插件页面显示",
      "cf-se.com"
    ]
  },
  {
    "type": "field",
    "port": "",
    "outboundTag": "direct",
    "ip": [
      "geoip:private",
      "geoip:cn"
    ],
    "domain": [
      "bitwarden.com",
      "bitwarden.net",
      "gravatar.com",
      "gstatic.com",
      "baiyunju.cc",
      "letsencrypt.org",
      "adblockplus.org",
      "safesugar.net",
      "#下两行谷歌广告",
      "googleads.g.doubleclick.net",
      "adservice.google.com",
      "#【以下全部是geo预定义域名列表】",
      "#下一行包含所有私有域名",
      "geosite:private",
      "#下一行包含常见大陆站点域名和CNNIC管理的大陆域名，即geolocation-cn和tld-cn的合集",
      "geosite:cn",
      "#下一行包含所有Adobe旗下域名",
      "geosite:adobe",
      "#下一行包含所有Adobe正版激活域名",
      "geosite:adobe-activation",
      "#下一行包含所有微软旗下域名",
      "geosite:microsoft",
      "#下一行包含微软msn相关域名少数与上一行微软列表重复",
      "geosite:msn",
      "#下一行包含所有苹果旗下域名",
      "geosite:apple",
      "#下一行包含所有广告平台、提供商域名",
      "geosite:category-ads-all",
      "#下一行包含可直连访问谷歌网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:google-cn",
      "#下一行包含可直连访问苹果网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:apple-cn"
    ],
    "protocol": []
  },
  {
    "type": "field",
    "port": "0-65535",
    "outboundTag": "proxy"
  }
]
```

- DNS设置
```
"dns": {
  "hosts": {
    "dns.google": "8.8.8.8",
    "dns.pub": "119.29.29.29",
    "dns.alidns.com": "223.5.5.5",
    "geosite:category-ads-all": "127.0.0.1"
  },
  "servers": [
    {
      "address": "https://1.1.1.1/dns-query",
      "domains": ["geosite:geolocation-!cn"],
      "expectIPs": ["geoip:!cn"]
    },
    "8.8.8.8",
    {
      "address": "114.114.114.114",
      "port": 53,
      "domains": ["geosite:cn", "geosite:category-games@cn"],
      "expectIPs": ["geoip:cn"],
      "skipFallback": true
    },
    {
      "address": "localhost",
      "skipFallback": true
    }
  ]
}
```

