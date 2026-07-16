# 04 - Nginx Reverse Proxy

---

## Overview

Nginx is used as a reverse proxy to receive all HTTP and HTTPS requests and then forward them to the Laravel container.

This repository uses a single Nginx container that can serve multiple Laravel applications simultaneously.

---

## Request Flow

Internet

↓

Cloudflare

↓

Nginx

↓

Laravel Container

↓

PHP-FPM

---

## Directory

```
nginx/

default.conf

ssl/

conf.d/

```

---

## Container

```
docker ps
```

> [!NOTE]
> Make sure the nginx container is running.

---

## Test Configuration

```
docker exec nginx nginx -t
```

Output

```
syntax is ok

test is successful
```

---

## Reload

```
docker exec nginx nginx -s reload
```

---

## Verify

```
curl localhost
```

---

## Common Problems

### 502 Bad Gateway

cause

- PHP death

- Container not running

- wrong port

### Permission Denied

check

```
storage/

bootstrap/cache
```

---

## Next

05 SSL
