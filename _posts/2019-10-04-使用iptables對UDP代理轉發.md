---
title: "使用iptables對UDP代理轉發"
date: 2019-10-02
categories:
  - blog
tags:
  - 代理轉發
  - 代理
---
對於其他設備，直接打上標籤仍給TPROXY 目標。對於本地包，要在V2RAY_MARK 鏈上打一個標籤，觸發 reroute check 。
```c
ip rule add fwmark 0x01/0x01 table 100
ip route add local 0.0.0.0/0 dev lo table 100
iptables -t mangle -N V2RAY
iptables -t mangle -N V2RAY_MARK
iptables -t mangle -A V2RAY -p udp --dport  <一號伺服器出口端口> -j TPROXY --on-port  <二號伺服器入口端口> --tproxy-mark 0x01/0x01
iptables -t mangle -A V2RAY  -d 0.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY  -d 10.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY  -d 100.64.0.0/10 -j RETURN
iptables -t mangle -A V2RAY  -d 127.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY  -d 169.254.0.0/16 -j RETURN
iptables -t mangle -A V2RAY  -d 172.16.0.0/12 -j RETURN
iptables -t mangle -A V2RAY  -d 192.0.0.0/24 -j RETURN
iptables -t mangle -A V2RAY  -d 192.0.2.0/24 -j RETURN
iptables -t mangle -A V2RAY  -d 192.88.99.0/24 -j RETURN
iptables -t mangle -A V2RAY  -d 192.168.0.0/16 -j RETURN
iptables -t mangle -A V2RAY  -d 198.18.0.0/15 -j RETURN
iptables -t mangle -A V2RAY  -d 198.51.100.0/24 -j RETURN
iptables -t mangle -A V2RAY  -d 203.0.113.0/24 -j RETURN
iptables -t mangle -A V2RAY  -d 224.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY  -d 240.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY  -d 255.255.255.255 -j RETURN
iptables -t mangle -A V2RAY -d <出口伺服器地址>  -j RETURN
iptables -t mangle -A V2RAY -p udp -j TPROXY --on-port <一號伺服器入口端口> --tproxy-mark 0x01/0x01
iptables -t mangle -A V2RAY_MARK -p udp --dport <一號伺服器出口端口> -j MARK --set-mark 1
iptables -t mangle -A V2RAY_MARK -d 0.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 10.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 100.64.0.0/10 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 127.0.0.0/8 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 169.254.0.0/16 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 172.16.0.0/12 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 192.0.0.0/24 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 192.0.2.0/24 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 192.88.99.0/24 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 192.168.0.0/16 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 198.18.0.0/15 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 198.51.100.0/24 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 203.0.113.0/24 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 224.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 240.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY_MARK  -d 255.255.255.255 -j RETURN
iptables -t mangle -A V2RAY_MARK -d <出口伺服器地址>  -j RETURN
iptables -t mangle -A V2RAY_MARK -p udp -j MARK --set-mark 1
```
啟用規則
```c
iptables -t mangle -A PREROUTING -j V2RAY
iptables -t mangle -A OUTPUT -j V2RAY_MARK
```