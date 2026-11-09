# Evidence M03 — Catatan

## Informasi VPS
- Provider: IDCloudHost (WestJKT-a / jkt03)
- OS: Ubuntu Server 24.04.5 LTS
- Spesifikasi aktual: 2 vCPU, 2 GB RAM, 20 GB disk
- Spesifikasi modul: 1 vCPU, 1 GB RAM, 20 GB disk
- Public IP: 103.193.177.44
- Hostname: cc-m03-2583207073011

## Provider Firewall
Tab Firewall pada dashboard IDCloudHost tidak memiliki firewall terpasang
(No records). Filtering lalu lintas dilakukan oleh UFW pada host.
Screenshot: provider-firewall.png

## Temuan Troubleshooting 1 — SSH Hardening
File `99-pti2802.conf` (sesuai modul) tidak efektif karena
`50-cloud-init.conf` milik provider berisi `PasswordAuthentication yes`.
OpenSSH memakai nilai pertama yang terbaca, sehingga `sshd -T` masih
menampilkan `passwordauthentication yes`.
Solusi: file diganti nama menjadi `00-pti2802.conf` agar terbaca lebih
dahulu. Setelah itu `sshd -T` menampilkan `passwordauthentication no`.
Verifikasi: login `ucan` dan `root` ditolak (Permission denied (publickey)),
login `cloudstudent` dengan key berhasil.

## Catatan Perbedaan Spesifikasi
VPS memiliki 2 vCPU / 2 GB RAM. Konfigurasi Gunicorn tetap mengikuti modul
(1 worker, 2 thread) untuk menjaga headroom dan konsistensi dengan ADR-0001.
