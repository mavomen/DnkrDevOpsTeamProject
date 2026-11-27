# Dockerfile decisions

- Backend uses a slim Python runtime and installs pinned Python dependencies.
- Gunicorn runs the Flask application; Flask's development server and debug mode
  are not used in the container.
- Frontend and reverse proxy use the small official Nginx Alpine image.
- Each service has its own build context, keeping unrelated files out of images.
- `.dockerignore` files exclude caches, local secrets, Git metadata and generated files.
