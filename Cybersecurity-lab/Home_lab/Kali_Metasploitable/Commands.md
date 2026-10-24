**Nmap** et **Netcat (nc)** sont deux des outils en ligne de commande les plus puissants et incontournables pour l'administration réseau et la cybersécurité. Bien qu'ils opèrent tous les deux sur des réseaux TCP/IP, leurs objectifs sont très différents : Nmap sert à **cartographier et auditer**, tandis que Netcat sert à **interagir et transférer**.

Voici le détail de leur fonctionnement et de leurs usages.

---

## Nmap (Network Mapper)

Nmap est l'outil de référence pour l'exploration réseau et l'audit de sécurité. Il excelle dans la découverte d'appareils sur un réseau et l'identification précise des portes (ports) qui y sont ouvertes.

**Comment il fonctionne :** Il envoie des paquets réseau spécifiquement forgés aux hôtes cibles et analyse leurs réponses pour déduire ce qui se trouve en face.

**Principales fonctionnalités :**

*   **Découverte d'hôtes (Ping Sweep) :** Identifier quelles adresses IP sont actives sur un réseau.
*   **Scan de ports :** Déterminer quels ports (parmi les 65535 possibles) sont ouverts, fermés ou filtrés par un pare-feu.
*   **Détection de services et versions (`-sV`) :** Interroger les ports ouverts pour identifier exactement quel logiciel et quelle version y tournent (ex: Apache 2.4.41).
*   **Détection d'OS (`-O`) :** Deviner le système d'exploitation de la cible en analysant son comportement réseau (TCP/IP fingerprinting).
*   **Moteur de scripts (NSE) :** Automatiser des tâches avancées, comme la détection de vulnérabilités connues ou des attaques par force brute basiques.

**Commandes courantes :**

*   `nmap 192.168.1.1` : Scan rapide des 1000 ports les plus courants sur une IP.
*   `nmap -p- 192.168.1.1` : Scan complet des 65535 ports.
*   `nmap -A 192.168.1.1` : Scan agressif (détection d'OS, de version, scripts par défaut et traceroute).

---

## Netcat (nc)

Surnommé le "couteau suisse" du réseau TCP/IP, Netcat est un utilitaire brut, simple et extrêmement flexible. Il ne fait qu'une chose, mais il le fait parfaitement : **lire et écrire des données à travers des connexions réseau** (TCP ou UDP).

**Comment il fonctionne :** Il peut agir soit comme un serveur (en écoutant sur un port) soit comme un client (en se connectant à un port), et redirige l'entrée standard (stdin) vers la sortie standard (stdout) à travers le réseau.

**Principales fonctionnalités :**

*   **Création de serveurs et clients à la volée :** Parfait pour tester si un flux réseau passe à travers un pare-feu.
*   **Transfert de fichiers :** Envoyer un fichier d'une machine à une autre sans avoir besoin de configurer FTP, SSH ou un serveur web.
*   **Bannières (Banner Grabbing) :** Se connecter manuellement à un service (comme un serveur web ou mail) pour lire le texte brut qu'il renvoie.
*   **Reverse Shells & Bind Shells :** Très utilisé en cybersécurité offensive (pentest) pour obtenir un accès en ligne de commande (shell) sur une machine distante.

**Commandes courantes :**

*   `nc -l -p 4444` : Ouvre le port 4444 en écoute (mode serveur). Tout ce qui est reçu sera affiché à l'écran.
*   `nc 192.168.1.1 4444` : Se connecte au port 4444 de la machine cible (mode client). Vous pouvez alors taper du texte pour l'envoyer.
*   `nc -zv 192.168.1.1 80` : Teste rapidement (sans envoyer de données) si le port 80 est ouvert sur la cible.

---

> **En résumé :** On utilise d'abord **Nmap** pour scanner un réseau et découvrir qu'un serveur a le port 80 ouvert. Ensuite, on utilise **Netcat** pour se connecter manuellement à ce port 80 et lui envoyer des requêtes pour voir comment il réagit.
