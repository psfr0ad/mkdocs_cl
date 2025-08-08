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

## Configuration des applications .desktop et .sh :

1) Configuration d'un autostart d'application ici pour Remmina 
- créer le répertoire: 

    `sudo mkdir -p /home/client/.config/autostart`

- **créer le fichiers:**
 
    `sudo nano /home/client/.config/autostart/remmina.desktop`

- **Ajouter ceci dans le fichiers :**

```bash
[Desktop Entry]
Type=Application
Name=Remmina
Exec=/usr/bin/remmina
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
```

- **Rendre le fichiers éxecutable :**

    `chmod +x /home/client/.config/autostart/remmina.desktop`

!!! info "résultat attendue"
    Lorsque vous vous connecterez à l'utilisateur `client`, Remmina se lancera automatiquement sur le bureau, sans aucune action de votre part, prêt à l'emploi.

2) Configuration d'un fichier .sh pour rendre les applications invisbles et inaccessible depuis le bureau avec `Nodisplay=true` :

- **créer le fichier suivant :**

    ` sudo nano /home/client/modif-client-app-NoD.sh`

- **Ajouter ceci dans le fichier :**

```bash 
#!/bin/bash

# Répertoire contenant les fichiers . desktop pour l'utilisateur actuel
client_desktop_dir="$HOME/. local/share/applications"

# Créer le répertotre s'il n'existe pas
mkdir -p "$client_desktop_dir"

# Copier les fichiers , desktop du répertoire système vers le répertotre utilisat
cp /usr/share/applications/*. desktop "$client_desktop_dir"/ 

# Parcourir chaque fichier, desktop dans le répertoire utilisateur
for desktop_file in "$client_desktop_dir"/*,desktop: do
    # Vérifier si le fichier contient "remmina" dans son
    if [[ "$desktop_file" != *"remmina"* ]]; then
        # Ajouter NoDisplay-true si ce n'est pas déjà fait
        if ! grep -q "^NoDisplay=true" "$desktop_file"; then
            echo "NoDisplay=true" >> "$desktop_file"
        fi
    fi
done 

echo "Les fichiers .desktop ont été modifiés pour l'utilisateur client."
```

- **Rendre le fichier éxecutable :**

    `chmod +x /home/client/modif-client-app-NoD.sh`

- **Éxecuter le fichiers :**

    `./chmod +x /home/client/modif-client-app-NoD.sh`

!!! info "résultat attendue"
    Dans le terminal, un message doit apparaître : "Les fichiers .desktop ont été modifiés pour l’utilisateur client."

!!! warning "Important"
    Enfin, remettez `NoDisplay=true` dans les fichiers .desktop que vous souhaitez rendre visibles sur le bureau de l'utilisateur concerné.

3) Création de l'application personnalisée pour le lien Firefox.

- **Créer le fichiers /firefox_url.desktop :** 

    `sudo nano /home/client/.local/share/applications/firefox_url.desktop`

- **Ajouter ceci dans le fichier :**

```bash
[Desktop Entry]
Type=Application
Name=Firefox_URL
Exec=firefox --new-window "votre_lien"
Terminal=false
Icon=firefox-esr
StartUpNotify=true
```

- **Changer le propriétaire et le groupe du fichier :**

    `sudo chown client:client /home/client/.local/share/applications/firefox_url.desktop`

- **Rendre le fichier éxecutable :**

    `sudo chmod +x  /home/client/.local/share/applications/firefox_url.desktop`

4) Création de l’application Logout (qui permettra de se déconnecter du client léger)

- **Créer le fichier `/logout.desktop`**

    `sudo nano /home/client/.local/share/applications/logout.desktop`

- **Ajouter ceci dans le fichier :**

```bash
[Desktop Entry]
Type=Application
Name=Logout
Exec=gnome-session-quit --logout --no-prompt
Terminal=false
Icon=system-log-out
StartUpNotify=true
```

- **Changer le propriétaire et le groupe du fichier :**

    `sudo chown client:client  /home/client/.local/share/applications/logout.desktop`

- **Rendre le fichier éxecutable :**

    `sudo chmod +x   /home/client/.local/share/applications/logout.desktop`

---

## Configuration avancée

<!-- Contenu à venir -->

---

> *N’hésitez pas à revenir régulièrement pour consulter les mises à jour de cette section.*
