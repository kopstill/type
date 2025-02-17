---
layout: post
title: Shadowsocks and v2ray server tutorial
permalink: '/shadowsocks-v2ray-server-tutorial'
---

###### 基于shadowsocks+v2ray的服务端搭建教程

> shadowsocks选择的是基于C语言的[shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev){:target="_blank"}分支版本，v2ray作为其插件  
> [Github安装文档](https://github.com/shadowsocks/shadowsocks-libev/blob/master/README.md){:target="_blank"}

<ol>
    <li>参考Github文档安装shadowsocks-libev；</li>
    <li>安装v2ray-plugin插件；
        <ol>
            <li>根据操作系统下载最新版<a href="https://github.com/shadowsocks/v2ray-plugin/releases" target="_blank">v2ray-plugin</a>插件程序包；</li>
            <li>解压程序包并将解压出的可执行文件v2ray-plugin_linux_*移动到/usr/local/bin目录；</li>
        </ol>
    </li>
    <li>配置文件中plugin字段填入插件程序名v2ray-plugin_linux_*；</li>
</ol>

##### 安装BBR加速
参考秋水逸冰[一键安装最新内核并开启BBR脚本](https://teddysun.com/489.html){:target="_blank"}  

##### 配置文件示例

###### 单端口配置config.json
```
{
    "server":"0.0.0.0",
    "server_port":8000,
    "local_port":1080,
    "mode":"tcp_and_udp",
    "password":"password",
    "timeout":300,
    "fast_open":true,
    "method":"chacha20-ietf-poly1305",
    "plugin":"v2ray-plugin",
    "plugin_opts":"server"
}
```

---

###### 多端口配置manager.json
```
{
    "server":"0.0.0.0",
    "local_port":1080,
    "mode":"tcp_and_udp",
    "port_password":{
        "8000":"password0",
        "8001":"password1",
        "8002":"password2"
    },
    "timeout":300,
    "fast_open":true,
    "method":"chacha20-ietf-poly1305",
    "plugin":"v2ray-plugin",
    "plugin_opts":"server"
}
```

---

##### 相关命令

<ol>
    <li><font size=3>nohup ss-server -c /etc/shadowsocks-libev/config.json >~/shadowsocks.log 2>&1 &</font></li>
    <li><font size=3>nohup ss-manager -c /etc/shadowsocks-libev/manager.json >~/shadowsocks.log 2>&1 &</font></li>
    <li><font size=3>pkill ss-server / pkill v2ray-plugin / killall ss-server /killall v2ray-plugin</font></li>
</ol>
