# eShop — Fullstack Cloud-Native Microservices Showcase (Monorepo)

Showcase dự án fullstack “A–Z” theo hướng **Cloud-Native Microservices**: từ code backend/frontend/mobile → chạy local → docker/infra → CI/CD → Kubernetes → Cloud (Azure/AWS).

---

## Tech Stack (Base)

- **Backend:** .NET 10 Web APIs (Microservices), **API Gateway (YARP)**
- **Data/Infra (local):** SQL Server, Kafka (docker-compose)
- **Frontend:** Next.js (TypeScript, App Router, Tailwind)
- **Mobile:** React Native (Expo)
- **DevOps (roadmap):** Docker, Kubernetes, GitHub Actions, AKS/EKS

---

## Repository Structure

```txt
eShop/
  src/
    backend/                 # .NET microservices + gateway (+ docker-compose infra)
    frontend/
      web/                   # Next.js web app
    mobile-app/
      eShopMobile/           # React Native (Expo) app
  .github/workflows/         # CI/CD (planned)
  README.md
