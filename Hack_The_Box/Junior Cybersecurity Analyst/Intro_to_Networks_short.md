# 🌐 Hack The Box - Network Foundations Notes

Documentation complète et détaillée du module **Network Foundations** de Hack The Box Academy.

---

## 1. Networking Fundamentals

### 1.1 Introduction to Networks
* **Network** : Collection d'équipements interconnectés capables de communiquer en envoyant et recevant des données.
* **Transmission Types** :
  * **Analog** : Signaux continus représentant l'information (ex. radio traditionnelle).
  * **Digital** : Signaux discrets (bits) pour coder l'information.
* **Transmission Modes** :
  * **Simplex** : Communication unidirectionnelle uniquement (ex. du clavier vers l'ordinateur).
  * **Half-Duplex** : Communication bidirectionnelle non simultanée (ex. walkie-talkie).
  * **Full-Duplex** : Communication bidirectionnelle simultanée.
* **Transmission Media** :
  * **Paire torsadée** (*Twisted Pair*) : Câbles Ethernet.
  * **Coaxial** : Câbles utilisés pour la TV et l'Ethernet ancien.
  * **Fibre optique** (*Fiber Optic*) : Signal lumineux à très haut débit.
  * **Ondes radio** : Wi-Fi et réseaux cellulaires.
  * **Micro-ondes** : Communications satellites.
  * **Infrarouge** : Communications courte portée (télécommandes).

---

### 1.2 Network Concepts

#### OSI Model (Open Systems Interconnection)
Modèle conceptuel normalisé en 7 couches abstrayant les fonctions d'un système de télécommunication :

1. **Physical Layer (Layer 1)** : Transmet les flux de bits bruts sur le support physique (câbles Ethernet, hubs, répéteurs).
2. **Data Link Layer (Layer 2)** : Assure le transfert de données nœud à nœud, la synchronisation et la détection d'erreurs. Utilise les adresses **MAC** (Switches, bridges).
3. **Network Layer (Layer 3)** : Gère le routage et le transfert des paquets à travers différents réseaux. Utilise les adresses **IP** (Routeurs).
4. **Transport Layer (Layer 4)** : Assure les services de communication de bout en bout (fiable ou non), la segmentation, le réassemblage, le contrôle de flux et d'erreurs (**TCP**, **UDP**).
5. **Session Layer (Layer 5)** : Établit, maintient et termine les sessions et connexions entre applications.
6. **Presentation Layer (Layer 6)** : Traduit les données pour la couche application (chiffrement/déchiffrement, compression, conversion de formats).
7. **Application Layer (Layer 7)** : Fournit des services réseau directement aux applications utilisateur (HTTP, FTP, SMTP, DNS).

#### TCP/IP Model
Version condensée et pratique du modèle OSI pour Internet en 4 couches :

| Couche TCP/IP | Équivalent OSI | Description & Protocoles |
| :--- | :--- | :--- |
| **Application** | Session (5), Presentation (6), Application (7) | Services de communication spécifiques aux applications (**HTTP**, **FTP**, **SMTP**). |
| **Transport** | Transport (4) | Communication de bout en bout (**TCP** pour la fiabilité, **UDP** pour la rapidité). |
| **Internet** | Network (3) | Adressage logique et routage des paquets (**IP**, **ICMP**). |
| **Link** | Physical (1), Data Link (2) | Gestion des aspects physiques et adresses MAC (**Ethernet**, **Wi-Fi**). |

#### Protocoles Principaux

| Protocole | Couche | Description |
| :--- | :--- | :--- |
| **HTTP** | Application | Transfert de pages et contenus web entre navigateurs et serveurs. |
| **FTP** | Application | Transfert de fichiers (upload/download) entre systèmes. |
| **SMTP** | Application | Transmission de courriers électroniques entre serveurs. |
| **TCP** | Transport | Connexion fiable avec contrôle d'erreur et garantie d'ordre d'arrivée. |
| **UDP** | Transport | Communication rapide sans connexion ni contrôle d'erreur (ex. streaming). |
| **IP** | Internet | Adressage et routage des paquets à travers les réseaux. |

---

### 1.3 Components of a Network
* **NIC (Network Interface Card)** : Composant matériel permettant à un équipement de se connecter au réseau.
* **Adresse MAC (Media Access Control)** : Identifiant unique de 48 bits (format hexadécimal `00:1A:2B:3C:4D:5E`) opérant en couche 2.
  * **24 premiers bits** : OUI (*Organizationally Unique Identifier*) attribué au fabricant.
  * **24 derniers bits** : Identifiant propre à l'équipement.
  * **Commande Windows** : `getmac`

---

## 2. Network Communication and Addressing

### 2.1 Network Communication
La communication réseau repose sur trois composants cruciaux :
1. **Adresses MAC** (Couche 2) : Identification sur le réseau local (LAN).
2. **Adresses IP** (Couche 3) : Localisation et routage entre réseaux distincts.
   * **IPv4** : 32 bits (ex. `192.168.1.1`).
   * **IPv6** : 128 bits.
3. **Ports** (Couche 4) : Numéros associés aux processus/services pour orienter le trafic TCP/UDP.

---

### 2.2 Dynamic Host Configuration Protocol (DHCP)
Protocole automatisant la configuration IP des équipements (IP, masque, passerelle, DNS).

#### Le Processus DORA

| Étape | Action | Description |
| :---: | :--- | :--- |
| **1** | **Discover** | Le client émet un message broadcast pour trouver un serveur DHCP disponible. |
| **2** | **Offer** | Le serveur DHCP répond avec une proposition de bail IP. |
| **3** | **Request** | Le client répond pour accepter l'adresse IP proposée. |
| **4** | **Acknowledge (ACK)** | Le serveur confirme l'attribution de l'IP au client. |

* **DHCP Server** : Équipement gérant le pool d'adresses IP.
* **DHCP Client** : Équipement effectuant la demande de configuration.

---

### 2.3 Network Address Translation (NAT)
Le NAT permet à plusieurs équipements d'un réseau privé de partager une seule adresse IP publique (pénurie d'adresses IPv4).

#### Plages d'adresses privées (RFC 1918)
* `10.0.0.0` à `10.255.255.255`
* `172.16.0.0` à `172.31.255.255`
* `192.168.0.0` à `192.168.255.255`

#### Fonctionnement du NAT
Dans un réseau domestique :
* Interface **LAN** du routeur : IP privée (`192.168.1.1`).
* Interface **WAN** du routeur : IP publique attribuée par l'FAI (`203.0.113.50`).

#### Types de NAT
* **Static NAT** : Mappage 1:1 permanent entre une IP privée et une IP publique.
* **Dynamic NAT** : Attribution d'une IP publique à partir d'un pool d'adresses disponibles.
* **PAT (Port Address Translation / NAT Overload)** : Utilisation d'une seule IP publique en différenciant les équipements par des numéros de ports uniques.

#### Avantages & Inconvénients du NAT
* **Avantages** : Économise l'espace d'adressage IPv4, masque la structure interne du réseau.
* **Inconvénients** : Complexifie l'hébergement de serveurs publics (nécessite du *port forwarding*), peut altérer certains protocoles de bout en bout, complexifie le dépannage.

---

## 3. Internet Architecture and Wireless Technologies

### 3.1 Domain Name System (DNS)
Le DNS est l'annuaire d'Internet traduisant les noms de domaine lisibles (`www.example.com`) en adresses IP (`93.184.216.34`).

#### Hiérarchie DNS
* **Root Servers** : Sommet de la hiérarchie.
* **Top-Level Domains (TLDs)** : Extensions `.com`, `.org`, `.net`, ou codes pays (`.fr`, `.uk`).
* **Second-Level Domains** : Le nom principal (ex. `example` dans `example.com`).
* **Subdomains / Hostname** : Ex. `www` dans `www.example.com` ou `accounts` dans `accounts.google.com`.

#### Processus de résolution DNS (7 étapes)
1. L'utilisateur saisit `www.example.com` dans le navigateur.
2. L'ordinateur vérifie son **cache DNS local**.
3. Si non trouvé, il interroge un **serveur DNS récursif** (FAI, Google `8.8.8.8`).
4. Le serveur récursif interroge un **serveur racine** (*Root Server*) qui le redirige vers le TLD.
5. Le serveur TLD pointe vers le **serveur de noms autoritaire** de `example.com`.
6. Le serveur autoritaire renvoie l'IP correspondant à `www.example.com`.
7. Le serveur récursif retourne l'IP à l'ordinateur qui s'y connecte directement.

---

### 3.2 Internet Architecture

#### Modèles d'architecture
* **Peer-to-Peer (P2P)** : Chaque nœud est à la fois client et serveur.
  * *Avantages* : Scalabilité, résilience, distribution des coûts/ressources.
  * *Inconvénients* : Complexité de gestion, fiabilité variable des pairs, défis de sécurité.
* **Client-Serveur** :
  * **Single-Tier** : Client, serveur et base de données sur la même machine.
  * **Two-Tier** : Le client gère l'interface (présentation) et le serveur gère la base de données.
  * **Three-Tier** : Client (présentation) $\leftrightarrow$ Serveur d'application (logique métier) $\leftrightarrow$ Serveur de base de données.
  * *Avantages* : Contrôle centralisé, sécurité renforcée, performances optimisées.
  * *Inconvénients* : Point unique de défaillance (*Single Point of Failure*), coût/maintenance élevés, congestion réseau.
* **Hybrid Architecture** : Serveurs centraux pour l'authentification/coordination, transferts directs entre pairs (P2P).
* **Cloud Architecture** : Infrastructure managée par un tiers (AWS, Azure, GCP).
  * *5 caractéristiques* : Libre-service à la demande, accès réseau étendu, mutualisation des ressources, rapidité/élasticité, service mesuré.
  * *Avantages* : Scalabilité, réduction des coûts de matériel, flexibilité.
  * *Inconvénients* : Dépandance fournisseur (*Vendor lock-in*), enjeux de conformité/sécurité, dépendance Internet.
* **Software-Defined Architecture (SDN)** : Séparation du **Control Plane** (prise de décision du routage) et du **Data Plane** (acheminement du trafic).
  * *Avantages* : Contrôle centralisé, programmabilité/automatisation, efficacité.
  * *Inconvénients* : Vulnérabilité du contrôleur central, complexité d'implémentation.

---

### 3.3 Wireless Networks
Réseaux utilisant des ondes radio pour connecter des équipements sans câble.

* **Wireless Router** : Combine le routage, le point d'accès Wi-Fi (WAP) et le commutateur LAN.
* **Mobile Hotspot** : Partage de la connexion cellulaire via Wi-Fi.
* **Cell Tower** : Antenne gérant les cellules d'un réseau mobile.

#### Bandes de fréquences
1. **2.4 GHz** : Meilleure pénétration des murs, mais plus sujette aux interférences (micro-ondes, Bluetooth).
2. **5 GHz** : Débits plus rapides, mais portée plus courte et moins bonne pénétration des obstacles.
3. **Bandes cellulaires** : 4G LTE et 5G (700 MHz à 2.6 GHz et ondes millimétriques 28+ GHz).

---

## 4. Network Security and Data Flow Analysis

### 4.1 Network Security
Objectif : maintenir la triade **DIC** (**D**isponibilité, **I**ntégrité, **C**onfidentialité).

#### Firewalls (Pare-feux)
* **Packet Filtering Firewall** (Layers 3/4) : Filtre selon IP source/destination, ports et protocoles (ACL).
* **Stateful Inspection Firewall** (Layers 3/4) : Suit l'état des connexions établies.
* **Application Layer / Proxy Firewall** (Layer 7) : Inspecte le contenu applicatif (ex. en-têtes HTTP).
* **Next-Generation Firewall (NGFW)** : Allie l'inspection d'état, la détection d'intrusion (IPS) et l'inspection profonde des paquets (DPI).

#### IDS / IPS (Intrusion Detection & Prevention)
* **IDS** : Observe le trafic et génère des alertes sans bloquer.
* **IPS** : Inspecte et bloque le trafic malveillant en temps réel.
* **Techniques** :
  * **Signature-based** : Comparaison avec une base d'attaques connues.
  * **Anomaly-based** : Détection des déviations par rapport au comportement normal.
* **Types** :
  * **NIDS/NIPS** : Déployé sur le réseau pour inspecter tout le trafic.
  * **HIDS/HIPS** : Agent installé directement sur un hôte/serveur.

#### Bonnes Pratiques de Sécurité
1. **Politiques claires** : Appliquer le principe du moindre privilège.
2. **Mises à jour régulières** : Maintenir les règles et signatures à jour.
3. **Surveillance & Logs** : Analyser régulièrement les événements système.
4. **Sécurité en profondeur** (*Defense in Depth*) : Multiplier les couches de sécurité.
5. **Tests d'intrusion** : Réaliser des audits périodiques.

---

### 4.2 Data Flow Example (Requête Web)
Exemple pas à pas d'un ordinateur accédant à `www.example.com` :

1. **Accès réseau** : Connexion au Wi-Fi via SSID et authentification WPA2/WPA3.
2. **Configuration DHCP** : Obtention d'une IP privée (`192.168.1.10`), masque, passerelle (`192.168.1.1`) et serveur DNS (`8.8.8.8`).
3. **Résolution DNS** : Envoi de la requête DNS et réception de l'IP du serveur (`93.184.216.34`).
4. **Encapsulation de la donnée** :
   * *Layer 7* : Création de la requête `GET / HTTP/1.1`.
   * *Layer 4* : Ajout de l'en-tête TCP (Port Source dynamique $\rightarrow$ Port Dest `80`).
   * *Layer 3* : Ajout de l'en-tête IP (IP Source `192.168.1.10` $\rightarrow$ IP Dest `93.184.216.34`).
   * *Layer 2* : Encapsulation dans une trame Wi-Fi/Ethernet avec les adresses MAC source et destination (passerelle).
5. **Traduction NAT** : Le routeur retranscrit l'IP source privée en son IP publique (`203.0.113.45`) et modifie le port source.
6. **Réponse Serveur** : Le pare-feu du serveur vérifie le trafic, le serveur web (Apache/Nginx/IIS) traite la requête et renvoie la page web (`200 OK`).
7. **Décapsulation** : L'ordinateur reçoit la réponse, retire les en-têtes (L2 $\rightarrow$ L3 $\rightarrow$ L4) et le navigateur affiche le HTML/CSS.

---

## 5. Skills Assessment (HTB Lab Notes)

### Commandes Utiles Pwnbox / Linux

```bash
# Afficher toutes les interfaces réseau (même inactives)
ifconfig -a

# Afficher les connexions réseau et ports en écoute (format numérique)
netstat -tulnp4

# Afficher les services avec résolution de nom (ex: localhost, http, ssh)
netstat -tulp4

# Connaître la route empruntée vers une cible
ip route get <TARGET_IP>

# Tester la joignabilité d'un hôte (ICMP Layer 3)
ping -c 4 <TARGET_IP>

# Scanner les ports TCP d'une machine distante
nmap <TARGET_IP>

# Scanner des ports spécifiques avec scripts par défaut et détection de version
nmap -p21,80 -sC -sV <TARGET_IP>

# Connexion TCP brute avec Netcat
nc -v <TARGET_IP> <PORT>
