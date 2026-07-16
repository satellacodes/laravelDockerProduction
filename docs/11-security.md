# 11 Security

## Mengapa Security Penting

This repository was created with basic security practices for production servers in mind. One of the main reasons for this is the experience of dealing with incidents where databases were unauthorized accessed and replaced with ransomware messages due to insecure configurations.

> I was one of the victims :v

This documentation aims to help prevent similar mistakes.

---

## Checklist

- Don't expose MariaDB to internet
- Don't expose Redis
- using firewall
- using long password (i recomendend using generate opensll)
- Disable root login SSH
- use SSH Key
- Update server routine
- Backup auto
- Separate Docker Network
- use HTTPS

---

## MariaDB

> don't

```
3306:3306
```

> yes

```
expose:
  -3306
```

---

## Redis

Never publish a Redis port if it is only used by Laravel applications.

---

## Firewall

only open port

80

443

22

---

## Docker Network

use network internal.

```
docker network create backend
```

---

## Backup

Minimal backup:

- Database
- .env
- Storage
