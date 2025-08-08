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
---


## Mises à jour de sécurité

<!-- Contenu à venir -->

---

## Pare-feu et protections

<!-- Contenu à venir -->

---

> *La sécurité est un élément clé, gardez cette section à jour.*
