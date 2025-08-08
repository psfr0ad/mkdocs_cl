# Installation

---

Bienvenue dans la section **Installation**.  
Ici, vous trouverez toutes les étapes nécessaires pour installer et configurer votre client léger Debian.

---

## Table des matières

- [Mise à jour du système](#mise-à-jour-du-système)  
- [Installation des paquets essentiels](#installation-des-paquets-essentiels)  
- [Configuration supplémentaire](#configuration-supplémentaire)  

---

## Mise à jour du système

**Commencez par mettre à jour la liste des paquets et le système :**

`sudo apt update && sudo apt upgrade -y`

Debian utilise un fichier appelé /etc/apt/sources.list pour définir les dépôts depuis lesquels il télécharge les logiciels.

**Voici un exemple de configuration propre et complète pour Debian stable :**

```bash
deb https://deb.debian.org/debian bookworm main non-free-firmware

deb-src https://deb.debian.org/debian bookworm main non-free-firmware

deb https://security.debian.org/debian-security bookworm-security main non-free-firmware

deb-src https://security.debian.org/debian-security bookworm-security main non-free-firmware

deb https://deb.debian.org/debian bookworm-updates main non-free-firmware

deb-src https://deb.debian.org/debian bookworm-updates main non-free-firmware
```



---

## Installation des paquets essentiels

**Installation du RDP Remmina :**

Remmina est un client de bureau à distance compatible RDP, VNC, SSH, etc. Il est idéal pour un poste client léger.

`sudo apt install remmina`

**Installation de gnome-extension-manager :**

Dans un environnement client léger, il est souvent nécessaire de **limiter l’accès à certaines fonctionnalités de l’environnement graphique** pour améliorer la sécurité, la stabilité, ou simplifier l’expérience utilisateur.

L'extension **Just Perfection** permet de personnaliser à l'extrême l'interface Gnome et de masquer les éléments inutiles.

`sudo apt install gnome-shell-extension-manager`

!!! info "configuration"
    Pour configurer voir la page de **[configuration](configuration.md)**

---





> *N’hésitez pas à revenir régulièrement pour consulter les mises à jour de cette section.*
