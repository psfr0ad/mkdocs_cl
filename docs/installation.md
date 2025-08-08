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

---
## 🎛️ Installation de l'extension pour restreindre le bureau client

Dans un environnement client léger, il est souvent nécessaire de **limiter l’accès à certaines fonctionnalités de l’environnement graphique** pour améliorer la sécurité, la stabilité, ou simplifier l’expérience utilisateur.

L'extension **Just Perfection** permet de personnaliser à l'extrême l'interface Gnome et de masquer les éléments inutiles.

---

### 🧩 1. Installer l’extension manager

Commencez par installer l’application **Gnome Shell Extension Manager**, qui permet d’explorer et de gérer les extensions directement depuis le bureau.

`sudo apt install gnome-shell-extension-manager`

Une fois installée, lancez-la via le menu d’applications ou avec la commande :

`gnome-shell-extension-manager` 

**🔍 2. Rechercher l’extension "Just Perfection"**
Dans l’Extension Manager :

Allez dans l’onglet "Browse" (ou "Parcourir").

Recherchez "Just Perfection" dans la barre de recherche.

Cliquez sur Install pour l’installer.

**🧼 3. Désactiver les éléments du bureau**
Après installation :

- Allez dans l’onglet "Installed"

- Cliquez sur Just Perfection

- Cliquez sur "Personnaliser"

Dans les options, désactivez tout ce que vous ne souhaitez pas afficher, notamment :

- Activités

- Barre supérieure

- Menu utilisateur

- Dock

- Bouton d’alimentation

- Etc.

Laissez uniquement "Show Desktop Icons" ou "Desktop Shortcuts" activé, pour que les raccourcis du bureau restent visibles (par exemple, Remmina ou Firefox).

!!! info "Conseil"
    Pensez à tester la session avec un utilisateur non-administrateur pour valider le rendu final avant de déployer à grande échelle.

Avec Just Perfection, vous obtenez un bureau épuré, sécurisé, et parfaitement adapté à une utilisation client léger.

---

### ✅ Résultat

Tu obtiens :

- Un bureau **sans distractions**
- Un accès réduit aux fonctionnalités système
- Une meilleure UX pour les utilisateurs peu techniques

---

### 💡 Tu veux aller plus loin ?

Je peux t’ajouter une section sur :

- Le verrouillage du clic droit
- Le lancement automatique d'applications
- La suppression de la barre des tâches




> *N’hésitez pas à revenir régulièrement pour consulter les mises à jour de cette section.*
