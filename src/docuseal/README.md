# Docuseal

[Caddy](https://caddyserver.com) as reverse proxy for [Docuseal](https://docuseal.co), with [PostgreSQL](https://postgresql.org).

## 🚀 Quick start

Download the `compose.yaml` file:

```bash
curl -O https://raw.githubusercontent.com/gremo/compose-selfhosted/main/src/docuseal/compose.yaml
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
>  echo "DB_PASSWORD=$(head /dev/urandom | tr -dc 'A-Za-z0-9@$%&_+' | head -c10)"
>  echo
> } >> .env
> ```

## ⚙️ Environment variables

Supported variables:

| Variable      | Required | Default   | Description                         |
| ------------- | :------: | --------- | ----------------------------------- |
| `DOMAIN`      |          | localhost | The domain name                     |
| `DB_USER`     |          | docuseal  | User for the `DB_NAME` database     |
| `DB_PASSWORD` |    Y     |           | Password for the `DB_NAME` database |
| `DB_NAME`     |          | docuseal  | Database name                       |

## 🌐 Endpoints

```bash
docker compose up -d
```

| Endpoint           | Service  |
| ------------------ | -------- |
| <http://localhost> | Docuseal |

## 🪄 Tips

A www redirection to non-www can be performed adding the following labels to the `caddy` service:

```yaml
labels:
  caddy: www.${DOMAIN:-localhost}
  caddy.redir: "http://${DOMAIN:-localhost}{uri}"
```
