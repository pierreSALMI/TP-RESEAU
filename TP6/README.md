# TP 6 - Une topologie qui ressemble un peu à quelque chose, enfin ?

## Lab 1 : Simple OSPF

## Lab 2 : Un peu de complexité (et d'utilité ?...)

### 1. Présentation du lab et contexte

![Image topologie](./images/topologie.PNG)

### 2. Mise en place du lab

#### Checklist IP Routeurs

* Routeur1 :
```
    R1#show ip int br
    Interface                  IP-Address      OK? Method Status                Protocol
    Ethernet0/0                10.6.202.254    YES manual up                    up
    Ethernet0/1                10.6.100.1      YES NVRAM  up                    up
    Ethernet0/2                10.6.100.5      YES NVRAM  up                    up
    Ethernet0/3                unassigned      YES NVRAM  administratively down down

```

* Routeur2 :
```
    R2#show ip int br
    Interface                  IP-Address      OK? Method Status                Protocol
    Ethernet0/0                unassigned      YES NVRAM  administratively down down
    Ethernet0/1                10.6.100.2      YES NVRAM  up                    up
    Ethernet0/2                10.6.100.9      YES NVRAM  up                    up
    Ethernet0/3                unassigned      YES NVRAM  administratively down down

```

* Routeur3 :
```
    R3#show ip int br
    Interface                  IP-Address      OK? Method Status                Protocol
    Ethernet0/0                10.6.101.1      YES NVRAM  up                    up
    Ethernet0/1                10.6.100.14     YES NVRAM  up                    up
    Ethernet0/2                10.6.100.10     YES NVRAM  up                    up
    Ethernet0/3                unassigned      YES NVRAM  administratively down down
```

* Routeur4 :
```
    R4#show ip int br
    Interface                  IP-Address      OK? Method Status                Protocol
    Ethernet0/0                unassigned      YES NVRAM  administratively down down
    Ethernet0/1                10.6.100.13     YES NVRAM  up                    up
    Ethernet0/2                10.6.100.6      YES NVRAM  up                    up
    Ethernet0/3                unassigned      YES NVRAM  administratively down down
```

* Routeur5 :
```
    R5#show ip int br
    Interface                  IP-Address      OK? Method Status                Protocol
    Ethernet0/0                10.6.101.2      YES NVRAM  up                    up
    Ethernet0/1                10.6.201.254    YES NVRAM  up                    up
    Ethernet0/2                unassigned      YES NVRAM  administratively down down
    Ethernet0/3                unassigned      YES NVRAM  administratively down down
```

#### Checklist VMs

* Client1 :
```
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
        link/ether 08:00:27:ad:41:08 brd ff:ff:ff:ff:ff:ff
        inet 10.6.201.10/24 brd 10.6.201.255 scope global noprefixroute enp0s3
        valid_lft forever preferred_lft forever
        inet6 fe80::a00:27ff:fead:4108/64 scope link
        valid_lft forever preferred_lft forever
```

* Client2 :
```
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
        link/ether 08:00:27:91:08:dd brd ff:ff:ff:ff:ff:ff
        inet 10.6.201.11/24 brd 10.6.201.255 scope global noprefixroute enp0s3
        valid_lft forever preferred_lft forever
        inet6 fe80::a00:27ff:fe91:8dd/64 scope link
        valid_lft forever preferred_lft forever
```

* Server1 :
```
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
        link/ether 08:00:27:a0:8a:56 brd ff:ff:ff:ff:ff:ff
        inet 10.6.202.10/24 brd 10.6.202.255 scope global noprefixroute enp0s3
        valid_lft forever preferred_lft forever
        inet6 fe80::a00:27ff:fea0:8a56/64 scope link
        valid_lft forever preferred_lft forever
```

#### Configuration de OSPF

* Client1 ping server1 :
```
    [user@client1 ~]$ ping server1
    PING server1 (10.6.202.10) 56(84) bytes of data.
    64 bytes from server1 (10.6.202.10): icmp_seq=2 ttl=60 time=75.9 ms
    64 bytes from server1 (10.6.202.10): icmp_seq=3 ttl=60 time=71.1 ms
    64 bytes from server1 (10.6.202.10): icmp_seq=4 ttl=60 time=82.4 ms
    64 bytes from server1 (10.6.202.10): icmp_seq=5 ttl=60 time=76.4 ms
    ^C
    --- server1 ping statistics ---
    5 packets transmitted, 4 received, 20% packet loss, time 4010ms
    rtt min/avg/max/mdev = 71.127/76.494/82.454/4.033 ms
```

* Client2 ping server1 :
```
    [user@client2 ~]$ ping server1
    PING server1 (10.6.202.10) 56(84) bytes of data.
    64 bytes from server1 (10.6.202.10): icmp_seq=1 ttl=60 time=77.3 ms
    64 bytes from server1 (10.6.202.10): icmp_seq=2 ttl=60 time=87.1 ms
    64 bytes from server1 (10.6.202.10): icmp_seq=3 ttl=60 time=73.7 ms
    ^C
    --- server1 ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2003ms
    rtt min/avg/max/mdev = 73.765/79.423/87.162/5.672 ms
```

* server1 ping client1 :
```
    [user@server1 ~]$ ping client1
    PING client1 (10.6.201.10) 56(84) bytes of data.
    64 bytes from client1 (10.6.201.10): icmp_seq=1 ttl=60 time=73.8 ms
    64 bytes from client1 (10.6.201.10): icmp_seq=2 ttl=60 time=69.7 ms
    64 bytes from client1 (10.6.201.10): icmp_seq=3 ttl=60 time=75.4 ms
    ^C
    --- client1 ping statistics ---
    3 packets transmitted, 3 received, 0% packet loss, time 2004ms
    rtt min/avg/max/mdev = 69.741/72.983/75.406/2.394 ms
```

* server1 ping client2 :
```
    [user@server1 ~]$ ping client2
    PING client2 (10.6.201.11) 56(84) bytes of data.
    64 bytes from client2 (10.6.201.11): icmp_seq=2 ttl=60 time=60.6 ms
    64 bytes from client2 (10.6.201.11): icmp_seq=3 ttl=60 time=76.5 ms
    64 bytes from client2 (10.6.201.11): icmp_seq=4 ttl=60 time=71.5 ms
    64 bytes from client2 (10.6.201.11): icmp_seq=5 ttl=60 time=76.8 ms
    ^C
    --- client2 ping statistics ---
    5 packets transmitted, 4 received, 20% packet loss, time 4007ms
    rtt min/avg/max/mdev = 60.663/71.416/76.894/6.570 ms
```