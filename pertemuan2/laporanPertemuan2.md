# Laporan pertemuan 2 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 2.1 — Identifikasi CPU dan Memori

### Pertanyaan Percobaan 2.1
1. jumlah CPU(s), core/thread
2. total RAM
3. total swap. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat

### Jawaban Percobaan 2.1 - latihan 2.1
1. 1 CPU (Socket), 1 Core dan 1 Thread
2. total RAM sistem adalah 1.9Gi (sekitar 2 GB)
3. total Swap adalah 2.0Gi (2 GB).
   RAM (Random Access Memory) adalah memori utama yang sangat cepat untuk menyimpan data aplikasi yang sedang berjalan, namun kapasitasnya terbatas. Sedangkan Swap adalah area di hard disk yang digunakan sebagai "cadangan" ketika RAM sudah penuh, namun kecepatannya jauh lebih lambat karena harus mengakses penyimpanan fisik.
<img src="Screenshot 2026-02-18 114651.png" width="70%">
<img src="Screenshot 2026-02-18 114718.png" width="70%">
<img src="Screenshot 2026-02-18 114806.png" width="70%">

## Praktikum 2.2 — Identifikasi Perangkat PCI/USB dan Driver

### Pertanyaan Percobaan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

### Jawaban Percobaan 2.2 - latihan 2.2
Perangkat PCI: Ethernet Controller (NIC)

Vendor:Device ID
8086:100e

Nama perangkat
Intel Corporation 82540EM Gigabit Ethernet Controller

Driver / Kernel module
e1000

Deskripsi fungsi singkat
Perangkat ini adalah kartu jaringan (NIC) yang berfungsi untuk menghubungkan sistem ke jaringan (LAN/internet). Driver e1000 memungkinkan sistem Linux berkomunikasi dengan hardware jaringan tersebut.

<img src="Screenshot 2026-02-18 114806.png" width="70%">

## Praktikum 2.3 — Identifikasi Storage dan Filesystem

<img src="Screenshot 2026-02-18 125149.png" width="70%">

## Praktikum 2.4 — Melihat Modul Aktif dan Informasinya

<img src="Screenshot 2026-02-18 125824.png" width="70%">

## Praktikum 2.5 — Konfigurasi Auto-load dan Blacklist
<img src="Screenshot 2026-02-21 115748.png" width="70%">

## Praktikum 2.6 — Mengenali Block vs Character Device

### Pertanyaan Percobaan 2.6 - latihan 2.3
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan character device! (Hint: karakter pertama pada permission string).

### Jawaban Percobaan 2.6 - latihan 2.3
1. Block Device (/dev/sda)
Penanda: Karakter pertama adalah huruf b.
Artinya: File ini mewakili perangkat keras yang menyimpan dan mengirim data dalam bentuk blok (kumpulan data), contohnya Hard Drive atau SSD.

2. Character Device (/dev/tty)
Penanda: Karakter pertama adalah huruf c.
Artinya: File ini mewakili perangkat yang mengirim data karakter demi karakter secara berurutan, contohnya keyboard, mouse, atau terminal (TTY).

<img src="Screenshot 2026-02-21 120141.png" width="70%">

## Praktikum 2.7 — Melihat Informasi udev

<img src="Screenshot 2026-02-21 120922.png" width="70%">

## Praktikum 2.8 — Membuat Workspace Praktikum

<img src="Screenshot 2026-02-21 121345.png" width="70%">

## Praktikum 2.9 — Pencarian Pola dengan grep

<img src="Screenshot 2026-02-21 213232.png" width="70%">

## Praktikum 2.10 — Substitusi dengan sed (Aman di File Latihan)

<img src="Screenshot 2026-02-21 213640.png" width="70%">

## Praktikum 2.11 — Ekstraksi Kolom dengan awk

<img src="Screenshot 2026-02-21 214002.png" width="70%">

## Praktikum 2.12 — Melihat Proses dengan ps

<img src="Screenshot 2026-02-21 214209.png" width="70%">

## Praktikum 2.13 — Monitoring Real-time dengan top

<img src="Screenshot 2026-02-21 214427.png" width="70%">

## Praktikum 2.14 — Menghentikan Proses dengan kill

<img src="Screenshot 2026-02-21 214746.png" width="70%">

## Praktikum 2.15 — Cek Disk, Load, dan Service

<img src="Screenshot 2026-02-21 215041.png" width="70%">

## Praktikum 2.16 — Monitoring Port dan Koneksi(Network Basics)

### Pertanyaan Percobaan 2.16 - latihan 2.5
Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu
tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut
secara singkat.

### jawaban Percobaan 2.16 - latihan 2.5
Port 22 digunakan oleh layanan SSH (Secure Shell).
Service sshd memungkinkan pengguna untuk:
1. Login ke server secara remote
2. Mengelola server lewat terminal jarak jauh
3. Transfer file secara aman (menggunakan SCP atau SFTP)
Karena berjalan di 0.0.0.0:22, artinya server menerima koneksi SSH dari semua alamat IP yang diizinkan.

<img src="Screenshot 2026-02-21 215152.png" width="70%">

## 1.9 Latihan
### Pertanyaan
### Latihan 2.A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat,
ID vendor:device, dan kernel driver in use.
### Latihan 2.B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan
lsblk -f dan tuliskan tipe filesystem serta UUID-nya.
### Latihan 2.C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO,
WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.
### Latihan 2.D
Gunakan sed untuk mengganti semua kata server menjadi node pada file
latihan. Tunjukkan sebelum dan sesudah.
### Latihan 2.E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk
di atas 70%.
### Latihan 2.F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan
SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.
### Latihan 2.G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service
aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.

### jawaban
### Latihan 2.A
Nama perangkat: Ethernet controller – Intel 82540EM

ID vendor:device: 8086:100e

Kernel driver in use: e1000
### Latihan 2.B
Device root: /dev/mapper/ubuntu--vg-ubuntu--lv

Filesystem type: ext4

UUID: 894433b1-0c34-4f19-a4b5-8dee661eca7d
<img src="Screenshot 2026-02-21 220243.png" width="70%">

### Latihan 2.C
<img src="Screenshot 2026-02-21 220749.png" width="70%">

### Latihan 2.D
<img src="Screenshot 2026-02-21 220913.png" width="70%">

### Latihan 2.E
<img src="Screenshot 2026-02-21 221047.png" width="70%">

### Latihan 2.F
SIGTERM (15) meminta proses berhenti dengan baik

SIGKILL (9) langsung paksa berhenti, tidak bisa ditolak
### Latihan 2.G
<img src="Screenshot 2026-02-21 221249.png" width="70%">
