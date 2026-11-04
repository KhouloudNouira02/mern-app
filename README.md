TP2 : Docker et Docker Compose - Application MERN


---

## Vue d'Ensemble

Ce projet consiste en la conteneurisation et l'orchestration d'une application full-stack MERN (MongoDB, Express, React, Node.js) en utilisant Docker et Docker Compose, conformément aux spécifications du TP2.

---

## Table des Matières

- [Technologies Utilisées](#technologies-utilisées)
- [Structure du Dépôt](#structure-du-dépôt)
- [Variables d'Environnement](#variables-denvironnement)
- [Configuration Docker](#configuration-docker)
- [Images Docker](#images-docker)
- [Docker Compose et Orchestration](#docker-compose-et-orchestration)
- [Instructions d'Exécution](#instructions-dexécution)
- [Diagnostics et Débogage](#diagnostics-et-débogage)
- [Captures d'Écran et Validation](#captures-décran-et-validation)

---

## Technologies Utilisées

- **Frontend** : React
- **Backend** : Node.js, Express
- **Base de Données** : MongoDB
- **Conteneurisation et Orchestration** : Docker, Docker Compose

---

## Structure du Dépôt

```text
mern-app/
├── client/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── ...
├── server/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── ...
├── screenshots/
│   ├── docker-images.png
│   ├── docker-compose.png
│   └── web-app.png
├── docker-compose.yml
└── README.md
Variables d'Environnement
Les variables d'environnement configurées pour l'application sont les suivantes :

REACT_APP_API_URL : Définit l'URL de l'API pour le client React afin de communiquer avec le serveur depuis le navigateur.

MONGO_URI : Chaîne de connexion à la base de données MongoDB utilisée par le serveur Express (mongodb://mongodb:27017/mern).

Configuration Docker
Server (Express)
Le fichier server/Dockerfile utilise l'image de base node:lts-alpine, copie les fichiers de dépendances, exécute npm install, expose le port 9000 et lance l'application via npm start.

Client (React)
Le fichier client/Dockerfile utilise node:lts-alpine, installe les dépendances, génère le build de production avec npm run build, utilise le serveur HTTP léger serve et expose le port 3000.

Images Docker
Les images construites pour ce projet sont :

Client : mern-client (construite à partir de ./client)

Serveur : mern-server (construite à partir de ./server)

Base de Données : mongo:latest

Docker Compose et Orchestration
Le fichier docker-compose.yml orchestre l'ensemble des services :

mongodb : Utilise l'image officielle mongo, connectée au réseau mern-network, avec un volume nommé mern-data pour la persistance des données. Un contrôle de santé (healthcheck) est configuré pour vérifier la disponibilité de la base de données.

server : Dépend de mongodb avec la condition service_healthy. Il expose le port 9000 et définit la variable MONGO_URI.

client : Dépend du service server et expose le port 3000.

Réseau : Un réseau de type bridge nommé mern-network assure la communication interne entre les conteneurs.

Instructions d'Exécution
Cloner le dépôt et naviguer dans le répertoire racine.

Construire les images et lancer les conteneurs :

Bash
docker compose up -d --build
Vérifier le statut des services :

Bash
docker compose ps
Accéder à l'application web via l'URL : http://localhost:3000

Diagnostics et Débogage
Pour diagnostiquer un service en cas d'erreur au démarrage :

Consulter les journaux du serveur :

Bash
docker compose logs --tail=50 server
Consulter les journaux de la base de données :

Bash
docker compose logs --tail=50 mongodb
Vérifier le statut d'exécution et de santé des conteneurs via docker compose ps.

Captures d'Écran et Validation
1. Images Docker construites
2. Déploiement Docker Compose et statut Healthy
3. Application Web et Persistance MongoDB