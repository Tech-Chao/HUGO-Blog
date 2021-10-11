+++
author = "Hugo Authors"
title = "Emoji Support"
date = "2019-03-05"
description = "Guide to emoji usage in Hugo"
tags = [
    "搬瓦工 VPS",
]
+++

![](https://upload-images.jianshu.io/upload_images/1178839-d36dc2a666fcf1b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 简介
[搬瓦工](https://bwh8.net/aff.php?aff=35290)是一个低价VPS品牌，主打小微型vps主机和超低价年付方案。曾经在很长时间内推出过年付不足5美元的超低价VPS，而且还支持支付宝付款，可以说非常适合国内用户搭建科学上网工具VPN使用。 <!--more-->目前已经没有这样的低价方案了，不过现在最低的年付19美元的VPS依然销售，已经算是在同类VPS中价格最低的了。~~还可使用`bwh8ZBPVK`优惠码，在付款时再减6%~~(该优惠码失效，使用`BWH26FXH3HIQ `优惠6.25%)。 目前[搬瓦工](https://bwh8.net/aff.php?aff=35290)提供KVM和OpenVZ两种架构.个人建议选择`KVM架构`，理由就是`KVM`相对稳定。

 
目前[搬瓦工](https://bwh8.net/aff.php?aff=35290)销售的方案如下, 如果个人建站练手或使用科学上网的话直接购买[年19.99方案（KVM架构）](https://bwh8.net/aff.php?aff=35290&pid=43)。直接年付优惠是最大的,

[年付19.99方案（KVM架构）点击直达链接](https://bwh8.net/aff.php?aff=35290&pid=43)：

| 内存  | 硬盘     | 流量     | 价格         |
| ----- | -------- | -------- | ------------ |
| 512MB | 10GB SSD | 500GB/月 | **年$19.99** |


# 购买步骤

##  一、核对方案配置以及选择时间期限和机房
![](http://upload-images.jianshu.io/upload_images/1178839-3d8bfdf0eca044af.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
我们然后会看到上图所示的界面，根据图示我们需要确定选择的方案以及时间，默认是洛杉矶机房，我们也可以选择其他的几个机房之一，点击"ADD TO CART"添加购物车。

![](http://upload-images.jianshu.io/upload_images/1178839-44c56ea845241d08.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>~~可使用`bwh8ZBPVK`优惠码,再减6%.~~(该优惠码失效，使用`BWH26FXH3HIQ `优惠6.25%)
核对我们选择方案的价格，没有问题后点击CHECKOUT结账。

由于使用搬瓦工科学上网人数较多，部分ip被禁，搬瓦工官方取消了一部分服务器的一键安装ss功能，所以在这里记录下自行搭建ss功能方法。

## 二、登录或者新注册搬瓦工账户
![](http://upload-images.jianshu.io/upload_images/1178839-dd79e983cc56cd15.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

根据上图，如果我们有过账户，可以直接点击"Click here to login"登录以及付款就可以，如果还没有账户则需要注册账户。个人信息不要真实的，但也不能太离谱和乱写字符出来，好歹也要稍微用点拼音。

## 三、进入支付选择页面
![](https://upload-images.jianshu.io/upload_images/1178839-7fbdb59539b9e1c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



# 搭建服务器
购买完vps之后，接着我们开始搬瓦工vps的搭建。

1. 选择My Services
![](https://upload-images.jianshu.io/upload_images/1178839-83daa6f1e707f44d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 进入kimivm control panel
![](https://upload-images.jianshu.io/upload_images/1178839-867b43a403ab0307.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 安装shaowscocks服务器(如果没有此选项，直接跳到第4步).
![](https://upload-images.jianshu.io/upload_images/1178839-b6f40095140676c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/1178839-5167fb04c29ba84d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.[搬瓦工——SSH脚本方式安装Shadowsocks](https://blog.csdn.net/yuwuchaio/article/details/81567324)
如果上述步骤都顺利完成了的话，服务器应该已经搭建完成。接下来我们需要在客户端安装上网工具用来连接VPS服务器就可以科学上网了。

# 配置shadowsocks本地客户端
在配置服务器成功之后，搬瓦工有提示本地客户端的安装推荐，给出原始下载地址,如果链接失效，可以百度自行下载:

1. Android用户:[Android 客户端点击下载](https://github.com/shadowsocksr-backup/shadowsocksr-android/releases/download/3.4.0.8/shadowsocksr-release.apk)。

2. Windows 用户：[Windows 客户端点击下载](https://github.com/shadowsocksr-backup/shadowsocksr-csharp/releases/download/4.7.0/ShadowsocksR-4.7.0-win.7z)。

3. Mac 用户：[Mac 客户端点击下载](https://github.com/shadowsocksr-backup/ShadowsocksX-NG/releases/download/1.4.2-R8-subscribe-alpha-3/ShadowsocksX-NG-R8.dmg)。

4. iOS 用户: 国区商店App 已下架。可自行使用`PP助手`同步`Wingy`、`shadowsocksR`。非国区账号可在App store 搜索`Wingy`等。


打开各本地客户端配置方式大致相同。以Mac为例

## Mac
安装完成之后即可看到小飞机ss在右上角运行，然后再点击“服务器设置”，在打开的窗口左下角点击“+”号，之后再填写ss(Shadowsocks Server)服务器信息（在搭建完成服务器时生成的信息填入）打开Shadowsocks即可科学上网了！参考如下图：
![](https://upload-images.jianshu.io/upload_images/1178839-2b615136f96ba894.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
