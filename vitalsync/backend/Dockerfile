# Un multi-stage build permet de découper les étapes de construction d'une image en plusieurs étapes, afin de ne conserver que les fichiers nécessaires à sa configuration et création. Cela permet de réduire la taille finale d'une image.

# En terme de sécurité, comme la taille de l'image est réduite à son strict nécessaire, cela réduit le champ d'attaque possible quand une dépendance a une faille de vulnérabilité.

# Dependencies install and tests execution
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm test

# build a lightweight image with alpine
FROM node:20-alpine
WORKDIR /app
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/package*.json ./
COPY --from=build /app ./
EXPOSE 3000
CMD ["node", "dist/server.js"]