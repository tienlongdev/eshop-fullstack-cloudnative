# eShop — E-commerce Platform (Cellphones-style) | Polyglot Microservices 2026 (Monorepo)

Mục tiêu: xây dựng hệ thống TMĐT kiểu **cellphones.com.vn** (catalog lớn, biến thể sản phẩm, flash-sale, tồn kho theo kho/chi nhánh, checkout + thanh toán, theo dõi đơn, CMS home sections, search) theo kiến trúc **Cloud-Native Microservices 2026**.

Showcase: polyglot runtime, event-driven Kafka, database-per-service, gateway, observability, CI/CD, K8s, Cloud.

----

## 1) Tech Stack

### Backend Platform
- **Services:** .NET 10 + NestJS (polyglot microservices)
- **Messaging:** Kafka (event-driven)
- **Databases:** PostgreSQL + MongoDB + Redis (polyglot persistence)
- **Gateway:** YARP (.NET)
- **Observability (roadmap):** OpenTelemetry + Grafana + Tempo/Jaeger
- **Deploy (roadmap):** Docker + Kubernetes + GitHub Actions + Cloud (AKS/EKS)

### Frontend / Mobile
- **Web:** Next.js (TypeScript)
- **Mobile:** React Native (Expo)

---

## 2) Folder Structure

```txt
eShop/
  src/
    backend/
      services/
        auth/AuthService/                  # Auth/OIDC (phase 2: Keycloak / custom)
        catalog/CatalogService/            # Product, Category, Brand, Variant (Mongo)
        pricing/PricingService/            # Price, promo, voucher (Postgres)
        inventory/InventoryService/        # Stock, reservation (Redis + Postgres)
        cart/CartService/                  # Cart (Redis)
        ordering/OrderingService/          # Checkout, order lifecycle (Postgres)
        payment/PaymentService/            # Payment intent + webhook (Postgres)
        notification/NotificationWorker/   # consume Kafka: email/sms/push
        cms/CmsService/                    # home sections, banners, landing pages
        search/SearchService/              # search (phase 3: OpenSearch/Elastic)
        ai/AiAssistantService/             # recommendation/semantic search (phase 4)
      gateways/
        api-gateway/ApiGateway/            # YARP gateway
      libs/
        contracts/                         # event schemas, OpenAPI/AsyncAPI
    frontend/
      web/                                 # Next.js
    mobile-app/
      eShopMobile/                         # Expo RN
  docker-compose.yml                        # run infra + services (planned)
  README.md
```

## Run Backend (APIs)

> Dev mode: chạy theo thứ tự **Infra → Services → Gateway**   
> Mỗi service nên chạy ở **một terminal riêng**.

```txt
# Terminal 0 — Start Infra (Postgres + Mongo + Redis + Kafka)
cd C:\dev\eShop\src\backend\deploy\compose
docker compose up -d

# Kafka UI: http://localhost:8080

# Start OrderingService (.NET 10)
cd C:\dev\eShop\src\backend
dotnet run --project services\ordering\OrderingService --urls http://localhost:5002


# Start CatalogService (NestJS)
cd C:\dev\eShop\src\backend\services\catalog\CatalogService
npm.cmd install
npm.cmd run start:dev
# Default: http://localhost:3000

# Start API Gateway (YARP)
cd C:\dev\eShop\src\backend
dotnet run --project gateways\api-gateway\ApiGateway --urls http://localhost:5000

# Stop Infra (khi chạy xong)
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