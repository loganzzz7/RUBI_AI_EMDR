# RTLA v2 Architecture

## Overview

RTLA v2 is the first database-backed version of the Rubi Therapeutic Language Architecture (RTLA).

This version focuses on building a structured clinical knowledge base that can be reviewed, versioned, and exported for use by the local offline SLM. A lightweight web interface allows non-technical persons to browse the database without interacting directly with PostgreSQL.

---

# Technology Stack

| Component | Role |
|-----------|------|
| **GitHub** | Version control for source code, JSON phrase datasets, documentation, and database migrations. |
| **Next.js** | Lightweight frontend used to browse layers, phrases, and phrase metadata. |
| **FastAPI** | Backend REST API that serves data from PostgreSQL to the frontend. |
| **SQLAlchemy** | ORM that allows the application to interact with PostgreSQL using Python objects instead of raw SQL. |
| **Alembic** | Tracks and applies version-controlled database schema changes. |
| **Amazon RDS (PostgreSQL)** | Primary relational database and source of truth for RTLA phrases, modules, metadata, reviews, and versions. |
| **Amazon S3** | Stores approved release bundles (JSON/CSV) for use by the local offline SLM. |
| **Amazon EC2** | Hosts the RTLA application and backend services. |

---

# High-Level Workflow

```text
GitHub JSON
    |
    v
Import Script
    |
    v
Amazon RDS (PostgreSQL)
    |
    v
FastAPI
    |
    v
Next.js
    |
    v
Clinician Review (* proposed)
    |
    v
Approved Release
    |
    v
Amazon S3
    |
    v
Local Offline SLM
```