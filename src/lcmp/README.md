# LCMP

LCMP stack with [Caddy](https://caddyserver.com) as web server and [PHP](https://php.net) FPM, with [MariaDB](https://mariadb.org) and [phpMyAdmin](https://phpmyadmin.net).

## 🚀 Quick start

Download the `compose.yaml` file:

```bash
curl -O https://raw.githubusercontent.com/gremo/compose-selfhosted/main/src/lcmp/compose.yaml
```

Create an empty `.env` file to hold environment variables:

```bash
touch .env
```

Create a test script in the `public/` directory:

```bash
mkdir public && echo "<?php phpinfo()" > public/index.php
```

> [!Tip]
> You can populate secrets in the `.env` file randomly:
>
> ```bash
> {
>  echo "DB_PASSWORD=$(head /dev/urandom | tr -dc 'A-Za-z0-9@$%&_+' | head -c10)"
>  echo
> } >> .env
> ```

## ⚙️ Environment variables

> [!Important]
> Database root password is random, after starting the project run `docker compose logs | grep -i "GENERATED ROOT PASSWORD"` and note it.

Supported variables:

| Variable      | Required | Default   | Description                         |
| ------------- | :------: | --------- | ----------------------------------- |
| `DOMAIN`      |          | localhost | The domain name                     |
| `DB_USER`     |          | php       | User for the `DB_NAME` database     |
| `DB_PASSWORD` |    Y     |           | Password for the `DB_NAME` database |
| `DB_NAME`     |          | app       | Database name                       |

## 🌐 Endpoints

```bash
docker compose up -d
```

| Endpoint                      | Service    |
| ----------------------------- | ---------- |
| <http://localhost>            | PHP-FPM    |
| <http://localhost/phpmyadmin> | phpMyAdmin |

## 🪄 Tips

A www redirection to non-www can be performed adding the following labels to the `caddy` service:

```yaml
labels:
  caddy: www.${DOMAIN:-localhost}
  caddy.redir: "http://${DOMAIN:-localhost}{uri}"
```
