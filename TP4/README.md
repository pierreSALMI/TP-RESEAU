# TP4 - Routage Statique

## I. Mise en place du lab

### 1. Création des réseaux
Création de deux cartes réseau ayant comme IP : 10.1.0.1 et 10.2.0.1 sans serveur DHCP.

### 2. Création des VMs
On clone 3 VMs depuis la VM patron.

- [x] Désactiver SELinux (fait sur le patron)
- [x] Installation de certains paquets dans le patron (fait sur le patron)
- [x] Désactivation de la carte NAT (fait sur le patron)
- [x] Définition des IPs statiques
- [x] Connexion SSH
    * client1 `ssh user@10.1.0.10 `
    * server1 `ssh user@10.2.0.10 `
    * router1 `ssh user@10.1.0.254 `

- [x] Définition du nom de domaine
    * `[user@client1 ~]$ hostname --fqdn client1 `
    * `[user@routeur1 ~]$ hostname --fqdn routeur1.tp4`
    * ` [user@server1 ~]$ hostname --fqdn server1`

- [x] Remplissage du fichier /etc/hosts

client1 :
``` 
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.2.0.10 server1 server1.tp4
10.1.0.254 router1 router1.tp4 
```

server1 :
```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.1.0.10 client1 client1.tp4
10.2.0.254 router1 router1.tp4
```

router1 :
```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.2.0.10 server1 server1.tp4
10.1.0.10 client1 client1.tp4
```

- [x] client1 ping router 1

```
[user@client1 ~]$ ping router1
PING router1 (10.1.0.254) 56(84) bytes of data.
64 bytes from router1 (10.1.0.254): icmp_seq=1 ttl=64 time=0.720 ms
64 bytes from router1 (10.1.0.254): icmp_seq=2 ttl=64 time=0.769 ms
64 bytes from router1 (10.1.0.254): icmp_seq=3 ttl=64 time=0.858 ms
64 bytes from router1 (10.1.0.254): icmp_seq=4 ttl=64 time=0.734 ms
^C
--- router1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3009ms
rtt min/avg/max/mdev = 0.720/0.770/0.858/0.057 ms
```

- [x] server1 ping router1

```
[user@server1 ~]$ ping router1
PING router1 (10.2.0.254) 56(84) bytes of data.
64 bytes from router1 (10.2.0.254): icmp_seq=1 ttl=64 time=1.19 ms
64 bytes from router1 (10.2.0.254): icmp_seq=2 ttl=64 time=0.854 ms
64 bytes from router1 (10.2.0.254): icmp_seq=3 ttl=64 time=0.458 ms
64 bytes from router1 (10.2.0.254): icmp_seq=4 ttl=64 time=0.375 ms
^C
--- router1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 0.375/0.720/1.193/0.327 ms
```

### 3. Mise en lace du routage statique

1. Router1
```
[user@routeur1 ~]$ ip route
10.1.0.0/24 dev enp0s8 proto kernel scope link src 10.1.0.254 metric 100
10.2.0.0/24 dev enp0s9 proto kernel scope link src 10.2.0.254 metric 101
```

2. client1
```
[user@client1 ~]$ ip route show
10.1.0.0/24 dev enp0s8 proto kernel scope link src 10.1.0.10 metric 100
10.2.0.0/24 via 10.2.0.254 dev enp0s8 proto static metric 100
10.2.0.254 dev enp0s8 proto static scope link metric 100
```

3. server1
```
[user@server1 ~]$ ip route show
10.1.0.0/24 via 10.1.0.254 dev enp0s8 proto static metric 100
10.1.0.254 dev enp0s8 proto static scope link metric 100
10.2.0.0/24 dev enp0s8 proto kernel scope link src 10.2.0.10 metric 100
```

4. test
    * client1 ``` [user@client1 ~]$ ping server1
PING server1 (10.2.0.10) 56(84) bytes of data.
64 bytes from server1 (10.2.0.10): icmp_seq=1 ttl=63 time=0.778 ms
64 bytes from server1 (10.2.0.10): icmp_seq=2 ttl=63 time=1.41 ms
64 bytes from server1 (10.2.0.10): icmp_seq=3 ttl=63 time=1.39 ms
^C
--- server1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.778/1.195/1.411/0.298 ms ```