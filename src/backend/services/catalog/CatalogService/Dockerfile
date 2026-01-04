FROM node:20-alpine
WORKDIR /app

COPY src/backend/services/catalog/CatalogService/package*.json ./
RUN npm ci

COPY src/backend/services/catalog/CatalogService/ ./
EXPOSE 3000
CMD ["npm", "run", "start:dev"]
