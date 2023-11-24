# Directus

[Caddy](https://caddyserver.com) as reverse proxy for [Directus](https://directus.io), with [MariaDB](https://mariadb.org) and [phpMyAdmin](https://phpmyadmin.net).

## 🚀 Quick start

Download the `compose.yaml` file:

```bash
curl -O https://raw.githubusercontent.com/gremo/compose-selfhosted/main/src/directus/compose.yaml
```

Create an empty `.env` file to hold environment variables:

```bash
touch .env
```

> [!Tip]
> You can populate secrets in the `.env` file randomly:
>
> ```bash
> {
>  echo "KEY=$(uuidgen -r)"
>  echo "SECRET=$(uuidgen -r)"
>  echo "DB_PASSWORD=$(head /dev/urandom | tr -dc 'A-Za-z0-9@$%&_+' | head -c10)"
>  echo
> } >> .env
> ```

## ⚙️ Environment variables

> [!Important]
> Database root password is random, after starting the project run `docker compose logs | grep -i "GENERATED ROOT PASSWORD"` and note it.

Supported variables:

| Variable         | Required | Default   | Description                         |
| ---------------- | :------: | --------- | ----------------------------------- |
| `DOMAIN`         |          | localhost | The domain name                     |
| `ADMIN_EMAIL`    |    Y     |           | Administrator email                 |
| `ADMIN_PASSWORD` |    Y     |           | Administrator password              |
| `KEY`            |    Y     |           | Unique identifier for the project   |
| `SECRET`         |    Y     |           | Secret string for the project       |
| `DB_USER`        |          | directus  | User for the `DB_NAME` database     |
| `DB_PASSWORD`    |    Y     |           | Password for the `DB_NAME` database |
| `DB_NAME`        |          | directus  | Database name                       |

> [!Note]
> All other [Directus environment variables](https://docs.directus.io/self-hosted/config-options.html#general) are suppoorted too, being `.env` mounted to `/directus/.env`.

## 🌐 Endpoints

```bash
docker compose up -d
```

| Endpoint                      | Service    |
| ----------------------------- | ---------- |
| <http://localhost>            | Directus   |
| <http://localhost/phpmyadmin> | phpMyAdmin |

## 🪄 Tips

A www redirection to non-www can be performed adding the following labels to the `caddy` service:

```yaml
labels:
  caddy: www.${DOMAIN:-localhost}
  caddy.redir: "http://${DOMAIN:-localhost}{uri}"
```
