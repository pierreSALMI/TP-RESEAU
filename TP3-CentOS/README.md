# Tp3_réseau_ CentOS

## I. Création et utilisation simples d'une VM CentOS

4. Configuration réseau d'une machine CentOS

    Connexion exterieur:

    ```
    [admin@localhost ~]$ curl google.com
    <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
    <TITLE>301 Moved</TITLE></HEAD><BODY>
    <H1>301 Moved</H1>
    The document has moved
    <A HREF="http://www.google.com/">here</A>.
    </BODY></HTML>
    ```

## II. Notion de ports et SSH

1. Exploration des ports locaux

```
[admin@localhost ~]$ ss -4tln
```

2. SSH
```
C:\Users\pierr>ssh admin@192.168.127.10
```

3. Firewall
Connexion:
La commande ssh utilise par défault le port 22 pour se connecter. 
Pour se connecter à notre serveur il faut donc préciser le nouveau port attribué
```
C:\Users\pierr>ssh admin@192.168.127.10 2222
```

netcat
nc -l 5454
nc 192.167.127.10 5454


