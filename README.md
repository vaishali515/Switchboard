# 🚀 Switchboard - Distributed Backend Platform

## Overview
A production-style distributed microservices backend built to explore
event-driven architecture, horizontal scalability, and full observability.
Processes 500–1,000 domain events/min via Apache Kafka.

Java 17 Spring Boot 3 Apache Kafka PostgreSQL Docker Prometheus Grafana

## Architecture
[Architecture diagram image goes here]

Client → Nginx (Reverse Proxy)
       → API Gateway
       → Auth Service · Notification Service · Portfolio Service
       → Apache Kafka (event bus)
       → RabbitMQ (async jobs)
       → PostgreSQL (Neon serverless)
       → Observability (Prometheus + Grafana + Loki + Tempo)

## Key Technical Decisions
| Decision | Choice | Why |
|---|---|---|
| Event streaming | Apache Kafka | Durable, high-throughput, replay capability |
| Async jobs | RabbitMQ | Per-service job queues, DLQ support |
| Auth | JWT + OAuth2 + Redis OTP | Stateless, scalable, TTL-enforced sessions |
| Observability | OpenTelemetry → Tempo | Full distributed trace correlation |
| CI/CD | GitHub Actions | Reproducible, fast pipeline |

## Performance
- API latency: p95 ~300ms (down from 800ms — 62% reduction)
- Event throughput: 500–1,000 events/min sustained
- All services containerized with Docker Compose

## Services
- `auth-service` — JWT auth, Redis OTP, OAuth2
- `notification-service` — Kafka consumer, email/SMS dispatch
- `portfolio-service` — User portfolio CRUD, paginated APIs
- `workspace-service` — Workspace management
- `api-gateway` — Routing, rate limiting, auth passthrough
- `roadmap-service` — Goal tracking

## Local Setup
```bash
git clone https://github.com/vaishali515/switchboard
cd switchboard
docker-compose up -d
```
