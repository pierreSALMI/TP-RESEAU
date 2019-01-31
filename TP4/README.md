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
- [x] Connexion SSH
    * client1 ```ssh user@10.1.0.10 ```
    * server1 ```ssh user@10.2.0.10 ```
    * router1 ```ssh user@10.1.0.254 ```

- [x] Définition du nom de domaine
    * ``  [user@client1 ~]$ hostname --fqdn client1 ``
    
