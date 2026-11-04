FROM node:lts-alpine

WORKDIR /app

# Copie des fichiers de dépendances
COPY package*.json ./
RUN npm install

# Copie du reste du code du serveur
COPY . .

EXPOSE 9000

# Variable de connexion à MongoDB
ENV MONGO_URI=mongodb://mongodb:27017/mern

CMD ["npm", "start"]