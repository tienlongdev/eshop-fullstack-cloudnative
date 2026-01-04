# eShop — Fullstack Cloud-Native Microservices Showcase (Monorepo)

---

## Tech Stack

### Backend Platform
- **Services:** .NET 10 + NestJS
- **Messaging:** Kafka
- **Databases:** PostgreSQL + MongoDB + Redis
- **Gateway:** YARP (.NET)

### Frontend / Mobile
- **Web:** Next.js (TypeScript)
- **Mobile:** React Native (Expo)

---

## Folder Structure

```txt
eShop/
  src/
    backend/
      services/
        ordering/OrderingService/      # .NET 10
        catalog/CatalogService/        # NestJS
      gateways/
        api-gateway/ApiGateway/        # YARP
      deploy/
        compose/docker-compose.yml     # postgres + mongo + redis + kafka + kafka-ui
    frontend/
      web/                             # Next.js
    mobile-app/
      eShopMobile/                     # Expo React Native
  README.md
```


## Run Backend (APIs)

> Start theo thứ tự: **Infra → Services → Gateway**  
> Mỗi service nên chạy ở **một terminal riêng**.

```txt
# 0) Go to repo root
cd C:\dev\eShop

# 1) Start local infrastructure (Postgres + Mongo + Redis + Kafka)
cd src\backend\deploy\compose
docker compose up -d

# Kafka UI: http://localhost:8080

# 2) Start OrderingService (.NET 10)
cd C:\dev\eShop\src\backend
dotnet run --project services\ordering\OrderingService --urls http://localhost:5002

# 3) Start CatalogService (NestJS)
cd C:\dev\eShop\src\backend\services\catalog\CatalogService
npm.cmd install
npm.cmd run start:dev
# Default: http://localhost:3000

# 4) Start API Gateway (YARP)
cd C:\dev\eShop\src\backend
dotnet run --project gateways\api-gateway\ApiGateway --urls http://localhost:5000


# Stop local infrastructure (when done)
cd C:\dev\eShop\src\backend\deploy\compose
docker compose down

```

## Run Web (Next.js)

> Web sẽ chạy cố định port **3001**.

```txt
cd C:\dev\eShop\src\frontend\web
npm.cmd install
npm.cmd run dev -- -p 3001

# Open: http://localhost:3001


```


## Run Mobile (React Native / Expo)

```txt

cd C:\dev\eShop\src\mobile-app\eShopMobile

npm.cmd install

npm.cmd start

```