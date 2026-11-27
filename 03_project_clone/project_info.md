# Project Information

## Project Source
- Repository: https://github.com/nasser-tarek/multi-service-docker-app
- Default branch: `main`

## Description
A simple multi-service web application consisting of a static frontend, a Flask backend, a PostgreSQL database, and an Nginx reverse proxy.

## Technologies
- Frontend: HTML, Nginx
- Backend: Python, Flask
- Database: PostgreSQL 15
- Containerization: Docker and Docker Compose
- Reverse Proxy: Nginx

## Original Backend Dependencies
The original repository contains a `requirements.txt` file. The dependencies in the adapted Stage 4 implementation are:

```text
Flask==3.1.1
gunicorn==23.0.0
psycopg2-binary==2.9.10
```

## Services and Ports

| Service | Internal Port |
|---|---:|
| Frontend | 80 |
| Backend | 5000 |
| PostgreSQL | 5432 |
| Reverse Proxy | 80 |

The original README documents access through host port `8080`.

## Original Configuration
The original Docker Compose file defines the following PostgreSQL environment variables:

- `POSTGRES_USER`
- `POSTGRES_PASSWORD`
- `POSTGRES_DB`

The original backend uses the database service name `db` and contains database connection defaults in its application code.

## Database
PostgreSQL stores the application visit counter. The `backend/init.sql` file initializes the database table.

## Docker Configuration
The original repository includes Dockerfiles, a Docker Compose configuration, and an Nginx reverse proxy configuration. These files were inspected and later adapted during Stage 4.

## Stage 4 Adaptations
The Stage 4 implementation introduces configurable database connection variables:

- `DB_HOST`
- `DB_PORT`
- `DB_NAME`
- `DB_USER`
- `DB_PASSWORD`

It also uses pinned Python dependencies, health checks, service dependencies, and an external host port mapping through the reverse proxy. These are adaptations, not claims about the original repository.

## License Information
No LICENSE file was found in the cloned repository, and GitHub reports no detected license. Redistribution permissions have therefore not been established.

## Inspection Summary
The project is suitable for Docker practice because it contains multiple services, a database, internal networking, and an Nginx reverse proxy.
