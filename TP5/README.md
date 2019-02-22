# TP 5 - Premier pas dans le monde Cisco

## I Préparation du lab

![Image topologie](./images/topologie.PNG)

## II Lancement et configuration du lab

### Checklist IP VMs

#### Client 1

- [x] Désactiver SELinux (fait sur le patron)
- [x] Installation de certains paquets dans le patron (fait sur le patron)
- [x] Désactivation de la carte NAT (fait sur le patron)
- [x] Définition des IPs statiques
- [x] Connexion SSH
    * `ssh user@192.168.143.4`
- [x] Définition du nom de domaine
    * `[user@client1 ~]$ hostname --fqdn client1.tp5`
- [x] Remplissage du fichier /etc/hosts
    ```
    127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
    ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

    10.5.1.10 server1 server1.tp5
    10.5.2.11 client2 client2.tp5
    ```
