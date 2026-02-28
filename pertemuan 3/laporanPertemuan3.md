# Laporan pertemuan 3 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## 1.11 Latihan

### Latihan 3.1
### pertanyaan
Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

### jawaban

<img src="Screenshot 2026-02-28 201513.png" width="70%">

### Latihan 3.2
### pertanyaan
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

### jawaban

<img src="Screenshot 2026-02-28 204055.png" width="70%">

### Latihan 3.3
### pertanyaan
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file

### jawaban

<img src="Screenshot 2026-02-28 204939.png" width="70%">

### Latihan 3.4
### pertanyaan
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file

### jawaban

<img src="Screenshot 2026-02-28 205948.png" width="70%">
<img src="Screenshot 2026-02-28 205959.png" width="70%">

### Latihan 3.5
### pertanyaan
Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry

### jawaban

<img src="Screenshot 2026-02-28 211853.png" width="70%">
