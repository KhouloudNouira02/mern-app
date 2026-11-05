FROM node:lts-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Définition de l'URL relative de l'API pour Nginx Proxy
ENV REACT_APP_API_URL=/api

# Construction des fichiers statiques de production
RUN npm run build

# Étape 2 : Serveur Web Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80