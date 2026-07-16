# 05 - SSL Certificate (Cloudflare + acme.sh)

## Overview

This repository uses the Cloudflare DNS Challenge along with acme.sh to obtain an SSL certificate from Let's Encrypt.

This method was chosen because it offers several advantages:

- No need to open port 80 for validation.
- Supports wildcard certificates (\*.example.com).
- Easy to auto-renew.
- Well-suited for Docker and reverse proxy environments.

The generated certificate will be installed in the nginx/ssl directory and then used by the Nginx container.

---

# Architecture

```text
Let's Encrypt
       │
       │ DNS Challenge
       ▼
Cloudflare DNS
       │
       ▼
acme.sh
       │
       ▼
nginx/ssl/
├── fullchain.pem
└── private.pem
       │
       ▼
Nginx Container
```

---

# Prerequisites

Before creating a certificate, ensure:

- The domain is active.
- The domain uses Cloudflare.
- The DNS record points to the VPS.
- The Cloudflare API Token has been generated.
- Port 443 is open on the firewall.

---

# Install acme.sh

Install acme.sh:

```bash
curl https://get.acme.sh | sh
```

source shell:

```bash
source ~/.bashrc
```

Verify

```bash
acme.sh --version
```

---

# Cloudflare API Token

Create an API Token via Cloudflare Dashboard with the following permissions:

- Zone → DNS → Edit
- Zone → Zone → Read

Save the token as an environment variable:

```bash
export CF_Token="YOUR_API_TOKEN"
```

If using Zone ID and Account ID, conform to the official acme.sh documentation.

---

# Generate Certificate

Examples for primary and wildcard domains:

```bash
acme.sh --issue \
--dns dns_cf \
-d example.com \
-d '*.example.com'
```

Once successful, the certificate will be saved in the internal acme.sh directory.

---

# Install Certificate

Copy the certificate to the directory that Nginx uses:

```bash
mkdir -p nginx/ssl
```

then

```bash
acme.sh --install-cert \
-d example.com \
--key-file       nginx/ssl/private.pem \
--fullchain-file nginx/ssl/fullchain.pem
```

directory contents

```text
nginx/
└── ssl/
    ├── private.pem
    └── fullchain.pem
```

---

# Reload Nginx

After the certificate is renewed

```bash
docker exec nginx nginx -t
```

if configuration valid

```bash
docker exec nginx nginx -s reload
```

---

# Automatic Renewal

acme.sh will check the certificate validity period automatically.

To ensure the update process was successful, run:

```bash
acme.sh --renew -d example.com
```

Once the certificate is updated, reload the Nginx container to use the new certificate.

---

# Verify SSL

check using OpenSSL:

```bash
openssl s_client -connect example.com:443
```

or

```bash
curl -Iv https://example.com
```

crosscheck

- Valid certificate.
- No warnings.
- Complete certificate chain.

---

# Troubleshooting

## Certificate Not Found

Make sure the following files are available:

```text
nginx/ssl/private.pem
nginx/ssl/fullchain.pem
```

---

## Permission Denied

Check SSL directory permissions:

```bash
chmod 600 nginx/ssl/private.pem
chmod 644 nginx/ssl/fullchain.pem
```

---

## Nginx Failed to Start

Configuration validation:

```bash
docker exec nginx nginx -t
```

Make sure the certificate path matches the mounted volume.

---

## Cloudflare Authentication Failed

double check

- API Token
- Permission Token
- Domain yang digunakan
- Environment Variable `CF_Token`

---

# Best Practices

- Use DNS Challenge instead of HTTP Challenge for production servers.
- Mount the SSL directory as **read-only**.
- Use a wildcard certificate if serving many subdomains.
- Test the Nginx configuration before reloading.
- Ensure the certificate renewal process is automatic and documented.

---

# Next

06 Laravel
