# PostgreSQL & pgAdmin Setup with Docker Compose

This project provides a simple Docker Compose configuration to set up a PostgreSQL database along with pgAdmin, a popular web-based database management tool.

---

## 📁 Project Structure

```
<your-microservice>/
├── docker-compose.yaml
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

* [Docker](https://docs.docker.com/get-docker/) installed
* [Docker Compose](https://docs.docker.com/compose/install/) installed (or Docker Desktop)

### 📦 Setup

1. Save the following `docker-compose.yaml` file in the root directory of your microservice.

```yaml
services:
  postgres:
    container_name: postgres_container
    image: postgres
    environment:
      POSTGRES_USER: username
      POSTGRES_PASSWORD: password
      PGDATA: /data/postgres
    volumes:
      - postgres:/data/postgres
    ports:
      - "5432:5432"
    networks:
      - postgres
    restart: unless-stopped

  pgadmin:
    container_name: pgadmin_container
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: ${PGADMIN_DEFAULT_EMAIL:-pgadmin4@pgadmin.org}
      PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_DEFAULT_PASSWORD:-admin}
      PGADMIN_CONFIG_SERVER_MODE: "False"
    volumes:
      - pgadmin:/var/lib/pgadmin
    ports:
      - "5050:80"
    networks:
      - postgres
    restart: unless-stopped

networks:
  postgres:
    driver: bridge

volumes:
  postgres:
  pgadmin:
```



2. Navigate to the directory containing the `docker-compose.yaml` file.

3. Run the following command:

```bash
docker compose up
```

---

## 🌐 Accessing the Services

* **PostgreSQL:** Accessible on `localhost:5432`
* **pgAdmin:** Open your browser and go to `http://localhost:5050`

  * Email: `admin@admin.com`
  * Password: `admin123`

> In pgAdmin, you can add a new server:
>
> * **Host:** `db`
> * **Port:** `5432`
> * **Username:** `admin`
> * **Password:** `admin123`

---

## 📌 Notes

* Data is persisted using a Docker volume (`pgdata`), so it won't be lost when containers are stopped.
* Customize the environment variables as per your project needs.

---

## 🧹 Cleanup

To stop and remove the containers and volumes:

```bash
docker compose down -v
```

---

## 📚 Resources

* [PostgreSQL Official Docs](https://www.postgresql.org/docs/)
* [pgAdmin Documentation](https://www.pgadmin.org/docs/)
* [Docker Compose Reference](https://docs.docker.com/compose/)

---

Happy Developing! 🎉

---
