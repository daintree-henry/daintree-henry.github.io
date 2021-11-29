---
layout: post
title:  "Bastion Node 설치"
date:   2021-11-29 10:31:00 +0900
nav_order: 1
---

## Bastion Node 설치
- 각 노드의 게이트웨이 역할 및 외부에서 SSH 접근을 위한 Bastion 노드를 설치한다.
- CENTOS7로 설치하였으며 리소스는 1 vCPU / 1GB RAM / 32GB Storage를 할당하였다.
- Bastion 노드는 마스터/워커 노드의 외부 접근 및 로드밸런싱을 위한 LB를 설치할 것이다. 또한 SSH로 접근하여 Kubernetes 설치 및 명령어를 실행하는 Client 역할도 수행할 것이다.

![](../_homekube/images/쿠버네티스%20개인%20서버%20구축-Bastion%20Node생성.png)

<br>



왼쪽 위 도구 -> 환경 설정 -> 네트워크 ->  
NAT 네트워크가 없으면 오른쪽 +를 눌러 생성 후 톱니바퀴를 클릭
네트워크 CIDR을 10.0.2.0/24로 설정 ->
포트포워딩 규칙을 아래와 같이 설정
![](../_homekube/images/쿠버네티스%20개인%20서버%20구축-버추얼박스포트포워딩.png)


Bastion Node의 IP는 10.0.2.6 고정 IP로 할당했다.
```shell
[root@localhost ~]# cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
UUID=406606f1-4b2c-4357-8fde-19c29436edb6
DEVICE=enp0s3
ONBOOT=yes
IPV4_ADDRESS=10.0.2.6/24

[root@localhost ~]# service network restart
Restarting network (via systemctl):                        [  OK  ]

[root@localhost ~]# ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default      qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP g     roup default qlen 1000
    link/ether 08:00:27:3e:19:eb brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.6/24 brd 10.0.2.255 scope global noprefixroute dynamic enp0s3
       valid_lft 548sec preferred_lft 548sec
    inet6 fe80::8a85:2f03:164b:3558/64 scope link noprefixroute
       valid_lft forever preferred_lft forever

```

이제 외부에서 12.34.56.78:22에 접속해 보면 정상적으로 Bastion 노드에 접속한 것을 확인할 수 있다.



{% if site.disqus-shortname %}
  {% include disqus.html %}
{% endif %}