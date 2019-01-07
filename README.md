# Tp_réseau

## I. Exploration locale

1. Affichage d'informations sur la pile TCP/IP locale
Ligne de commande: `ipconfig /all`

Interface Wifi:
Nom : Intel(R) Dual Band Wireless-AC 7265
Adresse IP: 10.33.3.200
Adresse MAC: 88-78-73-51-96-04
Adresse réseau : 10.33.0.0
Adresse de broadcast : 10.33.3.255

Interface Ethernet:
Nom : Realtek PCIe GBE Family Controller
Adresse IP : None
Adresse MAC : 88-D7-F6-34-24-99

Commande pour trouver la passerelle: `ipconfig | findstr /i "passerelle"`
Passerelle : 10.33.3.253


(Image Info_carte)

La gateway relie notre ordinateur à d'autre réseau comme "Internet"

2. Modifications des informations

Premiere IP : 10.33.0.1
Derniere IP : 10.33.3.254

(image changement_adresse)

## II. Exploration locale en duo

  

Après avoir brancé le câble Ethernet aux PCs on peut commencer.

*  **Création du réseau**

  
On définit une adresse IP sur nos cartes réseau afin que notre réseau existe.

Sur notre carte Ethernet nous avons modifié comme suis :

*  **Réseau local** :

* Adresse IP PC1 : 172.16.1.1

* Adresse IP PC2 : 172.16.1.2

* Masque de réseau : 255.255.255.252

  
  

On vérifie grâce à cette commande que nos changements ont pris effet :

  
  

`ipconfig /all`

  
  

![Image du réseau local](/images/duo_changeip.PNG)

  
  

Après s'être assuré que nos deux ordinateurs ont leur adresse IP bien configurée, on fait un ping sur un PC :

  
  

`ping 172.16.1.1`

  

![Ping local](/images/pinglocal.PNG)

  
  

Le ping marche, c'est que nous sommes connectés.

*  **Utilisation d'un des deux comme gateway**

On désactive l'interface WiFi sur l'un des deux postes,
les PCs sont bel et bien connectés par ethernet.
* Sur le PC qui n'a plus internet on a défini comme passerelle l'adresse IP de l'autre PC :
![Passerelle](/images/duo_connected.PNG)

* Sur le PC qui a toujours internet on a mis le partage de connexion sur la carte wifi connecté à la connexion Ethernet.

Pour tester la connectivité on s'est pingé, avec une réponse des deux côtés.

Malgré ça, la connexion à internet demeure impossible sur un navigateur. (Vive Windaube) 

Du coup, on a modifié le DNS sur le PC n'ayant pas internet par 
* DNS Primaire : 8.8.8.8
* DNS Secondaire : 8.8.4.4

Une fois ceci fait, la connexion à Google est possible.
Le partage de connexion fonctionne désormais.

*  **Petit chat privé ?** :
Une fois netcat installé sur Windows, on a tapé les commandes suivantes pour communiquer :

	* Sur le PC serveur : `nc.exe -l -p 80`
	* Sur le PC client : `nc.exe 192.168.137.1 80`
	
Une fois ceci fait nous pouvons parler sur le CMD ! Youhouu
![Connected](/images/duo_netcat.PNG)

*  **Wireshark** :
	* Les trames circulant pendant un ping :
![Trames](/images/duo_wping.PNG)

	* Les trames circulant pendant un netcat :
![Trames](/images/duo_wnetcat.PNG)

	* Les trames circulant pendant que le PC2 se connecte à internet par la gateway du PC1 :
![Trames](/images/duo_wgateway.PNG)

*  **Firewall** :
	* Pour activer le ping sur le firewall de Windows on tape cette commande la sur le CMD :
`netsh advfirewall firewall add rule name="ICMP Allow incoming V4 echo request" protocol=icmpv4:8,any dir=in action=allow`

	* Pour activer le netcat on est allé sur le pare-feu Windows afin d'activer le port 8888 en port local.
On autorise tous les ports en port distant car on ne connais pas le port de connexion du pc distant.

Le netcat sous Firewall marche !

# III. Manipulations d'autres outils/protocoles côté client

*  **DHCP** : 
	* Adresse DHCP :10.33.3.254
	* Bail expirant : jeudi 20 décembre 2018 13:03:20
	* Commande pour demander une autre adresse : `ipconfig /renew`

* **DNS** :
	* Serveurs DNS : 10.33.10.20
	
	
