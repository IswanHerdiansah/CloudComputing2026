# ADR-0001: Initial VPS Deployment Architecture

## Status
Accepted

## Context
VPS IDCloudHost, Ubuntu Server 24.04, public IPv4. Spesifikasi modul
1 vCPU / 1 GB RAM / 20 GB disk; spesifikasi aktual 2 vCPU / 2 GB RAM.
Proyek memerlukan deployment publik yang aman, ringan, dan reproduktif.

## Decision
- Flask sebagai web framework
- Gunicorn 1 worker, 2 thread, bind 127.0.0.1:8000
- systemd untuk manajemen proses
- Caddy sebagai reverse proxy publik di port 80
- UFW sebagai host firewall
- GitHub sebagai single source of truth, deploy key per repository

## Alternatives
1. Node.js + PM2
2. NGINX + Gunicorn
3. Docker
4. PHP-FPM

## Rationale
- Python 3.12 adalah default Ubuntu 24.04, tanpa runtime tambahan.
- Gunicorn pada loopback membuat Caddy satu-satunya entry point publik.
- Caddy memiliki konfigurasi singkat dan siap HTTPS otomatis pada M04.
- systemd native pada Ubuntu, memberi auto-restart dan start saat boot.
- Docker ditunda karena containerization adalah capaian M06.
- NGINX valid, tetapi Caddy lebih sederhana untuk transisi ke HTTPS.

## Consequences
### Positive
- Footprint kecil dan konfigurasi mudah dibaca.
- Backend tidak terekspos langsung ke internet.
- Jalur HTTPS pada M04 hanya perubahan Caddyfile.
### Negative
- Single VPS: tanpa redundansi.
- Deployment masih manual (git pull dan restart service).
- Hanya HTTP pada M03.

## Review Trigger
Review pada M06/M07.
