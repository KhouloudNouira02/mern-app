# TP2.1 : Déploiement d'une Application MERN sur AWS ECS et ECR

Ce projet présente le déploiement conteneurisé d'une application MERN (MongoDB, Express, React, Node.js) sur **AWS ECS avec AWS Fargate**, avec hébergement des images Docker sur **Amazon ECR**.

---

## Architecture du Déploiement

- **Frontend (Client)** : React servi par Nginx (Port 80) – image hébergée sur Amazon ECR[cite: 7].
- **Backend (Server)** : API Express/Node.js (Port 9000) – image hébergée sur Amazon ECR[cite: 7].
- **Base de données** : MongoDB Atlas (Connexion via String d'URI avec authentification)[cite: 9].
- **Orchestration** : AWS ECS Cluster (`mern-cluster`) avec Fargate et révision de tâche `mern-task:6`[cite: 9, 12].

---

##  Images Docker & Amazon ECR

Les images Docker ont été construites localement puis publiées sur Amazon ECR (Région : `us-east-1`)[cite: 7, 10] :

- **Client React (Nginx)** : `362416860691.dkr.ecr.us-east-1.amazonaws.com/mern-client:v1`[cite: 10]
- **Serveur Express** : `362416860691.dkr.ecr.us-east-1.amazonaws.com/mern-server:v1`[cite: 10]

---

##  Modifications Apportées

1. **`client/Dockerfile`** : Build multi-étapes Node.js vers Nginx Alpine[cite: 7].
2. **`client/nginx.conf`** : Redirection des requêtes API `/api/` vers le backend local et gestion du routage React[cite: 7].
3. **Variables d'environnement ECS** : Configuration sécurisée de `MONGO_URI` dans la définition de tâche `mern-task`[cite: 9, 12].

---

## Difficultés Rencontrées & Solutions

1. **Erreur d'authentification MongoDB (`bad auth` - Code 8000)** : 
   - *Problème* : Incohérence initiale entre le mot de passe dans MongoDB Atlas et la variable d'environnement `MONGO_URI` dans ECS[cite: 10].
   - *Solution* : Réinitialisation du mot de passe de l'utilisateur `khouloud` sur Atlas et mise à jour de la définition de tâche ECS vers la révision `mern-task:6`[cite: 10, 12].

2. **Expiration de session AWS Academy** : 
   - *Problème* : Expiration des identifiants temporaires de session IAM entraînant un blocage du déploiement.
   - *Solution* : Redémarrage de la session AWS Learner Lab et renouvellement du jeton de connexion AWS CLI / Docker.

3. **Inaccessibilité réseau sur IP privée (`100.60.75.156`)** :
   - *Problème* : Tentative initiale d'accès via l'adresse IP privée du VPC[cite: 10].
   - *Solution* : Récupération de l'adresse IP publique attribuée à la tâche Fargate (`54.175.19.80`)[cite: 9].

---

##  Nettoyage des Ressources

Afin d'éviter toute surconsommation de crédits AWS Academy / Learner Lab :
- Le service ECS `mern-task-service-8p06cpl2` et les tâches associées ont été arrêtés[cite: 9, 12].
- Le cluster ECS `mern-cluster` a été nettoyé[cite: 9].
- Les dépôts ECR `mern-client` et `mern-server` ainsi que les groupes de journaux CloudWatch ont été supprimés[cite: 10].