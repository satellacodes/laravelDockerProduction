# 12 - Monitoring

## Overview

Monitoring is the process of monitoring the condition of servers, applications, and all running services to ensure the system remains stable, secure, and performs well.

In a production environment, monitoring should be carried out periodically to ensure:

- The server has sufficient resources.
- All containers are running normally.
- The database remains responsive.
- Redis is not experiencing any issues.
- Nginx is able to serve requests.
- Laravel is not producing recurring errors.
- SSL is still active.
- The backup was successfully created.

Good monitoring can help detect problems before they cause downtime.

---

# Monitoring Checklist

## Daily

- Docker Container running
- Laravel accessible
- Nginx running normally
- MariaDB running
- Redis running
- Queue Worker active
- Scheduler active
- SSL still valid
- Backup successful
- Disk not full

---

## Weekly

- Cleaning up unused Docker images
- Checking error logs
- Ensuring backup restores are possible
- Deleting unused containers
- Checking for package updates

---

## Monthly

- Update Operating System
- Update Docker Engine
- Update Docker Compose
- Update Base Image
- Audit Firewall
- Audit Docker Network
- Audit User SSH
- Rotasi Password Database

---

# 1. System Resource

## CPU Load

```bash
uptime
```

---

# 2. Memory

Look RAM used.

```bash
free -h
```

---

# 3. Disk Usage

# 4. Disk I/O

.

---

# 5. Docker Monitoring

## Status Container

```bash
docker ps
```

## Docker Logs

```bash
docker compose logs
```

Realtime:

```bash
docker compose logs -f
```

Container specific:

```bash
docker compose logs nginx
```

or

```bash
docker compose logs app
```

---

# 6. Nginx

Validate configuration.

```bash
docker exec nginx nginx -t
```

Output hope:

```text
syntax is ok
test is successful
```

Reload configuration.

```bash
docker exec nginx nginx -s reload
```

see access log.

```bash
tail -f /var/log/nginx/access.log
```

see error log.

```bash
tail -f /var/log/nginx/error.log
```

The error log is the first place to check if a 502 Bad Gateway or 504 Gateway Timeout occurs.

---

# 7. Laravel

Enter the application container.

```bash
docker exec -it app bash
```

View the scheduler list.

```bash
php artisan schedule:list
```

Ensure environment configuration.

```bash
php artisan about
```

see cache.

```bash
php artisan optimize
```

see log Laravel.

```bash
tail -f storage/logs/laravel.log
```

Recurring errors need to be addressed immediately as they can be an indication of an application problem.

---

# 8. Queue Worker

---

# 9. Redis

Entering in Redis.

```bash
docker exec -it redis redis-cli
```

Ping server.

```bash
PING
```

Output:

```text
PONG
```

See information Redis.

```bash
INFO
```

- used_memory
- connected_clients
- uptime

---

# 10. MariaDB

Entering container.

```bash
docker exec -it mariadb bash
```

See status.

```bash
mysqladmin status
```

Entering database.

```bash
mysql -u root -p
```

see size database.

```sql
SHOW DATABASES;
```

Make sure to backup regularly before making major changes.

---

# 11. SSL

Ensure the certificate is still valid.

```bash
openssl s_client -connect domain.com:443
```

atau

```bash
curl -Iv https://domain.com
```

Check the certificate expiration date.

---

# 12. Network

View the ports currently in use.

```bash
ss -tulpn
```

Make sure only the necessary ports are open to the public.

---

# 13. Security Monitoring

View last login.

```bash
last
```

```bash
journalctl -u sshd
```

check firewall.

```bash
firewall-cmd --list-all
```

Make sure only absolutely necessary ports are allowed.

---

# 14. Backup Verification

Make sure the backup file is available.

Contoh:

```text
backup/
├── database.sql.gz
├── storage.tar.gz
└── env.backup
```

Test the restore process regularly. Backups that haven't been restored may not be usable when needed.

---

# Next

➡ **14 - Troubleshooting**
