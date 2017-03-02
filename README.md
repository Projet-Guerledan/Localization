






###################### Installations #####################


# connection raspberry filaire

brancher un cable éthernet entre la raspberry et l'ordi et faire un partage de connection éthernet avec l'ordinateur
une fois que les deux systèmes sont connectés, taper dans un terminal:
h0stname -I

L'adresse IP de l'ordinateur apparait, par exemple 10.42.0.1
et ensuite à partir de cette adresse, remplacer le dernier chiffre de l'adresse comme suit et taper:

nmap -sn 10.42.0.0/24

l'adresse de la raspberry apparait, par exemple 10.42.0.75, puis tapper

ssh pi@10.42.0.75

le mot de passe de la raspberry sera demandée, pour ma part mdp = "raspberry"

pour sortir de la connection: tapper "exit"

pour que les interfaces graphiques puissent fonctionner, tapper : xhost +10.42.0.75
ensuite utiliser: ssh -X pi@10.42.0.75


pour autoriser le ssh ou le vnc, il faut tapper  "sudo raspi-config" dans un terminal de la raspberry
et choisir ssh enable ou vnc enable  dans "interfacing option"
il faut ensuite telecharger vnc viewer pour visualiser sur l'ordiannateur la raspberry:
https://www.realvnc.com/download/viewer/


# connection raspberry wifi


configurer l'antenne wifi après l'avoir reset (appuyer longtemps sur le bouton reset)
L'IP par defaut est alors retrouvée dans la documentation (dans notre cas c'etait 192.168.1.20)
Il faut alors configurer une connection filaire au routeur avec ip fixe
parametre ipv4 manuel, dans notre cas on a choisi : 
adresse : 192.168.1.25 ; masque 255.255.255.0 ; passerelle 192.168.1.20

On se connecte alors à la configuration du routeur dans un moteur de recherche en tappant l'adresse ip 192.168.1.20
On configure en router et en access point (WPS)
On peut alors se connecter au wifi du routeur en ip fixe configurer de la meme maniere que le filaire mais pour la wifi.

On peut alors mettre en place la connection filaire similaire pour la raspberry,
dans notre cas en mode graphique grace à vnc:
adresse : 192.168.1.21 ; masque 255.255.255.0 ; passerelle 192.168.1.20
Une fois la connection mise en place on peut brancher le routeur à la raspberry,
et la raspberry se connecte automatiquement à la connection par ip fixe mise en place

Sur notre ordinateur, on se connecte en wifi au routeur,
on peut alors tapper "nmap -sn 192.168.1.0/24"
On obtient les adresses ip du routeur, de l'ordinateur, et de la raspberry,
On peut alors se connecter à la raspberry en tappant "ssh pi@192.168.1.21"

# GPS

pour connecter un gps usb, il faut installer les packet:
gpsd et gpsd-client
puis on peut voir le gps fonctionner en tappant dans un terminal xgps

Lorsque le gps fonctionne il clignotte, si sa diode reste alumée sans clignoter c'est qu'il ne capte pas les satellites

Si python est installé on peut alors utiliser un code python pour lire les données gps


# Divers

connaitre le pid des processus: ps -e
arreter le processus: kill -SIGTERM <pid>

copier des fichier de la rasp au pc (depuis un terminal du pc (pas en ssh)) avec login@adresseip = pi@10.42.0.75
scp login@adresseip:Chemin/Fichier .

installer librairie python gpio :   sudo apt-get install python-dev python-rpi.gpio




