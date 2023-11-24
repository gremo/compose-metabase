# Uptime Kuma

[Caddy](https://caddyserver.com) as reverse proxy for [Uptime Kuma](https://uptime.kuma.pet).

## 🚀 Quick start

Download the `compose.yaml` file:

```bash
curl -O https://raw.githubusercontent.com/gremo/compose-selfhosted/main/src/uptime-kuma/compose.yaml
```

Create an empty `.env` file to hold environment variables:

```bash
touch .env
```

## ⚙️ Environment variables

Supported variables:

| Variable | Required | Default   | Description     |
| -------- | :------: | --------- | --------------- |
| `DOMAIN` |          | localhost | The domain name |

## 🌐 Endpoints

```bash
docker compose up -d
```

| Endpoint           | Service     |
| ------------------ | ----------- |
| <http://localhost> | Uptime Kuma |

## 🪄 Tips

A www redirection to non-www can be performed adding the following labels to the `caddy` service:

```yaml
labels:
  caddy: www.${DOMAIN:-localhost}
  caddy.redir: "http://${DOMAIN:-localhost}{uri}"
```
