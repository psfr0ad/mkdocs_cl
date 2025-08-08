# Configuration

---

Bienvenue dans la section **Configuration**.  
Cette page est destinée à détailler les étapes nécessaires pour configurer votre client léger Debian.

---

## Table des matières

- [Introduction](#introduction)  
- [Configuration système](#configuration-système)  
- [Configuration utilisateur](#configuration-utilisateur)  
- [Configuration réseau](#configuration-réseau)  
- [Configuration avancée](#configuration-avancée)  

---

## Introduction

Configurer correctement un client léger Debian est une étape cruciale pour garantir des performances optimales, une sécurité renforcée et une expérience utilisateur fluide.

Cette section vous guidera à travers les principales étapes de configuration, notamment :

- L’optimisation de l’environnement système
- La mise en place d’une session légère (LXDE, XFCE, ou autre)
- La gestion des connexions distantes (RDP, VNC, SSH)
- La configuration réseau (fixe ou DHCP)
- Le durcissement de la sécurité système

!!! info "Public visé"
    Cette section s’adresse principalement aux administrateurs système, formateurs, ou toute personne souhaitant déployer un poste Debian simple, rapide et sécurisé.

---

## Pourquoi une configuration personnalisée ?

Un client léger bien configuré permet de :

- Réduire la charge sur le matériel
- Limiter les risques de failles ou d’abus
- Adapter le poste aux besoins précis de l’utilisateur
- Automatiser les tâches répétitives

---

Dans les pages suivantes, nous allons aborder les configurations minimales et avancées, avec des commandes en ligne et des bonnes pratiques éprouvées.

> *Prenez le temps de lire chaque étape avant de l’appliquer à votre système réel.*


---

## Configuration utilisateur

Dans un environnement client léger, il est important de créer un utilisateur dédié et de **limiter ses droits** pour garantir la sécurité et le bon fonctionnement du système.

Cette section vous guide pour :

- Créer un nouvel utilisateur
- Définir son mot de passe
- Restreindre ses privilèges (suppression du droit `sudo`)
- Appliquer les bonnes pratiques de sécurité

---

## 🧑‍💻 Création de l'utilisateur

Nous allons créer un utilisateur standard, par exemple nommé `client`.


`sudo adduser client`

Le système vous demandera :

 - Mot de passe

 - Informations facultatives (vous pouvez les laisser vides)

 🔐 Retirer les droits sudo

Par défaut, l’utilisateur n’a pas accès à sudo.

Mais si vous l’avez ajouté à un groupe comme sudo ou adm par erreur, vous pouvez le retirer :

`sudo deluser client sudo`

Vérifiez qu’il n’appartient à aucun groupe privilégié :

`groups client`

L'utilisateur ne doit faire partie que de groupes standards comme client, users, etc.


!!! warning "Important"
    Ne retirez pas vos propres droits sudo si vous êtes connecté avec cet utilisateur !
    Assurez-vous d’avoir un accès administrateur via un autre compte.

---

✅ Bonnes pratiques
Ne jamais donner sudo à un utilisateur final non technique

Bloquer les accès à des fichiers sensibles (/etc, /var/log, etc.)

Activer des politiques de mots de passe si nécessaire (pam_pwquality, chage, etc.)

---

## Configuration des appliations .desktop et .sh :

1) Configuration d'un autostart d'application ici pour Remmina 
- créer le répertoire: 

 `sudo mkdir -p /home/client/.config/autostart`

- créer le fichiers:
 
`sudo nano /home/client/.config/autostart/remmina.desktop`

- Ajouter ceci dans le fichiers :

```bash
[Desktop Entry]
Type=Application
Name=Remmina
Exec=/usr/bin/remmina
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
```

- Rendre le fichiers éxecutable :

`chmod +x /home/client/.config/autostart/remmina.desktop`

!!! info "résultat attendue"
    Lorsque vous vous connecterez à l'utilisateur `client`, Remmina se lancera automatiquement sur le bureau, sans aucune action de votre part, prêt à l'emploi.


---

## Configuration avancée

<!-- Contenu à venir -->

---

> *N’hésitez pas à revenir régulièrement pour consulter les mises à jour de cette section.*
