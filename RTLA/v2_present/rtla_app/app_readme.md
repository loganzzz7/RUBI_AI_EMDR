# RTLA Application Structure

This document describes the purpose of each directory and file within the `rtla_app` application.

```
rtla_app/
├── app/
│   ├── config.py
│   ├── database.py
│   ├── main.py
│   ├── models
│   ├── routers
│   ├── schemas
│   └── services
├── app_readme.md
├── data/
├── migrations/
├── requirements.txt
└── scripts/
```

---

## app/

Contains the main RTLA application source code.

### main.py

Application entry point that starts FastAPI and registers all API routes.

### database.py

Creates the PostgreSQL database connection and SQLAlchemy session.

### config.py

Stores application configuration such as database URLs, AWS credentials, and environment variables.

---

## models/

Defines the SQLAlchemy database models.

Each model corresponds to a table in PostgreSQL.

i.e.
- Phrase
- Module
- Review
- PhraseVersion

---

## schemas/

Defines the Pydantic models used for request validation and API responses.

---

## routers/

Defines REST API endpoints.

i.e.
- `/layers`
- `/phrases`
- `/modules`

---

## services/

Contains business logic.

Examples:

- importing phrases
- generating release bundles
- validating metadata
- exporting JSON

---

## scripts/

Utility scripts not a part of the web server.

i.e.
- import JSON datasets
- validate phrase files
- export approved releases
- upload release bundles to S3

---

## data/

Stores JSON datasets before they are imported into PostgreSQL.

i.e.
```
phase_1.json
phase_2.json
phase_3.json
```

---

## migrations/

Database schema history via Alembic.

---

## requirements.txt

Python package dependencies.