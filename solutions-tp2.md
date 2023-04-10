Cours : Utilisation et administration des systèmes informatiques
Sigle : INF1070
Session : Hiver 2023
Groupe : 11

Enseignant : <Johnny Tsheke Shele>

Auteur : <Bouargan Zakariae> (<BOUZ90340206>)

Solution de la mission M01

État de la mission : résolue

Démarche
J'ai utilisé la commande "sudo apt-get update" pour mettre à jour mes paquets
Ensuite j'ai utilisé la commande "sudo apt-get install docker-compose docker curl" pour installer docker-compose, docker et curl. 
J'ai téléchargé le fichier tp2.tar.gz et puis je l'est extrayé avec la commande "tar xzf tp2.tar.gz", ensuite j'ai accedé au fichier tp2 avec la commande "cd tp2"
J'ai tapez la commande suivante: "sudo chown -R 33:33 data/nextcloud" ensuite "docker-compose up -d"
J'ai utilisé la command "sudo nano /etc/hosts"  pour editer le fichier text hosts, j'ai choisi le editeur de texte nano car il est facile à manipuler, et j'ai ajouté la ligne suivante "127.0.0.1 nextcloud.localhost"

Ensuite, en entrant
./checkM01.sh
Le resultat était "Tout fonctionne correctement." 

la mission a été validée, ce qui a conclu cette mission.


Solution de la mission M02

État de la mission : résolue
M02.1)
Démarche
Il y a trois containers Docker présents.
J'ai utilisé la commande "sudo docker ps -a" pour afficher tous les containers qui sont present grace à l'option -a 

Il y a deux containers Docker en train de trouner.
J'ai utilisé la commande "sudo docker ps" pour afficher les containers qui sont entrain de tourner

M02.2)
Démarche
D'après Wikipedia une addresse IPV4 elle se compose de 4 nombres délimites par 3 points et ses nombres varient de 0 jusqu'à 256. Donc le regex que j'ai utilisé est le suivant : "(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)(\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}"

(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?) : cette partie matche les trois premiers octets de l'adresse IPv4. Cette partie de la regex permet de matcher les nombres entre 0 et 255.

"25[0-5]" : matche les nombres entre 250 et 255
"2[0-4][0-9]" : matche les nombres entre 200 et 249
"[01]?[0-9][0-9]?" : matche les nombres entre 0 et 199. Cette partie de la regex est un peu plus complexe. Les [01]? matchent soit 0 soit 1, mais pas nécessairement. Cela permet de matcher les nombres de 0 à 199. Les [0-9] matchent ensuite n'importe quel chiffre entre 0 et 9. Les ? permettent de matcher le dernier chiffre optionnel. Cela permet de matcher les nombres de 0 à 99.
"(\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}" : cette partie matche les trois derniers octets de l'adresse IPv4, séparés par des points.

Le resultat est:
		"Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                "IPv4Address": "172.19.0.2/16",


Solution de la mission M03

État de la mission : résolue
M03.1)
Démarche
Pour obtenir les en-têtes HTTP de la réponse du serveur web, on peut utiliser la commande curl avec l'option -I pour n'obtenir que les en-têtes. En exécutant la commande suivante : "curl -I -k https://localhost"
Le résultat est:
"alt-svc: h3=":443"; ma=2592000
content-type: text/plain; charset=utf-8
server: Caddy
content-length: 13
date: Mon, 10 Apr 2023 08:00:58 GMT"

Le server est Caddy

M03.2)
Démarche
Pour se connecter en SSH sur la machine du serveur web, nous pouvons utiliser la commande suivante : "ssh root@localhost -p 2222"
Cela va nous connecter en tant qu'utilisateur root sur la machine du serveur web qui est accessible sur le port 2222 de localhost. Nous devrons saisir le mot de passe "root" lorsque nous y serons invités.

M03.3)
Démarche
Pour trouver les processus actifs sur le serveur web, nous pouvons utiliser la commande suivante : "ps aux"
Cela va nous afficher la liste de tous les processus actifs sur le système, y compris ceux du serveur web.
Les processus actifs sont les suivants :
	sshd avec PID 1
	caddy avec PID 8
	sshd pour la session SSH avec PID 25
	un shell interactif avec PID 27
	la commande ps avec PID 28
	
M03.4)
Démarche
J'ai installé apache2 avec la commande suivante "apk add apache2", ensuite le chemin où se trouve le fichier de configuration du serveur web est : "/etc/apache2/httpd.conf"

Solution de la mission M04

État de la mission : résolue
M04.1)
Démarche
La commande pour inspecter le réseau tp2_default et trouver l'adresse IPv4 du serveur de base de données MariaDB est la suivante: "docker network inspect tp2_default | grep -E "(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)(\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}""

En inspectant le résultat, on peut trouver l'adresse IPv4 du serveur MariaDB sous la section "Containers". L'adresse IPv4 est 172.19.0.2.

Pour vérifier que cette adresse est accessible, on peut utiliser la commande ping suivante : "ping 172.19.0.2 -c 4
"

Le resultat est le suivant: 
PING 172.19.0.2 (172.19.0.2) 56(84) bytes of data.
64 bytes from 172.19.0.2: icmp_seq=1 ttl=64 time=0.172 ms
64 bytes from 172.19.0.2: icmp_seq=2 ttl=64 time=0.104 ms
64 bytes from 172.19.0.2: icmp_seq=3 ttl=64 time=0.097 ms
64 bytes from 172.19.0.2: icmp_seq=4 ttl=64 time=0.097 ms

--- 172.19.0.2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3058ms
rtt min/avg/max/mdev = 0.097/0.117/0.172/0.031 ms


M04.2)
Démarche
Pour installer le client MariaDB, on peut utiliser la commande suivante : 
"sudo apt-get update"
"sudo apt-get install mariadb-client"

M04.3)
Démarche




















