# Manual Deployment M03

## Application Path
`/srv/cc-m03`

## Service
`cc-m03.service`

## Backend
`127.0.0.1:8000`

## Public Endpoint
`http://103.193.177.44/`

## Catatan Konfigurasi Spesifik IDCloudHost
- SSH hardening ditulis di `/etc/ssh/sshd_config.d/00-pti2802.conf`
  (bukan `99-`), karena `50-cloud-init.conf` milik provider berisi
  `PasswordAuthentication yes` dan OpenSSH memakai nilai pertama yang terbaca.
- Tidak ada firewall provider yang terpasang; filtering dilakukan oleh UFW.
- Swap 1 GB dibuat di `/swapfile` dan dipersist lewat `/etc/fstab`.

## Update Procedure

```bash
cd /srv/cc-m03
git pull
source .venv/bin/activate
python -m pip install -r requirements.txt
sudo systemctl restart cc-m03
sudo systemctl status cc-m03 --no-pager
curl -fsS http://127.0.0.1:8000/health
curl -fsS http://127.0.0.1/health
```

## Rollback Dasar

```bash
git log --oneline --decorate -10
git checkout m03
sudo systemctl restart cc-m03
git switch main
```
