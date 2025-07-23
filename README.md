# 🛠️ VPS Infrastructure – Deployment & Setup

This repository contains the configuration and structure for hosting multiple Docker-based applications on a Scaleway VPS, including encrypted storage and automated HTTPS with Caddy.

## 🔐 Security & Storage

### Encrypted Disk

Sensitive user data (e.g., databases) is stored on a LUKS-encrypted volume mounted at `/mnt/securedata`.

### SSH Access

Only via public SSH keys.

### Caddy

Provides automatic HTTPS via Let's Encrypt for all exposed services.

## 📁 Server Structure

```bash
/srv
├── apps                # Main apps (API + DB)
│   ├── warden/
│   ├── atlas/
│   ├── iris/
│   └── looter/
├── netdata/            # Monitoring
│   └── docker-compose.yml
└── caddy/              # Reverse proxy + certs
    └── Caddyfile


/mnt/securedata         # Secured data
├── warden/
│   └── db/
├── atlas/
│   ├── upload/
│   └── db/
├── iris/
└── looter/
```

## ⚙️ Services

Each application has its own `docker-compose.yml`, `.env`, and optionally a `Taskfile.yml` for command automation.

### Stack for Warden

- AdonisJs API
- MySQL database (`/mnt/securedata/warden/db`)
- Served via Caddy: `https://sleeved.com/warden`

## 🚀 Manual Deployment Steps

Each service has his own deployement workflow you can setup each of thous by following technic specification.

### For Warden

- [Technic information](https://sleeved.atlassian.net/wiki/spaces/SleevedConception/pages/44400645/WAR+-+Infos+techniques+d+ploiement)
- [Deployement workflow](https://sleeved.atlassian.net/wiki/spaces/SleevedConception/pages/44400662/WAR+-+Workflow+de+d+ploiement)

### For Atlas

‼️ Not concepted yes

### For Iris

‼️ Not concepted yes

### For Looter

‼️ Not concepted yes

## 🛠️ Configure Caddy

Caddy configuration file is located at `/etc/caddy/Caddyfile`.

#### Minimal Caddyfile Example:

```caddy
sleeved.fr {
  root * /srv/landing
  file_server
}
```

## 🌍 DNS Configuration

Set your domain (e.g., via IONOS) to point to the VPS public IP:

```
Type: A
Host: @
Value: 51.15.201.35
```

## 📦 Tools Used

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Caddy](https://caddyserver.com/)
- [Netdata](https://www.netdata.cloud/)
- [cryptsetup + LUKS](https://wiki.archlinux.org/title/Dm-crypt)
