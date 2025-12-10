# HOMELAB

Ce dépôt contient la documentation et les fichiers d’infrastructure de mon homelab.
Vous y trouverez des notes, des configurations et des mises en place concernant l’infrastructure, les applications, le réseau, et plus encore.

## Prérequis

## Logiciels

* [Technitium DNS](https://technitium.com/dns/) comme serveur DNS
* [Wireguard](https://www.wireguard.com/) comme VPN
* [TrueNAS](https://www.truenas.com/truenas-community-edition/) comme système NAS pour la gestion des données

## Installation de Proxmox

* Téléchargez l’image ISO de l’installateur Proxmox VE depuis [le site officiel](https://www.proxmox.com/en/downloads).
* Créez une clé USB bootable avec l’image ; Pour ce faire, j’ai utilisé [Rufus](https://rufus.ie/en/).
* Branchez la clé USB sur votre serveur et définissez l’USB comme premier périphérique de démarrage dans le BIOS.
* Procédez à l’installation via l’interface graphique.

| Champ             | Valeure         | Explication                                        |
|-------------------|------------------|----------------------------------------------------------------------------------------|
| Hostname (FQDN)   | pve.homelab      | Nom de domaine complet pour le serveur Proxmox. Choisissez ce qui vous convient.       |
| IP Address (CIDR) | 192.168.1.50/24  | Adresse IP statique avec masque CIDR. Doit être statique et libre.                     |
| Gateway           | 192.168.1.1      | La passerelle ou le routeur utilisé pour le trafic sortant. Ici, l’IP de votre routeur.|
| DNS Server        | 1.1.1.1          | Résolveur DNS pour les requêtes. Vous pouvez mettre 8.8.8.8 ou 1.1.1.1.                |

[ x ] Pin Interfaces - Cochez cette case, cela évite des problèmes futurs.

Une fois l’installation terminée, retirez la clé USB bootable et redémarrez votre serveur. Celui-ci affichera alors son adresse IP. Utiliser cette adresse avec le port 8006 pour accéder à l’interface Web de Proxmox.

Lors de votre première connexion, une notification apparaîtra:

> **No Valid Subscription**</br>
> ⚠️  You do not have a valid subscription for this server...

Cette fenêtre apparaît parce que nous utilisons la version communautaire gratuite de Proxmox sans licence entreprise. Ce n’est qu’un avertissement : il n’y a aucune limitation fonctionnelle. Cela encourage simplement à payer pour le support, mais toutes les fonctionnalités restent accessibles via les dépôts communautaires. Pour supprimer cette fenêtre, nous pouvons modifier un fichier JavaScript (proxmoxlib.js) ou utiliser un script communautaire destiné à Proxmox.

## Scripts communautaires Proxmox (Community Helper Scripts)

Les Proxmox Community Helper Scripts sont une collection d’outils d’automatisation open source pour Proxmox VE, conçus pour simplifier les tâches courantes comme l’installation d’applications (Plex, Jellyfin, Docker, etc.) dans des conteneurs LXC légers.
Ils peuvent également aider à configurer les dépôts, supprimer l’avertissement d’abonnement, nettoyer les anciens noyaux, offrir des assistants interactifs et fournir des paramètres sécurisés pour les homelabs.
Cette vaste bibliothèque de scripts maintenus par la communauté permet de réduire des opérations allant jusqu'à 30–60 minutes à seulement 30 secondes.