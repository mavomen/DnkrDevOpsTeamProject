# Compose decisions

- Four services: PostgreSQL, Flask backend, static frontend and Nginx reverse proxy.
- PostgreSQL data persists in the named `db_data` volume.
- PostgreSQL initialization SQL is mounted read-only.
- Database credentials are supplied through an untracked `.env` file.
- `depends_on` with `service_healthy` gates dependent startup on health checks.
- The database is not exposed to the host.
- Only Nginx publishes a host port (default `8080`).
- `backend_net` is internal; `proxy_net` connects the app-facing services.
- Services use `unless-stopped` restart policies.
