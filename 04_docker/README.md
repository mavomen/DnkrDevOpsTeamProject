# Stage 4 - Dockerization

## Expected repository layout

The Compose file assumes this layout at the team repository root:

```text
.
├── 03_project_clone/
│   └── multi-service-docker-app/
│       ├── backend/
│       │   ├── app.py
│       │   ├── init.sql
│       │   └── requirements.txt
│       ├── frontend/
│       │   └── index.html
│       └── reverse_proxy/
│           └── default.conf
└── 04_docker/
    ├── docker-compose.yml
    ├── .env
    └── README.md
```

The Dockerfiles and `.dockerignore` files in this bundle are overlay files.
Copy them into the matching service directories inside the upstream project.
The replacement `backend/app.py` and `backend/requirements.txt` are also
provided as safer runtime versions.

## Prepare

1. Resolve the upstream project's license/permission status before copying
   or committing its source files.
2. Place the upstream project at
   `03_project_clone/multi-service-docker-app/`.
3. Copy the files from `03_project_clone_overlay/` into the matching
   directories in that clone, replacing the old Dockerfiles and backend
   runtime files where indicated.
4. Create the local environment file:

   ```bash
   cp 04_docker/.env.example 04_docker/.env
   nano 04_docker/.env
   ```

   Set `POSTGRES_PASSWORD` to a strong unique value. Do not commit `.env`.

## Build and run

From the team repository root:

```bash
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml config
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml build
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml up -d
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml ps
```

Open `http://localhost:8080` (or the configured `APP_PORT`).
The frontend's existing page should display the visit counter.

## Verification

```bash
curl -i http://localhost:8080/
curl -i http://localhost:8080/api/
curl -i http://localhost:8080/api/healthz
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml logs --tail=100
```

Expected:
- `/` serves the frontend HTML.
- `/api/` returns JSON containing the visit count.
- `/api/healthz` returns a healthy response when PostgreSQL is reachable.
- `db`, `backend`, `frontend`, and `reverse_proxy` become healthy.

## Stop / cleanup

```bash
docker compose --env-file 04_docker/.env -f 04_docker/docker-compose.yml down
```

This keeps the named database volume. To intentionally delete the database
data too, use `down -v` (destructive; do not run unless the data is disposable).

## Network design

- `db` is only attached to `backend_net`, which is internal.
- `backend` joins `backend_net` and `proxy_net`.
- `frontend` and `reverse_proxy` join `proxy_net`.
- Only the reverse proxy publishes a host port.
- PostgreSQL has no published host port.
