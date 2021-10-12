+++
author = "咸鱼"
title = "搬瓦工+V2ray科学上网搭建新手指南"
date = "2021-10-05"
toc = true
comments = true
description = "搬瓦工（BandwagonHost）教程 + V2Ray + clashX 搭建新手指南"
tags = [
    "搬瓦工",
    "VPS",
    "V2Ray"
]
categories = [
    "VPS"
]
+++

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgbwg_logo.png)
## 一、前言
相较于目前市面上烂大街的 SSR 翻墙，V2RAY在安全、伪装、稳定等方面几乎是碾压 SSR，本教程介绍了如何搭建和使用 V2Ray ,就算是新手只要按照步骤进行操作一样可以搭建成功。

<!--more-->
## 二、准备工作

在搭建工作开始之前，你需要知道你需要经历哪些步骤：

- 购买一个 VPS：想要搭建 V2Ray，就必须要拥有一台 VPS。
- 获取 VPS 信息：我们必须要知道 VPS IP 地址，root 用户密码，SSH 端口
- 安装 Xshell（WINDOWS）iTerm2（macOS）: Xshell 是一个 SSH 客户端，iTerm2 则是 MAC 平台的 SSH客户端。要登录 VPS，当然需要 SSH 客户端
- 登录 VPS: 使用 Xshell 配置 VPS SSH 信息，然后登录
- 安装 V2Ray:安装过程你可以随意选择你喜欢的传输协议或者配置 Shadowsocks
- V2Ray 安装完成: 此时你可以使用客户端配置 V2Ray 使用了

## 三、VPS购买
推荐购买[搬瓦工](https://bwh81.net/aff.php?aff=35290)，[搬瓦工](https://bwh81.net/aff.php?aff=35290)主打小微型 VPS 主机和超低价年付方案。曾经在很长时间内推出过年付不足5美元的超低价 VPS，而且还支持支付宝付款，可以说是对国内用户友好度极佳。 但随着使用人数的增多，[搬瓦工](https://bwh81.net/aff.php?aff=35290)目前已经砍掉了所有的低价套餐，目前在售最低的年付套餐时 49.9 美元，在同类VPS中性价比也算能打。 

一般来说，推荐购买 香港线路 或 CN2 GIA 线路，或者哪个便宜选择那个，如果个人建站练手或使用科学上网的话直接购买[年$49.99CN2(入门) ）](https://bwh81.net/aff.php?aff=35290&pid=57),当然如果你使用量比较多或者想要分享给同学和朋友一起用的话，选择合适的套餐即可。直接年付优惠是最大的,又或者你土豪的话，选择最贵的也行。

销售火爆的套餐：

| 套餐      | CPU | 内存 | 硬盘     | 流量       | 带宽   chch | 价格                   | 购买链接                                               |
| --------- | --- | ---- | -------- | ---------- | ----------- | ---------------------- | ------------------------------------------------------ |
| CN2(入门) | 1核 | 1GB  | 20GB SSD | 1000GB /月 | 1Gbps       | **年$49.99**           | [点击购买](https://bwh81.net/aff.php?aff=35290&pid=57) |
| CN2 GIA-E | 2核 | 1GB  | 20GB SSD | 1000GB /月 | 2.5Gbps     | **季$49.99 年$169.99** | [点击购买](https://bwh81.net/aff.php?aff=35290&pid=87) |
| HK        | 2核 | 2GB  | 40GB SSD | 500GB /月  | 1Gbps       | **季$89.99 年$899.99** | [点击购买](https://bwh81.net/aff.php?aff=35290&pid=95) |


## 四、购买步骤

###  1、核对方案配置以及选择时间期限和机房
![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgprepay.jpg)

我们然后会看到上图所示的界面，根据图示我们需要确定选择的方案以及时间，默认是洛杉矶机房，目前我，点击"ADD TO CART"添加购物车。

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgbwg_checkout.jpg)

>~~可使用`bwh8ZBPVK`优惠码,再减6%.~~(该优惠码失效，使用`BWH3HYATVBJW `优惠6.58%)
核对我们选择方案的价格，没有问题后点击CHECKOUT结账。


### 2、登录或者新注册搬瓦工账户
![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgbwg_register.jpg)

如上图，如果我们有过账户，可以直接点击"Click here to login"登录以及付款就可以，如果还没有账户则需要注册账户。个人信息不要真实的，但也不能太离谱和乱写字符出来，好歹也要稍微用点拼音。

### 3、进入支付选择页面
![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgbgw_pau.png)

选择支付宝完成支付。

## 五、获取 VPS 信息
购买完 VPS 之后，接着我们开始获取 VPS 信息。

1. 选择My Services

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgmy_service.png)

2. 进入kimivm control panel

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgcontrol_panel.jpg)

3. 获取 IP 地址 和 端口号

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgip_port_main.png)

## 六、安装 Xshell（WINDOWS）或 iTerm2（macOS）

1. iTerm2下载地址：[https://iterm2.com/downloads.html](https://iterm2.com/downloads.html)

2. Xshell下载地址：[https://www.netsarang.com/zh/free-for-home-school/](https://www.netsarang.com/zh/free-for-home-school/)

## 七、登录 VPS
以 Xshell登录 VPS 为例，打开软件之后我们需要新建一个窗口SSH.

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgxshell_panel.png)

拿到我们上一步获取到的 IP 和 端口号，填入输入框

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgpwd_input.png)

用户名我们没有特别设置之后，就是默认的root，然后是密码。然后保存之后就可以连接。
![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgpwd_input.png)

小提示：如果连接后出现提示“WARNING! The remote SSH server rejected X11 forwarding request.”，不要担心。运行下面的命令就可以解决，Xshell界面支持鼠标右键的复制粘贴，按回车键就可以运行命令。（键盘的Ctrl+C、Ctrl+V是无效的哦）完成后重新连接vps服务器即可。

```
yum install xorg-x11-xauth -y
```

## 八、安装 V2Ray
输入下面命令回车，你可以复制过去，然后在 Xshell 界面右键或者按 Shift + Insert 即可粘贴。

```
bash <(curl -s -L https://git.io/v2ray.sh)
```

{{% notice tip "Tip" %}}
如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl
ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y
centos 系统安装 Curl 方法: yum update -y && yum install curl -y
安装好 curl 之后就能安装脚本了
{{% /notice %}}

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgv2ray_setting.png)
- 然后选择安装，即是输入 1 回车,
- 选择传输协议，如果没有特别的需求，使用默认的 TCP 传输协议即可，直接回车
- 然后会提示你“请输入 V2Ray 端口”，端口范围在“1-65535”之间，选择端口，如果没有特别的需求，使用默认的端口即可，直接回车
- 是否屏蔽广告，除非你真的需要，一般来说，直接回车即可
- 这时会提示你“是否配置 Shadowsocks ”，默认为“N”不配置 Shadowsocks，输入“Y”回车代表配置 Shadowsocks，直接回车即可。

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgv2ray_config.png)

按照上图信息设置完毕后“回车”会看到下图提示，

———- 安装信息 ————-

V2Ray 传输协议 = TCP

V2Ray 端口 = 54321

是否配置 Shadowsocks = 未配置

———- END ————-

然后提示你“按 Enter 回车键 继续….或按 Ctrl + C 取消”，我们按“Enter”键回车后安装 V2ray，如图（安装信息可能会因你的配置而变化，不用在乎截图信息）：
![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgv2ray_config_confirm.png)

接下来就是 V2ray 的安装过程，耐心等待即可，V2ray 安装完成后如图：
![ =100x100](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/imgv2ray_success.png)

上图的 V2ray 配置信息，用 V2RAY 的客户端配置号上图信息就能正常的科学上网了。

如果需要生成“vmess URL 链接”或者“二维码图片”输入以下命令：

```
# vmess URL 链接
v2ray url
# 二维码图片
v2ray qe
```

## 九、V2Ray 客户端使用教程

在配置服务器成功之后,我们有了上面的 V2ray 配置信息后，通过下载相应的客户端进行配置后就能够连接外网了。

目前我在用的是 **Clash**(颜值在线)，而且除了 iOS 平台下载不方便外，Windows、Mac、Android都已支持。

1. Mac+ClashX: [clashX-v1.30.1.dmg](https://github.com/yichengchen/clashX/releases)
2. Windows+Clash: [Clash.for.windows-0.11.6.exe](https://github.com/Fndroid/clash_for_windows_pkg/releases)
3. Android+Clash: [ClashForAndroid-v2.0.18.apk](https://github.com/Kr328/ClashForAndroid/releases)
4. iOS 用户:目前 App store 上没有免费 V2Ray 客户端，付费的 V2Ray 客户端有：
   - Shadowrocket（俗称小火箭，注意不是 shadowrocket VPN）
   - i2Ray
   - pepi
   - Kitsunebi
   - Quantumult（内置免费节点）
    因政策原因，这些应用在国内 App Store 上无法搜索到，请从其它地方找一个可用的境外 Apple ID，切换 App Store 然后再下载

如果不知道怎么配置客户端的话，可以在更多中查看配置教程。


## 更多
- [V2Ray和SSR有什么区别](https://www.v2rayssr.com/v2rayssr.html)
- [V2Ray 客户端大全](https://v2xtls.org/v2ray%e5%ae%a2%e6%88%b7%e7%ab%af/)
- [Clash for Windows 配置教程](https://v2xtls.org/clash-for-windows%E9%85%8D%E7%BD%AEv2ray%E6%95%99%E7%A8%8B/)
- [ClashX for Mac 配置教程](https://v2xtls.org/clashx%E9%85%8D%E7%BD%AEv2ray%E6%95%99%E7%A8%8B/)
