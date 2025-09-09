```
postgres:

    image: ${POSTGRES_IMAGE}

    container_name: postgres

    environment:

      POSTGRES_USER: ${POSTGRES_USER}

      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}

      POSTGRES_DB: ${POSTGRES_DB}

    ports:

      - "${POSTGRES_PORT_EXTERNAL}:${POSTGRES_PORT_INTERNAL}"

    volumes:

      - ./postgres/init:/docker-entrypoint-initdb.d

      - ./postgres/postgres_data:/postgresql/data

    restart: unless-stopped
```