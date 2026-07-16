# 02 - Install Docker

## Install Docker Engine

CentOS

```bash
dnf install docker docker-compose-plugin
```

Ubuntu

```bash
apt install docker.io docker-compose-plugin
```

---

## Enable Docker

```bash
systemctl enable docker
systemctl start docker
```

---

## Verify

```bash
docker version
docker compose version
```

---

## Create Docker Network

```bash
docker network create backend
```

---

## Test

```bash
docker run hello-world
```

---

## Next

03 network
