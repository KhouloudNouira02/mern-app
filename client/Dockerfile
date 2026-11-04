FROM node:lts-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Variable transmise lors du build pour fixer l'URL de l'API
ARG REACT_APP_API_URL=http://localhost:9000
ENV REACT_APP_API_URL=$REACT_APP_API_URL

# Build de l'application statique React
RUN npm run build

# Installation d'un serveur Web léger
RUN npm install -g serve

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]