---
layout: post
title: "草稿：VMWare虚拟网络环境"
description: "pen test environment setup"
category:
tags: []
---
{% include JB/setup %}

### MacOS VMWare Fusion
1. 打开配置文件 /Library/Preferences/VMware Fusion/networking
2. 配置如下:
```
VERSION=1,0
answer VNET_1_DHCP yes
answer VNET_1_DHCP_CFG_HASH D6807541FC324BE58EF1F7B5DAE133518FD0AC57
answer VNET_1_HOSTONLY_NETMASK 255.255.255.0
answer VNET_1_HOSTONLY_SUBNET 192.168.10.0
answer VNET_1_VIRTUAL_ADAPTER yes
answer VNET_8_DHCP yes
answer VNET_8_DHCP_CFG_HASH 433E015E46FA0E2B63810B570A6A9EA4498B9948
answer VNET_8_HOSTONLY_NETMASK 255.255.255.0
answer VNET_8_HOSTONLY_SUBNET 10.10.10.0
answer VNET_8_NAT yes
answer VNET_8_VIRTUAL_ADAPTER yes
```

### 配置各虚拟机的IP
网络适配器改为NAT模式
```
ifconfig
sudo vim /etc/networks/interfaces
```

### NAT路由转发功能
// TODO

### Host-Only模式
// TODO

### VMnet1和VMnet8
// TODO

### hosts文件
```vim /etc/hosts```
// TODO
