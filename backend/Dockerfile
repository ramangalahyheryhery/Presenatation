FROM node:18-alpine
WORKDIR /usr/src/app

COPY package*.json ./

# Installation dépendances
RUN npm ci --only=production

COPY . .

# Créer user non-root pour la sécurité
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

RUN chown -R nodejs:nodejs /usr/src/app
USER nodejs

EXPOSE 3000

ENV NODE_ENV=production
ENV PORT=3000

# Vérification de santé simplifiée
HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
  CMD wget -q -O - http://localhost:3000/ || exit 1

# Démarrer l'application
CMD ["node", "server.js"]
