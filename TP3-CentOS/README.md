# Tp3_réseau_ CentOS

## I. Création et utilisation simples d'une VM CentOS

4. Configuration réseau d'une machine CentOS

    * a. Connexion exterieur:
        ```
            [admin@localhost ~]$ curl google.com
            <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
            <TITLE>301 Moved</TITLE></HEAD><BODY>
            <H1>301 Moved</H1>
            The document has moved
            <A HREF="http://www.google.com/">here</A>.
            </BODY></HTML>
        ```

    * b. Ping VM---->Hote:
        ```
            [admin@localhost ~]$ ping 192.168.102.1
            PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
            64 bytes from 192.168.102.1: icmp_seq=1 ttl=128 time=0.416 ms
            64 bytes from 192.168.102.1: icmp_seq=2 ttl=128 time=0.574 ms
            64 bytes from 192.168.102.1: icmp_seq=3 ttl=128 time=0.590 ms
            64 bytes from 192.168.102.1: icmp_seq=4 ttl=128 time=0.598 ms
            64 bytes from 192.168.102.1: icmp_seq=5 ttl=128 time=0.575 ms
            ^C
            --- 192.168.102.1 ping statistics ---
            5 packets transmitted, 5 received, 0% packet loss, time 4003ms
            rtt min/avg/max/mdev = 0.416/0.550/0.598/0.072 ms
        ```
        Ping Hote---->Hote:
        ```
            C:\Users\pierr>ping 192.168.102.1  
            Envoi d’une requête 'Ping'  192.168.102.1 avec 32 octets de données :
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128

            Statistiques Ping pour 192.168.102.1:
                Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
            Durée approximative des boucles en millisecondes :
                Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
        ``` 
        Le PC et la VM peuvent ce ping entre elles donc elles peuvent communiquer

    * c. Table de routage:
        ```
            [admin@localhost ~]$ ip route
            default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
            10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
            192.168.102.0/24 dev enp0s8 proto kernel scope link src 192.168.102.10 metric 101      
        ```
        La premiere et deuxieme ligne correspond au adresses public 
        et la troisieme ligne correspond à Ip privé permettant la communication avec le PC

5. Faire joujou avec quelques commande
    * ping
        Ping VM---->Hote:
        ```
            [admin@localhost ~]$ ping 192.168.102.1
            PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
            64 bytes from 192.168.102.1: icmp_seq=1 ttl=128 time=0.416 ms
            64 bytes from 192.168.102.1: icmp_seq=2 ttl=128 time=0.574 ms
            64 bytes from 192.168.102.1: icmp_seq=3 ttl=128 time=0.590 ms
            64 bytes from 192.168.102.1: icmp_seq=4 ttl=128 time=0.598 ms
            64 bytes from 192.168.102.1: icmp_seq=5 ttl=128 time=0.575 ms
            ^C
            --- 192.168.102.1 ping statistics ---
            5 packets transmitted, 5 received, 0% packet loss, time 4003ms
            rtt min/avg/max/mdev = 0.416/0.550/0.598/0.072 ms
        ```
        Ping Hote---->Hote:
        ```
            C:\Users\pierr>ping 192.168.102.1  
            Envoi d’une requête 'Ping'  192.168.102.1 avec 32 octets de données :
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128
            Réponse de 192.168.102.1 : octets=32 temps<1ms TTL=128

            Statistiques Ping pour 192.168.102.1:
                Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
            Durée approximative des boucles en millisecondes :
                Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
        ```
    * Table de routage
        VM
        ```
            [admin@localhost ~]$ ip route
            default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
            10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
            192.168.102.0/24 dev enp0s8 proto kernel scope link src 192.168.102.10 metric 101
        ```
        Hote
        ```
            C:\Users\pierr>route print

            192.168.102.0    255.255.255.0         On-link     192.168.102.1    281
            192.168.102.1  255.255.255.255         On-link     192.168.102.1    281
        ```
    * On telecharge un fichier avec la commande wget
        ```
            [admin@localhost ~]# wget google.com
            --2019-01-08 16:42:20--  http://google.com/
            Résolution de google.com (google.com)... 216.58.208.238, 2a00:1450:4007:810::200e
            Connexion vers google.com (google.com)|216.58.208.238|:80...connecté.
            requête HTTP transmise, en attente de la réponse...301 Moved Permanently
            Emplacement: http://www.google.com/ [suivant]
            --2019-01-08 16:42:20--  http://www.google.com/
            Résolution de www.google.com (www.google.com)... 172.217.22.132, 2a00:1450:4007:810::2004
            Connexion vers www.google.com (www.google.com)|172.217.22.132|:80...connecté.
            requête HTTP transmise, en attente de la réponse...200 OK
            Longueur: non spécifié [text/html]
            Sauvegarde en : «index.html»

                [ <=>                                   ] 11 356      --.-K/s   ds 0,001s

            2019-01-08 16:42:20 (17,4 MB/s) - «index.html» sauvegardé [11356]
        ```
    * Adresse :

        Ynov.com : 217.70.184.38
        
        google.com :  216.58.205.14
    

## II. Notion de ports et SSH

1. Exploration des ports locaux

```
    [admin@localhost ~]$ ss -4tln
    State      Recv-Q Send-Q               Local Address:Port                              Peer Address:Port
    LISTEN     0      128                              *:22                                           *:*
    LISTEN     0      100                      127.0.0.1:25                                           *:*
```

2. SSH
    * Connexion au serveur SSH:
    ```
        C:\Users\pierr>ssh admin@192.168.127.10
    ```

3. Firewall

    * A.SSH:

        Changement du port:
        ```
            [admin@localhost ~]$ sudo nano /etc/ssh/sshd_config
        ```
        On change la ligne : "#Port 22" en "Port 2222"

        Vérification :
        ```
            [admin@localhost ~]$ ss -4tln
            State       Recv-Q Send-Q             Local Address:Port                            Peer Address:Port
            LISTEN      0      128                            *:2222                                       *:*
            LISTEN      0      100                    127.0.0.1:25                                         *:*
        ```

        Nouvelle connexion au serveur SSH:

        La commande ssh utilise par défault le port 22 pour se connecter. Il faut donc préciser le nouveau port attribué avec l'option "-p".
        ```
            C:\Users\pierr>ssh admin@192.168.127.10 -p 2222
        ```

    * B. netcat:

        Serveur:
        ```
            [admin@localhost ~]$ nc -l 5454
            d
            d
            reussi
            youpi
        ```

        Client:
        ```
            C:\Users\pierr\Desktop\netcat-1.11>nc 192.168.102.10 5454
            d
            d
            reussi
            youpi
        ```

# III. Routage statique

L'objectif de cette partie est de transformer nos PC en routeurs et de permettre au deuxième PC de se connecter à la machine du premier, et inversement.


```
Internet            Internet
    |                    |
  WiFi                  WiFi
    |                    |
   PC 1  ---Ethernet--- PC 2
    |                    |
Host-only 1          Host-only 2
    |                    |
   VM 1                 VM 2
```


# 1. Préparation des hôtes
Ok, alors la le principe c'est de modifier l'adresse de la carte HOST ONLY et l'adresse de la carte ETHERNET.
Nos cartes Ethernet sont dans le réseau : 192.168.112.0/30

PC1 : réseau 1 : 192.168.101.0/24


VM1 (sur PC1) : 192.168.101.10


PC2 : réseau 2 : 192.168.102.0/24


VM2 (sur PC2) : 192.168.102.10


# Check 

On check PC1 vers VM1 :


```
C:\Users\Ju'>ping 192.168.101.10

Envoi d’une requête 'Ping'  192.168.101.10 avec 32 octets de données :
Réponse de 192.168.101.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.101.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.101.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.101.10 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 192.168.101.10:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```


VM1 vers PC1 : 


```
[root@localhost ~]# ping 192.168.101.1
PING 192.168.101.1 (192.168.101.1) 56(84) bytes of data.
64 bytes from 192.168.101.1: icmp_seq=1 ttl=64 time=0.224 ms
64 bytes from 192.168.101.1: icmp_seq=2 ttl=64 time=0.274 ms
64 bytes from 192.168.101.1: icmp_seq=3 ttl=64 time=0.291 ms
64 bytes from 192.168.101.1: icmp_seq=4 ttl=64 time=0.293 ms
64 bytes from 192.168.101.1: icmp_seq=5 ttl=64 time=0.290 ms
^C
--- 192.168.101.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4013ms
rtt min/avg/max/mdev = 0.224/0.274/0.293/0.030 ms
```

PC2 vers VM2 :

```
C:\Users\pierr>ping 192.168.102.10

Envoi d’une requête 'Ping'  192.168.102.10 avec 32 octets de données :
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 192.168.102.10:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

VM2 vers PC2 :

```
[admin@localhost ~]$ ping 192.168.102.1
PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
64 bytes from 192.168.102.1: icmp_seq=1 ttl=128 time=0.306 ms
64 bytes from 192.168.102.1: icmp_seq=2 ttl=128 time=0.579 ms
64 bytes from 192.168.102.1: icmp_seq=3 ttl=128 time=0.278 ms
64 bytes from 192.168.102.1: icmp_seq=4 ttl=128 time=0.562 ms
^C
--- 192.168.102.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3001ms
rtt min/avg/max/mdev = 0.278/0.431/0.579/0.140 ms
```


PC1 vers PC2 :


```
C:\Users\Ju'>ping 192.168.112.2

Envoi d’une requête 'Ping'  192.168.112.2 avec 32 octets de données :
Réponse de 192.168.112.2 : octets=32 temps=2 ms TTL=128
Réponse de 192.168.112.2 : octets=32 temps=1 ms TTL=128
Réponse de 192.168.112.2 : octets=32 temps=1 ms TTL=128
Réponse de 192.168.112.2 : octets=32 temps=1 ms TTL=128

Statistiques Ping pour 192.168.112.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 2ms, Moyenne = 1ms

C:\Users\Ju'>
```


PC2 vers PC1 :


```
C:\Users\pierr>ping 192.168.112.1

Envoi d’une requête 'Ping'  192.168.112.1 avec 32 octets de données :
Réponse de 192.168.112.1 : octets=32 temps=1 ms TTL=64
Réponse de 192.168.112.1 : octets=32 temps=2 ms TTL=64
Réponse de 192.168.112.1 : octets=32 temps=2 ms TTL=64
Réponse de 192.168.112.1 : octets=32 temps=1 ms TTL=64

Statistiques Ping pour 192.168.112.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 2ms, Moyenne = 1ms

```


# Activation du routage sur les PCs

Vu que nous sommes sur Windows, il a fallut modifier la clé registre `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\ Services\Tcpip\Parameters\IPEnableRouter` en passant sa valeur de **0** à **1**

Ensuite, on a démarré le service après un reboot.

# 2. Configuration du routage

Bilan des adresses IP :

* PC1 :
    * Carte Ethernet : 192.168.112.1
    * Carte Host Only : 192.168.101.1
* VM1 :
    * Carte Host Only : 192.168.101.10
* PC2 :
    * Carte Ethernet : 192.168.112.2
    * Carte Host Only : 192.168.102.1
* VM2 :
    * Carte Host Only : 192.168.102.10


# Sur le PC1 :

On doit dire au PC1 comment accéder au réseau 2 :

`route add 192.168.102.0/24 mask 255.255.255.0 192.168.112.2`

Signifiant : " On ajoute une route pour aller sur l'adresse 192.168.102.0 en passant par le chemin 192.168.112.2 "

# Sur le PC2 :

On fait la chose inverse


# Sur la VM1

Pour lui dire d'accéder au réseau 12 en passant par 1:

`ip route add 192.168.112.0/24 via 192.168.101.1 dev enp0s8`

Pour lui dire d'accéder au réseau 2 :

`ip route add 192.168.102.0/24 via 192.168.101.1 dev enp0s8`

VM1 Ping l'adresse de PC2 dans le réseau 12 :

```
[root@localhost ~]# ping 192.168.112.1
PING 192.168.112.1 (192.168.112.1) 56(84) bytes of data.
64 bytes from 192.168.112.1: icmp_seq=1 ttl=63 time=0.781 ms
64 bytes from 192.168.112.1: icmp_seq=2 ttl=63 time=0.336 ms
64 bytes from 192.168.112.1: icmp_seq=3 ttl=63 time=0.278 ms
64 bytes from 192.168.112.1: icmp_seq=4 ttl=63 time=0.278 ms
64 bytes from 192.168.112.1: icmp_seq=5 ttl=63 time=0.271 ms
^C
--- 192.168.112.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 0.271/0.388/0.781/0.199 ms
```

VM1 Ping l'adresse de PC2 dans le réseau 2 :

```
[root@localhost ~]# ping 192.168.102.1
PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
64 bytes from 192.168.102.1: icmp_seq=1 ttl=126 time=2.12 ms
64 bytes from 192.168.102.1: icmp_seq=2 ttl=126 time=1.99 ms
64 bytes from 192.168.102.1: icmp_seq=3 ttl=126 time=1.99 ms
64 bytes from 192.168.102.1: icmp_seq=4 ttl=126 time=1.82 ms
64 bytes from 192.168.102.1: icmp_seq=5 ttl=126 time=1.83 ms
^C
--- 192.168.102.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4226ms
rtt min/avg/max/mdev = 1.829/1.955/2.126/0.112 ms
```

# Sur la VM2

Pareil que la VM1

# 3. Configuration des noms de domaine :

VM1 qui ping PC2 et VM2 :
```
[root@localhost etc]# ping pc2.tp3.b1
PING pc2 (192.168.112.2) 56(84) bytes of data.
64 bytes from pc2 (192.168.112.2): icmp_seq=1 ttl=127 time=1.81 ms
64 bytes from pc2 (192.168.112.2): icmp_seq=2 ttl=127 time=1.60 ms
64 bytes from pc2 (192.168.112.2): icmp_seq=3 ttl=127 time=1.49 ms
64 bytes from pc2 (192.168.112.2): icmp_seq=4 ttl=127 time=1.81 ms
^C
--- pc2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4009ms
rtt min/avg/max/mdev = 1.492/1.655/1.817/0.137 ms
[root@localhost etc]# ping vm2.tp3.b1
PING vm2 (192.168.102.10) 56(84) bytes of data.
64 bytes from vm2 (192.168.102.10): icmp_seq=1 ttl=62 time=2.59 ms
64 bytes from vm2 (192.168.102.10): icmp_seq=2 ttl=62 time=2.36 ms
64 bytes from vm2 (192.168.102.10): icmp_seq=3 ttl=62 time=2.25 ms
64 bytes from vm2 (192.168.102.10): icmp_seq=4 ttl=62 time=2.65 ms
^C
--- vm2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 2.253/2.468/2.658/0.164 ms
```

La configuration du fichier hosts sur PC1 :

```
#
127.0.0.1 localhost pc1 pc1.tp3.b1
::1 localhost
192.168.112.2 pc2 pc2.tp3.b1
192.168.102.10 vm2 vm2.tp3.b1
```

Le but ultime de netcat entre VM1 et VM2 :

```
[root@localhost etc]# nc -l 5454
Bonjour, voii^Hci^H^H^H^H^H^H^[[3~^[[3~^H^H^H^H^H^H^H
^H^H^H^H^H^H^H^Hslt
Voici slt
le test du netcat termin2
````

(Sachant que la VM2 a utilisé `nc vm1 5454`)

La VM1 peut désormais ping tous les FQDN (y compris vm1.tp3.b1)

De même pour la VM2 (pouvant ping vm2.tp3.b1)