# Bank system: documentation

Banking solution built with Java 17, Spring Boot, WebFlux, RxJava 3, MongoDB,
Spring Cloud (Config, Eureka, Gateway), Resilience4j, Redis, Kafka and JWT.

## Repositories
| Repository | Port | Part | Purpose |
|---|---|---|---|
| config-repo | - | I | Externalized configuration (YAML) |
| config-server | 8888 | I | Serves the configuration |
| eureka-server | 8761 | II | Service registry |
| api-gateway | 8080 | II | Single entry point, validates JWT |
| customer-service | 8081 | I | Customers (personal / business, VIP / PYME) |
| account-service | 8082 | I | Accounts, rules by customer and profile |
| credit-service | 8083 | I | Credits and credit cards, overdue debt |
| transaction-service | 8084 | I | Deposits, withdrawals, transfers, payments, fees |
| report-service | 8085 | II | Reports by date range and last 10 movements |
| auth-service | 8086 | III | Registration, login and JWT |
| debit-card-service | 8087 | III | Debit cards and payments (Kafka) |
| yanki-service | 8088 | III | Mobile wallet |

## Architecture
- `diagrams/architecture.png` and `architecture.drawio`: one page per part.
- Database per service (MongoDB). Redis caches customers. Kafka connects the
  Part III services without REST calls.

## Run locally (IntelliJ)
1. Start MongoDB, Redis and Kafka (see below).
2. Start in this order: config-server, eureka-server, business services,
   auth-service, api-gateway.
3. Import `postman/` and log in through `POST /auth/login`.