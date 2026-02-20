🇬🇧 English version available [here](README.md)

---

# Présentation du projet `transcendance`

## Introduction

*Ce projet a été réalisé en **duo avec [Bibickette](https://github.com/bibickette)***

Ce README est organisé comme suit :

- [Description](#description)

- [Langages & Technologies](#langages--technologies)
  - [Langages](#langages)
  - [Technologies](#technologies)

- [Concepts clés](#concepts-clés)

- [Fonctionnalités](#fonctionnalités)

- [Captures d’écran](#captures-décran)
  - [Accueil & Authentification](#-accueil--authentification)
  - [Accueil une fois connecté](#-accueil-une-fois-connecté)
  - [Menu Pong & Gameplay](#-menu-pong--gameplay)
  - [Navigation & Statut en temps réel](#-navigation--statut-en-temps-réel)
  - [Gestion utilisateur](#-gestion-utilisateur)
  - [Amis & Profil public](#-amis--profil-public)
  - [Ressources & Crédits](#ressources--crédits)

- [Environnement système](#environnement-système)
  - [Base des conteneurs](#base-des-conteneurs)
  - [Environnement frontend](#environnement-frontend)
  - [Sécurité](#sécurité)
  - [Persistance des données](#persistance-des-données)

- [Structure du projet](#structure-du-projet)
  - [Variables d’environnement](#variables-denvironnement)

- [Accès à la base de données](#accès-à-la-base-de-données)

- [Utiliser `transcendance`](#utiliser-transcendance)
  - [Règles du Makefile](#règles-du-makefile)
  - [Comment utiliser `transcendance`](#comment-utiliser-transcendance)

---

## Description

Transcendance est une application **full-stack** de type **Single Page Application** (SPA) développée entièrement en **TypeScript**. Elle est conçue pour offrir une expérience **sécurisée**, **temps réel** et **multijoueur**, ainsi qu’une gestion dynamique des utilisateurs.

Les principaux objectifs du projet sont :
- Gameplay en temps réel : **Pong** classique, joueur contre joueur ou contre IA.
- Authentification sécurisée avec **JWT**, **2FA** optionnelle et **authentification distante**.
- Interactions utilisateur dynamiques : présence en ligne et demandes d’amis via **WebSockets**.
- SPA full-stack : backend et frontend fortement intégrés.
- Support multilingue (EN, FR, CN) via un **dictionnaire fait maison (i18n)** accessible sur tout le site.
- Environnement sécurisé et conteneurisé avec **HTTPS/TLS**, certificats SSL et services Docker isolés.

Ce projet illustre de bonnes pratiques en **sécurité web**, authentification, communication temps réel et orchestration de conteneurs.

* * *

## Langages & Technologies

### Langages
1. **TypeScript** : langage full-stack utilisé à la fois côté backend (serveur Fastify) et côté frontend (SPA). Apporte un typage statique pour un code plus sûr et maintenable.
2. **HTML** : langage de balisage pour structurer les pages frontend.
3. **JSON** : format utilisé pour les requêtes/réponses API, la configuration et le stockage de données structurées (dictionnaires, état du jeu, etc.).
4. **CSS** : style du frontend, via **TailwindCSS**, un framework moderne basé sur des classes utilitaires.

### Technologies

**Backend**
1. **Fastify** : framework Node.js utilisé côté backend. Gère le routage, les APIs REST, l’authentification et les WebSockets.
2. **SQLite** : base de données relationnelle légère stockant les informations utilisateurs, statistiques de jeu et le dictionnaire global.
3. Modules d’authentification :
   - **JWT & 2FA** : flux de connexion standard :
     - L’utilisateur se connecte avec email/mot de passe (haché en base).
     - Le backend délivre un token JWT pour gérer la session.
     - Si activée, la 2FA est requise pour finaliser la connexion.
   - **Authentification distante** :
     - Connexion via des fournisseurs externes (ex. GitHub).
     - Le backend délivre un JWT après une connexion distante réussie.
4. **Serveur WebSocket** : mises à jour temps réel pour :
   - Statut en ligne/hors ligne des amis
   - Réception de demandes d’amis

**Frontend**
1. **SPA en TypeScript vanilla** : gère toute la logique côté client.
2. **TailwindCSS** : framework CSS moderne, utilitaire, pour le style.
3. **Vite** : serveur de dev avec rechargement à chaud rapide.

**Infrastructure**
1. **Docker & Docker Compose** : environnements de dev et prod conteneurisés.
2. **NGINX** : reverse proxy en production avec SSL/TLS pour des connexions HTTPS sécurisées.
3. **Réseau de conteneurs** : communication isolée et sécurisée entre services.

* * *

## Concepts clés

1. **SPA full-stack** : application monopage alimentée par un backend sécurisé et un frontend dynamique.
2. **Communication temps réel** : WebSockets pour la présence en ligne, les événements de jeu et les notifications live.
3. **Authentification & Sécurité** : système de login sécurisé incluant :
   - Connexion locale avec mots de passe hachés, sessions JWT et 2FA optionnelle
   - Authentification distante via fournisseurs externes (GitHub OAuth)
   - HTTPS/TLS imposé partout
4. **Mécaniques de gameplay** : Pong classique avec IA ou multijoueur, incluant des tournois.
5. **Gestion de base de données** : SQLite pour la persistance des informations utilisateurs.
6. **Support multilingue** : système de dictionnaire permettant plusieurs langues sur tout le site.
7. **Déploiement conteneurisé** : Docker assure cohérence, reproductibilité et isolation des services.
8. **Style frontend** : UI responsive et moderne via TailwindCSS.

* * *

## Fonctionnalités

**Authentification**
- Sessions basées sur JWT avec mots de passe hachés.
- 2FA optionnelle pour plus de sécurité.
- Authentification distante (OAuth) avec GitHub.

**Gestion utilisateur**
- Inscription, connexion et gestion des utilisateurs.
- Liste d’amis avec statut en ligne/hors ligne en temps réel via WebSocket.
- Réception de demandes d’amis en temps réel.

**Gameplay**
- Pong classique : Joueur contre Joueur ou contre IA
- Mode tournoi : compétition via des matchs structurés
- Historique des parties et statistiques

**Frontend**
- SPA développée en TypeScript vanilla.
- Style via TailwindCSS.
- Hot reload en développement via Vite.

**Sécurité & Persistance**
- HTTPS/TLS imposé en développement et en production.
- Secrets et variables d’environnement stockés de manière sécurisée.
- Volumes Docker pour persister les images uploadées et la base SQLite.

* * *

## Captures d’écran

#### 🏠 Accueil & Authentification
<p align="center">
  <img src="screens/home.png" height="300">
</p>

<p align="center">
  <img src="screens/home_signup.png" height="250">
  <img src="screens/home_signin.png" height="250">
</p>

#### 🏠 Accueil une fois connecté
<p align="center">
  <img src="screens/home_login.png" height="300">
</p>

#### 🏓 Menu Pong & Gameplay
<p align="center">
  <img src="screens/pong.gif" height="300">
</p>
<p align="center">
  <img src="screens/pong_menu.png" height="300">
</p>

<p align="center">
  <img src="screens/pong_modal.png" height="300">
  <img src="screens/pong_history.png" height="300">
</p>

#### 🧭 Navigation & Statut en temps réel
<p align="center">
  <img src="screens/navbar.gif" height="100">
  <img src="screens/offonline.gif" height="100">
</p>

#### 👤 Gestion utilisateur
<p align="center">
  <img src="screens/profile.png" height="300">
  <img src="screens/profile_modal.png" height="300">
</p>

#### 👥 Amis & Profil public
<p align="center">
  <img src="screens/friends.png" height="300">
  <img src="screens/public_profile.png" height="300">
</p>

### Ressources & Crédits

Certaines ressources visuelles ont été adaptées à partir de ressources publiques disponibles en ligne, puis modifiées pour correspondre aux besoins de ce projet.

*Ce projet est strictement à but éducatif et non commercial.*

* * *

## Environnement système

Le projet Transcendance est entièrement conteneurisé avec **Docker** et orchestré avec **Docker Compose**. Les environnements **développement** et **production** sont conçus pour être **sécurisés**, **reproductibles** et isolés.

### Base des conteneurs
**Image de base** : `node:20-bullseye`  
**Runtime** : Docker  
**Orchestration** : Docker Compose

### Environnement frontend
1. **Serveur de développement** : serveur Vite en HTTPS.
   - Volume partagé pour appliquer immédiatement les modifications frontend dans le conteneur.
   - Rechargement à chaud (live reload) pour un développement rapide.

2. **Serveur de production** : reverse proxy NGINX servant la SPA en HTTPS.
   - La plupart des fichiers restent dans le conteneur pour l’isolation.
   - Dossiers persistants (photos de profil, base SQLite) montés en volumes partagés.

### Sécurité
- HTTPS est imposé en développement et en production.
- Les certificats sont gérés automatiquement à l’intérieur des conteneurs.
- Les fichiers sensibles, mots de passe et tokens sont stockés de manière sécurisée et ne sont jamais exposés dans le dépôt.

### Persistance des données
1. Des volumes partagés permettent de persister en toute sécurité :
   - Les images uploadées par les utilisateurs
   - La base de données SQLite
2. Les autres fichiers restent isolés dans les conteneurs afin d’éviter des modifications accidentelles ou des fuites.

* * *

## Structure du projet

```
transcendance/
│
├── backend/
│   ├── Dockerfile
│   ├── .env                # variables d’environnement
│   ├── src/
│   ├── data_db/
│   └── uploads/
│
├── config/certs
│
├── frontend/
│   ├── Dockerfile
│   ├── src/
│   ├── assets/
│   └── config/
│
├── logs/
│
├── docker-compose.yml
├── Makefile
└── README.md
```

* * *

### Variables d’environnement

Le projet utilise un fichier `.env` situé dans `packages/backend/` pour configurer les variables d’environnement.

⚠️ Le vrai fichier `.env` **ne doit pas** être commité.

Voici un exemple générique à titre de démonstration :

```
# OAuth GitHub
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_URL=https://github.com/
GITHUB_API=https://api.github.com/

# JWT
JWT_SECRET=change_me_in_production

# Développement uniquement, ne jamais utiliser en production
UNIVERSAL_PASSWORD=dev_password_only
FAKE_PASSWORD=fake_password_for_testing

# Service Email
GMAIL_APP_PASSWORD=your_gmail_app_password

# URL du frontend
# En développement : https://localhost:5173/
# En production : https://localhost:8443/
LOCALHOST=https://localhost:5173/
```

* * *

## Accès à la base de données

Liste de commandes pour **inspecter manuellement la base SQLite** :

1. Ouvrir le shell SQLite : `sqlite3 ./packages/backend/data_db/database.sqlite`
2. Lister les tables : `.tables`
3. Afficher les utilisateurs : `SELECT * FROM users;`
4. Quitter SQLite et le conteneur : `.exit`

* * *

# Utiliser `transcendance`

## Règles du Makefile

**🚀 Démarrage de l’environnement**

1. **all** en tant que *règle par défaut* : affiche un message invitant à choisir entre ***make dev*** ou ***make prod***.
2. **dev** : build et démarre l’environnement de développement via Docker Compose (volumes partagés + serveur Vite).
3. **prod** : build et démarre l’environnement de production via Docker Compose (reverse proxy NGINX + build optimisé).

**🛠 Setup & Initialisation**

4. **create** : exécute les règles *create_db*, *create_certs* et *create_logs*.
5. **create_db** : crée `data_db/` (dossier de base de données) et `uploads/users/` (dossier des avatars utilisateurs).
6. **create_certs** : crée `config/certs/` (dossier des certificats SSL).
7. **create_logs** : crée `logs/` (dossier de logs).

**🧹 Nettoyage**

8. **clean** : exécute *clean_db*, *clean_certs* et *clean_logs*.
9. **clean_db** : supprime `data_db/` (dossier de base de données) et `uploads/users/` (dossier des avatars utilisateurs).
10. **clean_certs** : supprime `config/certs/` (dossier des certificats SSL).
11. **clean_logs** : supprime `logs/` (dossier de logs).

**🔄 Reset complet**

12. **fclean_dev** : stop les conteneurs, supprime les volumes, et supprime les images Docker taguées `:dev`.
13. **fclean_prod** : stop les conteneurs, supprime les volumes, et supprime les images Docker taguées `:prod`.
14. **re_dev** : exécute *fclean_dev* puis *dev*.
15. **re_prod** : exécute *fclean_prod* puis *prod*.

**🐳 Gestion des conteneurs**

16. **stop** : stop les conteneurs en cours d’exécution sans les supprimer.
17. **down** : stop et supprime les conteneurs, réseaux et ressources associées.
18. **status** : affiche les conteneurs en cours, images Docker, réseaux et volumes.
19. **help** : affiche la liste des commandes du Makefile.

* * *

## Comment utiliser `transcendance`

1. Clonez `transcendance` dans un dossier : `git clone https://github.com/Naphiye/transcendance.git`
2. Allez dans le dossier `transcendance/packages/backend` puis créez un fichier d’environnement (`.env`) (*voir [variables d’environnement](#variables-denvironnement) et [structure du projet](#structure-du-projet) pour plus d’informations*).

### 🛠 Mode Développement
*⚠️ Si vous souhaitez alterner entre les modes développement et production, vous devez nettoyer la base de données au préalable.*

3. Allez dans le dossier `transcendance/` puis build et démarrez l’infrastructure avec `make dev`  
4. Vous pouvez maintenant accéder au site via `https://localhost:5173/`

**OU**

### 🚀 Mode Production
*⚠️ Si vous passez depuis le mode développement, nettoyez la base de données avant.*

3. Allez dans le dossier `transcendance/` puis build et démarrez l’infrastructure avec `make prod`  
4. Vous pouvez maintenant accéder au site via `https://localhost:8443/`

* * *
*Date de validation du projet : 12 décembre 2025*
