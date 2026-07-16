# 03 - Docker Network

This project uses a dedicated bridge network to isolate application services.

## Architecture

```

Internet
│
Cloudflare
│
Nginx
│
production-network
├── Laravel
├── MariaDB
├── Redis
└── phpMyAdmin

```

---

## Create Network

```bash
docker network create production
```

---

## Verify

```bash
docker network ls
```

Expected output

```text
backend
bridge
host
none
```

---

## Inspect

```bash
docker network inspect backend
```

---

## Why Dedicated Network?

- Better isolation
- Easier service discovery
- Internal DNS
- Improved security
- Cleaner compose configuration

---

## Next

04 nginx
