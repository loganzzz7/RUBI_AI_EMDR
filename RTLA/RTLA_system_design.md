# RTLA Platform Technology Stack

| **Component** | **Role** |
|:--------------|:---------|
| **GitHub** | Version control for source code, infrastructure, documentation, and database migrations. Serves as the central repository for collaborative development. |
| **Next.js** | Frontend web application that provides the user interface for clinicians, researchers, and administrators to manage RTLA content and platform operations. |
| **Nginx** | Reverse proxy and web server that routes incoming HTTPS requests to the appropriate backend services, serves static assets, and manages SSL termination. |
| **FastAPI** | Backend API responsible for authentication, business logic, validation, release generation, integrations, and communication between the frontend and PostgreSQL. |
| **SQLAlchemy** | Object-Relational Mapper (ORM) that maps Python classes to PostgreSQL tables, allowing database interactions through Python instead of raw SQL. |
| **Alembic** | Database schema migration tool that tracks and applies structural changes (tables, columns, indexes, and constraints) to PostgreSQL in a version-controlled and repeatable manner. |
| **Amazon RDS PostgreSQL** | Primary relational database and source of truth for all structured RTLA data, including phrases, modules, versions, reviews, evidence, users, and release metadata. |
| **Amazon S3** | Immutable object storage for published release artifacts such as JSON deployment bundles, CSV exports, clinical reports, evaluation datasets, and archived releases. |
| **Amazon EC2** | Cloud virtual machine that hosts the application stack (Nginx, Next.js, and FastAPI) and manages runtime execution of the platform. |
| **Amazon CloudWatch** | Centralized monitoring, logging, performance metrics, and alerting for application health, API performance, infrastructure utilization, and system diagnostics. |

---

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