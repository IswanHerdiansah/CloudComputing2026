# Requirements

## Problem Statement
Pelajar pemula bahasa Jepang mengalami kesulitan menemukan materi dasar
yang terstruktur dan dapat diakses kapan saja pada konteks belajar mandiri.
Sistem menyediakan platform web NihonGo Dasar yang menampilkan materi dasar
bahasa Jepang secara terpusat sehingga pelajar dapat belajar bertahap dari
satu tempat.

## Target Users
- Pelajar pemula bahasa Jepang (siswa/mahasiswa) yang belajar mandiri.
- Pengelola konten (pengajar atau admin) yang memelihara materi dan
  memastikan layanan berjalan.

## User Need
- Sebagai pelajar pemula, saya ingin melihat daftar materi dasar yang
  berurutan, sehingga saya tahu urutan belajar.
- Sebagai pengelola, saya ingin memeriksa status layanan lewat health
  endpoint, sehingga gangguan cepat diketahui.

## Functional Requirements
| ID | Requirement | Status M03 |
|---|---|---|
| FR-01 | Sistem menampilkan halaman utama. | Selesai |
| FR-02 | Sistem menyediakan health endpoint. | Selesai |
| FR-03 | Sistem menampilkan metadata aplikasi. | Selesai |
| FR-04 | Sistem menampilkan daftar materi dasar bahasa Jepang. | Direncanakan (M05) |

## Non-Functional Requirements
- NFR-01 Backend hanya listen pada loopback.
- NFR-02 Aplikasi dikelola systemd.
- NFR-03 Request publik masuk melalui reverse proxy.
- NFR-04 Secret tidak disimpan pada Git repository.
- NFR-05 Health endpoint mengembalikan HTTP 200 saat sehat.
- NFR-06 Deployment dapat direproduksi dari repository.
- NFR-07 Arsitektur sesuai VPS kecil.

## Scope M03
In scope: repository, requirements, architecture, ADR, baseline Flask app,
SSH hardening dasar, Gunicorn, systemd, Caddy, HTTP public deployment.

Out of scope: database production, Docker, Infrastructure as Code, CI/CD,
TLS/domain production, horizontal scaling, monitoring stack penuh.
Fitur pembelajaran (materi, kuis, progres) dikembangkan pada milestone
berikutnya.

## Constraints
- Spesifikasi modul: 1 vCPU, 1 GB RAM, 20 GB disk
- Spesifikasi aktual: 2 vCPU, 2 GB RAM, 20 GB disk (IDCloudHost)
- Ubuntu Server 24.04
- Public IPv4

## Acceptance Criteria M03
- [x] first deployment accessible (http://103.193.177.44/)
- [x] health endpoint works (GET /health mengembalikan 200)
- [x] backend loopback-only (127.0.0.1:8000)
- [x] SSH key-only, root login disabled
- [x] UFW active
