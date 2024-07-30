# MyMediaList

```yml
volumes:
    postgres_data:

services:
  api:
    container_name: mymedialist-api
    image: ghcr.io/mymedialist/api:latest
    hostname: api
    depends_on:
      - db
    environment:
      MYMEDIALIST_DB_HOST: db
      MYMEDIALIST_DB_PORT: 5432
      MYMEDIALIST_DB_USER: mymedialist
      MYMEDIALIST_DB_PASSWORD: mymedialist
      MYMEDIALIST_DB_NAME: mymedialist

  frontend:
    container_name: mymedialist-frontend
    image: ghcr.io/mymedialist/frontend:latest
    hostname: frontend
    depends_on:
      - api
    ports:
      - 3000:3000

  db:
    container_name: mymedialist-db
    image: postgres:16
    hostname: db
    environment:
      POSTGRES_DB: mymedialist
      POSTGRES_USER: mymedialist
      POSTGRES_PASSWORD: mymedialist
    volumes:
        - postgres_data:/var/lib/postgresql/data
    expose:
        - 5432
```

