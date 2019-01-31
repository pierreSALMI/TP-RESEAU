#TP4 - Routage Statique

##I. Mise en place du lab

1. Création des réseaux
Création de deux cartes réseau ayant comme IP : 10.1.0.1 et 10.2.0.1 sans serveur DHCP.

2. Création des VMs
On clone 3 VMs depuis la VM patron.

- [x] Désactiver SELinux (fait sur le patron)
- [x] Installation de certains paquets dans le patron (fait sur le patron)
- [x] Désactivation de la carte NAT (fait sur le patron)
- [x] Définition des IPs statiques
    * client1 ```   GNU nano 2.3.1                         File: ifcfg-enp0s8                                                          
NAME=enp0s8
DEVICE=enp0s8

BOOTPROTO=static
ONBOOT=yes

IPADDR=10.1.0.10
NETMASK=255.255.255.0
ZONE=public```
    * server1 ``` ```
    * router1 ``` ```
- [x] 