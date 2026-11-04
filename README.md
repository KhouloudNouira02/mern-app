# TP2 : Docker et Docker Compose - Application MERN



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
│   ├── docker-compose-up.png
│   └── web-app.png
├── docker-compose.yml
└── README.md