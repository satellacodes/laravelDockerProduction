# 01 - Server Preparation

## MY VPS

<img src="assets/mySMALLVPS.png" alt="screentshot vps" width="80%"/>

## Requirements

- VPS
- Root access
- Public IP
- Domain name
- Cloudflare

---

## Recommended Specification

| Usage  | CPU    | RAM  | Storage |
| ------ | ------ | ---- | ------- |
| Small  | 1 Core | 2 GB | 40 GB   |
| Medium | 2 Core | 4 GB | 80 GB   |
| Large  | 4 Core | 8 GB | 160 GB  |

---

## Supported OS

- Ubuntu 22.04
- Ubuntu 24.04
- Debian 12
- CentOS Stream 8
- and varian linux distributin

---

## Initial Server Update

```bash
dnf update -y
```

or

```bash
apt update && apt upgrade -y
```

---

## Configure Timezone

```bash
timedatectl set-timezone Asia/Jakarta
```

---

## Create Swap

Example:

```bash
fallocate -l 2G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

---

## Verify

```bash
free -h
```

---

## Next

02 install docker
