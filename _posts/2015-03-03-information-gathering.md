---
layout: post
title: "情报搜集"
description: ""
category: pentest
tags: [pentest]
---
{% include JB/setup %}


### PTES
[Intelligence Gathering](http://www.pentest-standard.org/index.php/Intelligence_Gathering)

### Kali
[kali](http://www.kali.org/)


### 被动信息搜集
1. [whois](https://zh.wikipedia.org/wiki/WHOIS)
  - 获取域名信息
  - [metasploit](http://www.metasploit.com/) `whois 域名或ip`
  - [chinaz](http://whois.chinaz.com/)
1. [netcraft](http://www.netcraft.com/)
  - 可以获取域名对应的服务器ip地址，网站使用的后台语言等信息。
1. nslookup 系统自带工具，可以获取更多域名服务器的信息。
  - [chinaz](http://tool.chinaz.com/nslookup/)
  - 使用帮助直接 `man nslookup`
1. More On PTES

### 主动信息搜集

#### nmap

nmap -sS -Pn <ip>

    nmap -sS -Pn 10.10.10.129

- -sS
- -Pn
- -A

#### ipidseq TCP空闲扫描

    use auxiliary/scanner/ip/ipidseq
    show options
    set RHOSTS 10.10.10.0/24
    set THREADS 50
    run

get "Incremental" ip, nmap参数 -sI 指定空闲主机ip

    nmap -Pn -sI <incremental ip> <target ip>

## 其他
- 要具备从攻击者角度思考问题的能力

- 网页搜索
- google hacking
- 网络拓扑扫描映射

