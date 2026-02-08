# configuration

Infrastructure and runtime configuration for the scalable ecommerce platform. This project provides Docker Compose, database initialization, and Keycloak realm import files so local development matches the platform specification.

## Project Scope (roadmap.sh)
This workspace follows the technical specifications from https://roadmap.sh/projects/scalable-ecommerce-platform.

Core microservices listed in the spec:
- User Service
- Product Catalog Service
- Shopping Cart Service
- Order Service
- Payment Service
- Notification Service

Additional components listed in the spec:
- API Gateway
- Service Discovery
- Centralized Logging
- Docker and Docker Compose
- CI/CD Pipeline

High-level implementation steps from the spec:
1) Set up Docker and Docker Compose
2) Develop microservices (start with MVPs)
3) Integrate services (REST or gRPC, plus API Gateway)
4) Implement Service Discovery (e.g., Consul or Eureka)
5) Set up monitoring and logging (Prometheus/Grafana, ELK)
6) Deploy (Docker Swarm or Kubernetes with autoscaling and load balancing)
7) CI/CD integration (Jenkins, GitLab CI, or GitHub Actions)

## What is in this project
- `docker-compose.yml` for local infrastructure.
- `postgres/initdb.d/00-create-dbs.sql` to create base databases.
- `keycloak/import/realm-export.json` for realm, roles, and clients.

Services defined in `docker-compose.yml`:
- `postgres` (PostgreSQL 16)
- `keycloak` (Keycloak 25)
- `user-service` (built from `../user-service`)

## Quick Start
From this folder:
```bash
docker compose up -d
```

## Keycloak Notes
- Realm: `ecommerce`
- Realm roles: `USER`, `ADMIN`, `WORKER`
- Clients:
  - `user-service` (service account, admin API)
  - `user-service-login` (direct login via password grant)

Secrets in `keycloak/import/realm-export.json` are placeholders. Update them for real environments.

## Databases
The init script creates:
- `keycloak`
- `users`

Add more databases in `postgres/initdb.d/00-create-dbs.sql` as new services are introduced.

