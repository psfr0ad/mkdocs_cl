# Sécurité

---

Cette section aborde les aspects essentiels pour sécuriser votre client léger Debian.

---

## Table des matières

- [Gestion des utilisateurs](#gestion-des-utilisateurs)  
- [Mises à jour de sécurité](#mises-à-jour-de-sécurité)  
- [Pare-feu et protections](#pare-feu-et-protections)  

---
!!! info danger "Danger"
     **Ne mettez pas en place la sécurité tant que l'installation et la configuration ne sont pas terminées.**

---

## Gestion des ACL pour l'utilisateur

L'objectif de cette configuration est de limiter l'accès aux outils système et applications de l'utilisateur `client` pour assurer une sécurité renforcée sur un poste client léger. Les **ACL** permettent de spécifier des permissions détaillées pour des utilisateurs et groupes, permettant de restreindre l'exécution de certaines commandes.

### Pourquoi utiliser les ACL ?
Les ACL permettent de **définir des permissions spécifiques** sur des fichiers et répertoires. Dans ce cas, elles sont utilisées pour empêcher l'utilisateur `client` d'exécuter des commandes sensibles ou des applications non nécessaires.

---

## Restreindre l'accès aux applications

Nous allons maintenant limiter l'accès à plusieurs applications de bureau essentielles, telles que le **centre de contrôle GNOME**, le **terminal GNOME**, et le **gestionnaire de logiciels GNOME**.

### Commandes pour limiter l'accès

Les commandes suivantes utiliseront `setfacl` pour **enlever les permissions d'exécution** pour l'utilisateur `client` sur certaines applications.

```bash
sudo setfacl -m u:client:0 /usr/bin/gnome-center-control

sudo setfacl -m u:client:0 /usr/bin/gnome-terminal

sudo setfacl -m u:client:0 /usr/bin/gnome-software
```

- Explications :

`gnome-center-control` : Empêche l'utilisateur client d'ouvrir le centre de contrôle GNOME.

`gnome-terminal`: Empêche l'utilisateur client d'ouvrir un terminal GNOME.

`gnome-software`: Empêche l'utilisateur client d'accéder au gestionnaire de logiciels GNOME pour installer ou mettre à jour des applications.


### Commandes sensibles

Certaines applications et outils système doivent être particulièrement surveillés et restreints, car ils permettent de gérer des configurations avancées ou des éléments essentiels du système. Voici une liste de commandes supplémentaires pour limiter l'accès à ces outils sensibles.

```bash
sudo setfacl -m u:client:0 /usr/bin/gnome-extensions-app

sudo setfacl -m u:client:0 /usr/bin/gnome-extensions

sudo setfacl -m u:client:0 /usr/bin/apt

sudo setfacl -m u:client:0 /usr/bin/dpkg

sudo setfacl -m u:client:0 /usr/bin/gnome-shell-extension-prefs
```

-Explications :

`gnome-extensions-app` et `gnome-extensions` : Empêchent l'utilisateur client de gérer les extensions GNOME.

`apt` et `dpkg` : Empêchent l'utilisateur client d'installer, de mettre à jour ou de supprimer des paquets avec APT et DPKG.

`gnome-shell-extension-prefs` : Empêche l'utilisateur client de modifier les préférences des extensions GNOME.

**Commandes sensibles à traiter avec précaution**

Ces commandes doivent être appliquées avec attention. Elles restreignent l'accès à des outils qui peuvent modifier l'environnement système de manière significative.

!!! warning "Important"
    Ne laissez pas ces commandes accessibles à des utilisateurs non autorisés. Ces outils peuvent affecter le système global.


**Désactivation du Bluetooth**

Si vous souhaitez désactiver l'accès au Bluetooth pour l'utilisateur client, vous pouvez également limiter l'accès aux outils Bluetooth avec les commandes suivantes :

```bash
sudo setfacl -m u:client:0 /usr/bin/bluetoothctl

sudo setfacl -m u:client:0 /usr/bin/hciconfig
```

Explications :

`bluetoothctl` : Empêche l'utilisateur client de gérer les périphériques Bluetooth.

`hciconfig` : Empêche l'utilisateur client de configurer les interfaces Bluetooth.


**Vérification des permissions :**

Après avoir appliqué les ACL, il est crucial de vérifier que l'utilisateur client ne peut pas exécuter les commandes restreintes. Vous pouvez tester les restrictions avec les commandes suivantes :

```bash
sudo -u client gnome-control-center

sudo -u client gnome-terminal

sudo -u client gnome-software

sudo -u client gnome-extensions-app
```

!!! info "attendue"
    permission denied


## Désactiver les téléchargements pour l'utilisateur `client`

Afin de restreindre les téléchargements dans le répertoire **Téléchargements** pour l'utilisateur `client`, nous allons utiliser deux commandes principales :

1. **Retirer les permissions d'exécution** sur le répertoire **Téléchargements**.
2. **Rendre le répertoire immutable** pour empêcher toute modification.

### Retirer les permissions d'exécution

La commande suivante permet de supprimer les permissions d'exécution pour l'utilisateur `client` sur le répertoire **Téléchargements**, ce qui empêche l'utilisateur d'y accéder via la ligne de commande :

```bash
sudo chmod -R -x /home/client/Téléchargements

sudo chattr +i /home/client/Téléchargements
```

---


## Mises à jour de sécurité

<!-- Contenu à venir -->

---

## Pare-feu et protections

<!-- Contenu à venir -->

---

> *La sécurité est un élément clé, gardez cette section à jour.*
