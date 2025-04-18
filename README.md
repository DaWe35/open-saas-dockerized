# Open SaaS dockerized

## Prerequisites
- Docker
- Docker Compose

## Setup
1. Clone the repository
2. Run setup and start development environment. This will create a new myapp folder and migrate the database, if the myapp folder is not present:
```bash
docker compose -f docker-compose.dev.yml up -d
```

3. See logs:
```bash
docker compose logs -f
```

The application will be available at [http://localhost:3000](http://localhost:3000) (you can change this port in the `.env` file `APP_PORT` variable)

## Database migration

Run this after you changed the prisma database schema.

```bash
docker compose -f docker-compose.migrate.yml up
```

## Deploy
Build:
```bash
docker compose -f docker-compose.build.yml up
```
Host:
```bash
docker compose -f docker-compose.prod.yml up
```

## Database Backup

To backup the PostgreSQL database, you can use the following command:

```bash
docker exec wasp-db pg_dump -U postgres postgres > backup_$(date +%Y%m%d_%H%M%S).sql
```

This command will:
1. Execute `pg_dump` inside the `wasp-db` container
2. Connect as the `postgres` user
3. Dump the `postgres` database
4. Save the output to a file named `backup_YYYYMMDD_HHMMSS.sql` in your current directory

To restore from a backup:

```bash
docker exec -i wasp-db psql -U postgres postgres < your_backup_file.sql
```
