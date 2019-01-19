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
