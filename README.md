# Hi Hysteria

## 一·简介

> Hysteria 是一个功能丰富的，专为恶劣网络环境进行优化的网络工具（双边加速），比如卫星网络、拥挤的公共 Wi-Fi、在**中国连接国外服务器**等。 基于修改版的 QUIC 协议。

Hysteria这是一款由go编写的非常优秀的“轻量”代理程序，它很好的解决了在搭建富强魔法服务器时最大的痛点——**线路拉跨**。

在魔法咏唱时最难的不是搭建维护，而是在晚高峰时期的交付质量。~~当三大运营商晚高变成了：奠信、连不通、移不动时，你我都有感触。~~ 虽然是走的udp但是提供obfs，暂时不会被运营商针对性的QoS(不开obfs也不会被QoS)。

1、原项目提供的bench:

![image](https://raw.githubusercontent.com/HyNetwork/hysteria/master/docs/bench/bench.png)

2、50mbps北方电信,北京出口 直连落地vir San Jose机房163线路，22-23点测试YT 1080p60直播流:

![image](imgs/speed.png)

```
190 dropped of 131329
```

3、无对钟国大陆线路优化，洛杉矶shockhosting机房，1c128m ovznat 4k@p60：
![image](imgs/yt.jpg)

```
139783 Kbps
```

该项目仅作学习用途，请查看的访客在5s之内立即删除并停止使用。

由它所引起的任何问题，作者并不承担风险和任何法律责任。

因为脚本现处于0.x的测试版本，可能会有一些bug，如果遇到请发issue，欢迎star，您的⭐是我维护的动力。

适配ubuntu/debian, centos/rhel操作系统,misple/arm/x86/s390x架构。

```
通知: 请使用wechat-video且hysteria Core版本低于1.2.1的用户更新双端
因为hysteria 1.2.1修复了不开obfs导致wechat-video失效的bug,如果不更新
会导致无法连接

(2022/09/10) 0.4.1:
1. 减小配置检测时等待时间，增加等待检测进程关闭的时间
2. 新增常见问题
```

[历史改进](md/log.md)

## 二·使用

### 第一次使用?

#### 1. [防火墙问题](md/firewall.md)

#### 2. [自签证书](md/certificate.md)

#### 3. [限制UDP的服务商排雷列表【2022/03/21更新】](md/blacklist.md)

#### 4. [hysteria各个协议介绍](md/protocol.md)

#### 5. [如何设置我的延迟、上行/下行速度？](md/speed.md)

#### 6. [支持的客户端](md/client.md)

#### 7. [常见问题/通知](md/issues.md)

### 拉取安装

```
su - root #switch to root user.
bash <(curl -fsSL https://git.io/hysteria.sh)
```

### 配置过程

首次安装后: `hihy`命令调出菜单,如更新了hihy脚本，请执行选项 `9`或者 `12`,获得最新的配置

```
 -------------------------------------------
|**********      Hi Hysteria       **********|
|**********    Author: emptysuns   **********|
|**********     Version: 0.4.1     **********|
 -------------------------------------------
Tips:hihy 命令再次运行本脚本.
............................................. 
############################### 

..................... 
1)  安装 hysteria 
2)  卸载 
..................... 
3)  启动 
4)  暂停 
5)  重新启动 
6)  运行状态 
..................... 
7)  更新Core 
8)  查看当前配置 
9)  重新配置 
10) 切换ipv4/ipv6优先级 
11) 更新hihy 
12) 完全重置所有配置 
13) 修改当前协议类型 

############################### 


0)退出 
............................................. 
请选择:
```

**脚本每次更新都可能会发生改变，请一定要展开并仔细参考演示过程，避免发生不必要的错误！**

<details>
  <summary>演示较长，点我查看</summary>
    <pre><blockcode> 
Local core version:v1.1.0
Remote core version:v1.1.0
Already the latest version.Ignore.
开始配置:
请选择证书申请方式:

1、使用ACME申请(推荐,需打开tcp 80/443)
2、使用本地证书文件
3、自签证书

输入序号:
3
请输入自签证书的域名(默认:wechat.com):

您已选择自签wechat.com证书加密.公网ip:1.2.3.4
请输入你想要开启的端口,此端口是server端口,建议10000-65535.(默认随机)

随机端口:12854

选择协议类型:

1、udp(QUIC)
2、faketcp
3、wechat-video(回车默认)

输入序号:
1
传输协议:udp

请输入您到此服务器的平均延迟,关系到转发速度(默认200,单位:ms):
180

期望速度,这是客户端的峰值速度,服务端默认不受限。Tips:脚本会自动*1.25做冗余，您期望过低或者过高会影响转发效率,请如实填写!
请输入客户端期望的下行速度:(默认50,单位:mbps):
200
请输入客户端期望的上行速度(默认10,单位:mbps):
40
请输入认证口令:
pekopeko

配置录入完成!

执行配置...

install.sh: line 618: 11172 Killed                  /etc/hihy/bin/appS -c /etc/hihy/conf/hihyServer.json server > /tmp/hihy_debug.info 2>&1

安装成功,请查看下方配置详细信息

1* [v2rayN/nekoray/hihy_cmd] 使用hysteria core直接运行
客户端配置文件输出至: /root/config.json ( 直接下载生成的配置文件[推荐] / 自行复制粘贴下方配置到本地 )
Tips:客户端默认只开启http(8888)、socks5(8889)代理!其他方式请参照hysteria文档自行修改客户端config.json
↓***********************************↓↓↓copy↓↓↓*******************************↓
{
"server": "1.2.3.4:12854",
"protocol": "udp",
"up_mbps": 50,
"down_mbps": 250,
"http": {
"listen": "127.0.0.1:10809",
"timeout" : 300,
"disable_udp": false
},
"socks5": {
"listen": "127.0.0.1:10808",
"timeout": 300,
"disable_udp": false
},
"alpn": "h3",
"acl": "acl/routes.acl",
"mmdb": "acl/Country.mmdb",
"auth_str": "pekopeko",
"server_name": "wechat.com",
"insecure": true,
"recv_window_conn": 23592960,
"recv_window": 94371840,
"disable_mtu_discovery": true,
"resolver": "https://223.5.5.5:443/dns-query",
"retry": 3,
"retry_interval": 3
}
↑***********************************↑↑↑copy↑↑↑*******************************↑

2* [Shadowrocket/Sagernet/Passwall] 一键链接:
hysteria://1.2.3.4:12854?protocol=udp&auth=pekopeko&peer=wechat.com&insecure=1&upmbps=50&downmbps=250&alpn=h3#Hys-1.2.3.4

3* [Clash.Meta] 推荐!配置文件已在/root/metaHys.yaml输出,请下载至客户端使用(beta)

  `</blockcode></pre>`

</details>

## 三·选读

#### 1. [借用其他支持Socks5的GUI，来获得一个图形界面](https://github.com/emptysuns/Hi_Hysteria/blob/main/md/gui.md)

## 四·Todo

**如果您有好的功能建议，请不要忘记开个issue提出来欧～～～欢迎PR来完成Todo或者给我纠正我的渣代码**

**我的爱好是写bug （￣▽￣）~**

* [X] 检测端口是否被占用
* [ ] 利用xray s5 inbound来支持按域名分流(warp)
* [X] 生成分享链接
* [X] hihy替换掉hysteria
* [ ] 规范化脚本代码
* [ ] 提供docker和systemd(已完成)两种运行方式
* [ ] 多密码支持
* [ ] 利用base64加密替换原来的auth_str
* [X] 兼容v2rayN,放弃cmd的更新
* [X] 支持clash.meta核心
* [ ] 优化clash配置选项
* [ ] 支持sing-box作为core运行方式
* [ ] 提供查看实时log选项
* [ ] 生成clash配置时，提供一个远程链接来代替本地导入

## 五·结语

魔改UDP的QUIC协议，加了tls和混淆的话，个人跑了一段时间大流量，未被运营商QoS，落地ip并没有被墙，也不知道什么时候被针对，大家且用且珍惜吧。

## 六·鸣谢

[@HyNetwork/hysteria](https://github.com/HyNetwork/hysteria)

[@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip)

[@mack-a/v2ray-agent](https://github.com/mack-a/v2ray-agent)

[@2dust/v2rayN](https://github.com/2dust/v2rayN)

[@Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)

[@zzzgydi/clash-verge](https://github.com/zzzgydi/clash-verge)

[@MetaCubeX/Clash.Meta](https://github.com/MetaCubeX/Clash.Meta)
