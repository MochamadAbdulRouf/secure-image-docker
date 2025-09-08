# Disini saya mempraktekkan sebuah mini project buatan saya dengan tema materi Security & Optimization Docker image 

## Skenario Proyek
Kita akan mengambil aplikasi Node.js API yang sudah familier, Tetapi kali ini kita akan fokus untuk membuatnya sekecil dan seaman mungkin. Kita akan melalui beberapa fase:

1. Baseline Membuat Dockerfile yang umum, yang berfungsi tapi tidak aman
2. Audit Memindai image ini menggunakan `Trivy` untuk menemukan celah keamanan
3. Hardening Menulis ulang Dockerfile dengan best pratices keamanan: non-root user, multi-stage build, dan minimal base image  
4. Verifikasi memindai ulang image yang sudah aman dan membandingkan hasilnya

```bash
docker build -t myapi:1.0 -f Dockerfile.v1 .

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
aquasec/trivy:latest \
--timeout 10m \
image myapi:1.0

![Hasil scan trivy untuk Docker v.1.0](image/docker-security%201.0.png)

### Image versi 2.0 yang aman dan membandingkannya 

```bash
docker build -t myapi:2.0 .

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
aquasec/trivy:latest \
--timeout 10m \
image myapi:2.0

![Hasil scan trivy untuk Docker v.1.0](image/docker%20security%202.0.png)
![Hasil scan trivy untuk Docker v.1.0](image/docker%20security%202.0%20v2%20.png)
