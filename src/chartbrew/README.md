# Chartbrew

[Caddy](https://caddyserver.com) as reverse proxy for [Chartbrew](https://chartbrew.com), with [MariaDB](https://mariadb.org) and [phpMyAdmin](https://phpmyadmin.net).

## 🚀 Quick start

Download the `compose.yaml` file:

```bash
curl -O https://raw.githubusercontent.com/gremo/compose-selfhosted/main/src/chartbrew/compose.yaml
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
>  echo "SECRET=$(uuidgen -r)"
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
| `SECRET`      |    Y     |           | Secret string for the project       |
| `DB_USER`     |          | chartbrew | User for the `DB_NAME` database     |
| `DB_PASSWORD` |    Y     |           | Password for the `DB_NAME` database |
| `DB_NAME`     |          | chartbrew | Database name                       |

> [!Note]
> All other [Chartbrew environment variables](https://docs.chartbrew.com/#environmental-variables) are suppoorted too, being `.env` mounted to `/code/.env`.

## 🌐 Endpoints

```bash
docker compose up -d
```

| Endpoint                      | Service    |
| ----------------------------- | ---------- |
| <http://localhost>            | Chartbew   |
| <http://localhost/phpmyadmin> | phpMyAdmin |

## 🪄 Tips

A www redirection to non-www can be performed adding the following labels to the `caddy` service:

```yaml
labels:
  caddy: www.${DOMAIN:-localhost}
  caddy.redir: "http://${DOMAIN:-localhost}{uri}"
```
