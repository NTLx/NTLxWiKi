---
title: 晶准远程办公说明
description: 
published: true
date: 2020-04-08T13:35:53.312Z
tags: 
---

# 实现方法

1. 首先通过连接VPN的方式，使自己的电脑能够连接到公司局域网内
2. 成功连接VPN后即可使用与公司内完全一致的网络资源
3. 对于已经完成全部工作文件备份的同事，可直接使用文件中心

## VPN 连接

### PPTP

1. 在任意系统的电脑或手机等设备的互联网（或网络）相关设置中，找到 VPN 设置
2. 添加新的 `PPTP` VPN 连接
3. 服务器地址为 `cubicise.ntlx.xyz`，账户名和密码与公司内账户相同
4. 保存 VPN 连接信息，连接即可

> 现代操作系统均提供在设置中搜索的功能，可直接搜索关键字“VPN”进入相关设置。

## 使用文件服务器

- VPN 连接成功后，浏览器直接访问 http://dsm.cm.com 即可使用文件中心（若此网址无法访问，可参考[公司网络资源目录](/Cubicise/Service)使用替代网址访问）
- VPN 连接成功后，Synology Drive、Chat、Note 等程序也可以连接到文件中心，与在公司的使用完全一致，可参考[公司内部文件服务器说明](/Cubicise/NAS)

## 使用远程桌面

- VPN连接成功后，远程桌面的使用与在公司内完全一致，可参考[公司内部办公中心说明](/Cubicise/VMPC)

# 备注

- VPN连接成功后，能使用的资源可参考[公司网络资源目录](/Cubicise/Service)
- 尚未完成全部工作文件备份的同事，请联系管理员帮忙将自己在公司的办公电脑开通远程功能，开通后的使用方法参考上文 `使用远程桌面`