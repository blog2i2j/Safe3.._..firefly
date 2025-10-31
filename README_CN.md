<h1 align="center">
  <br>
  <img src="https://github.com/Safe3/firefly/blob/main/logo.png" alt="firefly" width="70px">
</h1>
<h4 align="center">萤火虫 WireGuard Server</h4>

<p align="center">
<a href="https://github.com/Safe3/firefly/releases"><img src="https://img.shields.io/github/downloads/Safe3/firefly/total">
<a href="https://github.com/Safe3/firefly/graphs/contributors"><img src="https://img.shields.io/github/contributors-anon/Safe3/firefly">
<a href="https://github.com/Safe3/firefly/releases/"><img src="https://img.shields.io/github/release/Safe3/firefly">
<a href="https://github.com/Safe3/firefly/issues"><img src="https://img.shields.io/github/issues-raw/Safe3/firefly">
<a href="https://github.com/Safe3/firefly/discussions"><img src="https://img.shields.io/github/discussions/Safe3/firefly">
</p>
<p align="center">
  <a href="#dart-特色">特色</a> •
  <a href="#rocket-使用">使用</a> •
  <a href="#gift_heart-感谢">感谢</a> •
  <a href="#kissing_heart-联系">联系</a> •
  <a href="#key-授权">授权</a>
</p>




<p align="center">
  <a href="https://github.com/Safe3/firefly/blob/main/README.md">English</a>
  <br/><br/>
  ⭐请帮我们点个star以支持我们不断改进，谢谢！
</p>




---

最简单易用的轻量级、高性能 WireGuard 服务端软件，可广泛用于异地组网、远程办公、内网穿透等场景。

🏠 全功能在线SAAS版请访问官网：https://qq.uusec.com/

<h3 align="center">
  <img src="https://github.com/Safe3/firefly/blob/main/firefly_cn.png" alt="firefly" width="700px">
  <br>
</h3>

## :dart: 特色

 :green_circle: 提供美观且简单、易用的web管理后台

 :purple_circle: 支持所有原生 WireGuard 客户端接入

 :yellow_circle: 小巧轻量级，不到13M大小，不依赖WireGuard

 :orange_circle: go语言开发，单文件、高性能、支持多CPU架构

 :red_circle: 支持自动申请免费SSL证书并续期

 :large_blue_circle: 支持TCP协议中转，防UDP QoS限流（高级版）

## :rocket: 使用

萤火虫支持Linux x86、ARM CPU架构，服务端和客户端下载地址:  https://github.com/Safe3/firefly/releases  。



- ### 服务端安装

准备一台公网IP服务器，选择对应的CPU架构的二进制文件，如x86 64环境请下载[firefly-linux-amd64](https://github.com/Safe3/firefly/releases/download/v4.4/firefly-linux-amd64)

前期准备：

```bash
mkdir -p /opt/firefly && mv firefly-linux-amd64 /opt/firefly/firefly
```

服务安装：

```bash
chmod +x /opt/firefly/firefly && sudo /opt/firefly/firefly -s install
```

启动运行：

```bash
sudo /opt/firefly/firefly -s start
```

如果你想使用容器版，可以下载docker-compose.yml文件然后执行如下命令启动：

```bash
docker compose up -d
```

访问 http://ip:50121 登录管理后台，默认密码firefly

> :biohazard: ***如果服务器使用的是各种云服务，记得在云服务管理后台上开放萤火虫所需的udp端口50120、tcp端口50121和50122***



- ### 服务端配置


首次运行firefly会在软件目录生成conf/config.json配置文件，配置说明如下：

```json
{
 "version": 4.3,              // 萤火虫当前版本
 "host": "7.7.7.7",           // 萤火虫web管理后台ip或域名，默认为自动获取的公网ip
 "port": 50121,               // 萤火虫web管理后台端口
 "auto_ssl": false,           // 萤火虫web是否启用自动申请免费SSL证书并续期，启用前将web端口改为443并配置host为域名
 "password": "firefly",       // 萤火虫web管理后台登录认证密码
 "lang": "en",                // 萤火虫web管理后台多语言支持，中文请将en改为cn
 "ui_traffic_stats": true,    // 萤火虫web管理后台是否开启流量图特效
 "ui_chart_type": 2,          // 萤火虫web管理后台流量特效图类型
 "log_level": "error",        // 萤火虫服务端日志记录等级
 "wg_private_key": "YBw5KAo1vM2mz35GLhZB01ZNYWJYWdGZNQT1MebuCHk=",  // 萤火虫服务端 WireGuard 私钥
 "wg_device": "eth0",                   // 萤火虫服务端 WireGuard 出入流量网卡名称
 "wg_port": 50120,                      // 萤火虫服务端 WireGuard UDP端口
 "wg_mtu": 1280,                        // 萤火虫服务端 WireGuard MTU值
 "wg_persistent_keepalive": 25,         // 萤火虫客户端存活包发送间隔时间
 "wg_address": "198.18.0.1/15",         // 萤火虫客户端虚拟ip网段范围
 "wg_dns": "8.8.8.8",                   // 萤火虫客户端dns配置
 "wg_allowed_ips": "0.0.0.0/0, ::/0",   // 萤火虫客户端要转发流量到服务端的ip地址范围，默认所有流量
 "wg_proxy_address": ":50122"           // 萤火虫TCP协议中转监听地址，可防止UDP QoS限流
}
```



- ### 客户端安装

萤火虫支持所有原生WireGuard官方和第三方客户端，包括Windows、Linux、Mac、iOS、Android，下载地址：[https://github.com/Safe3/firefly/releases](https://github.com/Safe3/firefly/releases) ，根据提示一步步安装。



- ### 客户端配置

登录萤火虫服务端web管理后台，新建2个客户端，通过以下方式导入WireGuard客户端配置。

1.移动客户端可直接扫描萤火虫后台二维码导入配置

2.Windows、Mac客户端可下载萤火虫后台配置文件到本地后从WireGuard界面导入配置

3.Linux客户端将配置文件保存到/etc/wireguard/firefly.conf，执行wg-quick up firefly启动wireguard，开机自启动systemctl enable wg-quick@firefly

两个客户端启动之后，可以通过萤火虫服务端分配的ip 198.18.0.x 直接相互访问


## :1st_place_medal: 产品列表

来自我们的其它伟大产品：

[南墙](https://github.com/Safe3/uusec-waf) - 一款工业级免费、高性能、高扩展，支持AI和语义引擎的Web应用和API安全防护产品。

[OpenResty管家](https://github.com/Safe3/openresty-manager) - 最简单易用、功能强大、漂亮的主机管理面板，OpenResty Edge 的开源替代品。

[森罗万象](https://github.com/Safe3/CVS) - 强大的网络空间测绘、资产管理、漏洞扫描等全生命漏洞周期的综合攻击面管理平台，化繁为简，以一御百。


## :gift_heart: 感谢

由于开源后社区贡献代码为零，本项目不再开源。此repo仅供反馈bug和提建议，请支持萤火虫的朋友点个 :heart: 赞！

<p align="center">
<a href="https://github.com/Safe3/firefly/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Safe3/firefly&max=500">
</a>
</p>
捐赠请扫描如下二维码：
<img src="https://waf.uusec.com/_media/sponsor.jpg" alt="捐赠"  height="300px" />



## :kissing_heart: 联系

若想支持更多功能，如权限分组、高级路由、堡垒机、点对点传输等，请访问鹊桥: https://qq.uusec.com

- 问题提交：https://github.com/Safe3/firefly/issues

- 讨论社区：https://github.com/Safe3/firefly/discussions

- 官方 QQ 群：11500614

- 官方微信群：微信扫描以下二维码加入

  <img src="https://waf.uusec.com/_media/weixin.jpg" alt="微信群"  height="200px" />



## :key: 授权

萤火虫仅限于个人免费使用，请遵守本国法律，如要购买源码请联系我们获取商业授权。
