# High-Level Architecture

```text
                           GitHub
                              │
                              ▼
                          Amazon EC2
                    ┌────────────────────┐
                    │       Nginx        │
                    │--------------------│
                    │      Next.js       │
                    │--------------------│
                    │      FastAPI       │
                    └─────────┬──────────┘
                              │
                              ▼
                         SQLAlchemy
                              │
                              ▼
                           Alembic
                              │
                              ▼
                  Amazon RDS PostgreSQL
                              │
             ┌────────────────┴────────────────┐
             │                                 │
             ▼                                 ▼
      Amazon S3                          Amazon CloudWatch
  (Release approved                  (Monitoring, Logs,
   JSON)                              Metrics, Alerts,
                                      Performance)
```