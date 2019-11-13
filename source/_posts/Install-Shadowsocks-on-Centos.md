title: Install Shadowsocks on Centos
tags: |-

- shadowsocks
- 翻墙
- CentOS
- Shadowsocks
  permalink: install-shadowsocks-on-centos
  id: 4
  updated: '2014-09-23 14:53:01'
  date: 2014-07-15 18:45:44

---

> 身为有理想、有追求的有志青年，出于对自由的向往，怎能甘心接受被围在墙内？

**_so, I do that：_**

> install shadowsocks on my digitalocean VPS

### #ready

开发者必备之 _Development Tools_<br>
`yum groupinstall 'Development Tools'`<br>
`yum install git`

### #do it

`git clone https://github.com/madeye/shadowsocks-libev.git`<br>
`cd shadowsocks-libev`<br>
_编译安装三部曲：_<br>
`./configure`<br>
`make`<br>
`make install`<br>

### #use it

`nohup /usr/local/bin/ss-server -s IP地址 -p 端口 -k 密码 -m 加密方式 &`

> - -s #vps 的 IP 地址
> - -p #端口
> - -k #自定义的密码
> - -m #加密方式，推荐使用 aes-256-cfb

示例：`nohup /usr/local/bin/ss-server -s 11.22.33.44 -p 12345 -k 12345678 -m aes-256-cfb &`

为了方便，加入开机启动：
`echo "nohup /usr/local/bin/ss-server -s 11.22.33.44 -p 12345 -k 12345678 -m aes-256-cfb &" >> /etc/rc.local`

android 和 iOS 都有 Shadowsocks 客户端

> **_注意：_**<br>当你完成以上所有步骤以后，你可能会很伤心，很难过，因为你的客户端能连上但不能上网。<br>
> **_请不要伤心，也不要难过：_**<br>执行神一样的命令`yum update`即可。
