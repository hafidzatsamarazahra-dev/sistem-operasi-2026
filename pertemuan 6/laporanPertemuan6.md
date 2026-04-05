# Laporan pertemuan 2 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 6.1 — Melihat Proses dan Thread

### Latihan 6.1

<img src="Screenshot 2026-04-03 200624.png" width="70%">

### pertanyaan
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID
terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang
menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda
lihat?

### jawaban
1. 360,PID terkecil = 1
2. 
<img src="Screenshot 2026-04-03 201436.png" width="70%">

Setelah menjalankan pstree -p, ditemukan bahwa proses bash berada di bawah proses login.

Dengan demikian, proses induk (PPID) dari bash adalah login, karena bash dijalankan setelah proses login berhasil.
3. 
<img src="Screenshot 2026-04-03 200624.png" width="70%">
<img src="Screenshot 2026-04-03 201724.png" width="70%">

ps aux : fokus ke proses
ps aux -L : lebih detail karena menampilkan thread di dalam proses

## Praktikum 6.2 — Mengamati Siklus Hidup Proses

### Latihan 6.2

### pertanyaan
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi
apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit
code masing-masing. Pola apa yang Anda temukan?

### jawaban

1. 
<img src="Screenshot 2026-04-05 113755.png" width="70%">

Statusnya S (sleeping) karena proses hanya menunggu waktu (tidak memakai CPU).

2. 
<img src="Screenshot 2026-04-05 114200.png" width="70%">

Polanya:

0 : sukses
≠ 0 : gagal

Artinya, semua perintah yang berhasil selalu menghasilkan exit code 0, sedangkan yang gagal menghasilkan angka selain 0 .

## Praktikum 6.3 — Mengatur Prioritas Proses

### Latihan 6.3

### pertanyaan
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan
ps.
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa
Linux membatasi hal ini untuk user biasa?

### jawaban
1. 
<img src="Screenshot 2026-04-05 114608.png" width="70%">

Hasil: NI = 5, STAT = SN
Arti: proses berjalan dengan prioritas lebih rendah dan dalam kondisi sleeping

2. 
<img src="Screenshot 2026-04-05 114851.png" width="70%">

Hasil: NI berubah jadi 10
Arti: prioritas makin rendah

3. 
<img src="Screenshot 2026-04-05 114917.png" width="70%">

Hasil: gagal / permission denied
Alasan:
Nilai negatif = prioritas tinggi
Hanya root yang boleh agar sistem tetap stabil dan adil

## Praktikum 6.4 — Mengirim Sinyal ke Proses

### Latihan 6.4

### pertanyaan
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom
STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan
Anda memilih SIGKILL daripada SIGTERM?

### jawaban
1. 
<img src="Screenshot 2026-04-05 115518.png" width="70%">

Proses memasuki status Stopped. Dalam kondisi ini, proses masih ada di memori tetapi tidak dijadwalkan untuk menggunakan CPU sampai ia menerima sinyal untuk melanjutkan.

2. 
<img src="Screenshot 2026-04-05 115621.png" width="70%">

Kolom STAT akan kembali menjadi aktif, yang menandakan proses telah melanjutkan eksekusinya di latar belakang.

3. 
<img src="Screenshot 2026-04-05 115734.png" width="70%">

Pilih SIGKILL hanya jika SIGTERM tidak berhasil menghentikan proses yang macet (hang) atau tidak responsif. 
* SIGTERM: Pilihan pertama (aman & bersih).
* SIGKILL: Pilihan terakhir (paksa & instan).

## Praktikum 6.5 — Manajemen Job Foreground dan Background

### Latihan 6.5

### pertanyaan
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang
ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan
baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .

### jawaban
1. 
<img src="Screenshot 2026-04-05 202053.png" width="70%">

2. <img src="Screenshot 2026-04-05 201822.png" width="70%">
 
3. 
<img src="Screenshot 2026-04-05 201853.png" width="70%"> 

Apakah berjalan dengan baik? Tidak, top tidak dapat berjalan dengan baik di background.

Mengapa? Program top adalah aplikasi interaktif yang membutuhkan akses langsung ke terminal (standard output untuk menampilkan UI dan standard input untuk menerima perintah tombol seperti 'q' atau 'k'). Linux akan secara otomatis menghentikan (suspend) kembali proses interaktif yang mencoba berjalan di latar belakang karena ia tidak memiliki akses ke terminal untuk berinteraksi dengan pengguna.

4. <img src="Screenshot 2026-04-05 201931.png" width="70%">

## Praktikum 6.6 — Pemantauan Proses

### Latihan 6.6

### pertanyaan
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa
informasi ini berguna?
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah.
Tekan F9 dan amati opsi sinyal yang tersedia.

### jawaban
1. 
<img src="Screenshot 2026-04-05 202537.png" width="70%">

Proses yang biasanya muncul: Karena kita sering mengerjakan tugas kuliah, biasanya yang menduduki peringkat atas adalah Firefox/Chrome (apalagi kalau buka banyak tab dokumentasi), MySQL/PostgreSQL (jika layanan database aktif), atau mungkin Java (jika sedang menjalankan tugas pemrograman atau aplikasi seperti LDPlayer)

2. 
<img src="Screenshot 2026-04-05 202843.png" width="70%">

Kegunaan: Ini sangat krusial saat kita melakukan debugging atau optimasi sistem. Kita bisa memantau apakah beban kerja terdistribusi rata ke seluruh CPU atau justru terjadi bottleneck hanya pada satu core saja. Informasi ini membantu kita memastikan bahwa VM yang kita gunakan sudah terkonfigurasi dengan efisien.

3. 
<img src="Screenshot 2026-04-05 203027.png" width="70%">

## 1.8 Latihan

### Latihan 6.A

### pertanyaan
Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa
nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang
dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian
besar proses di sistem berada dalam kondisi ini?

### jawaban
1. 
<img src="Screenshot 2026-04-05 205104.png" width="70%">
Nama Proses: Pada sistem Linux modern (seperti Ubuntu Server yang kamu pakai), proses dengan PID 1 adalah systemd (sebelumnya dikenal sebagai init).

Fungsi: Ia adalah "Ibu dari semua proses" (Parent of all processes).

Inisialisasi: Proses pertama yang dijalankan oleh kernel saat booting.

Manajemen: Bertanggung jawab untuk menjalankan layanan (services), mengelola sistem, dan memastikan proses lain berjalan dengan benar. Jika systemd mati, sistem kamu akan crash (Kernel Panic).

2. 
<img src="Screenshot 2026-04-05 204427.png" width="70%">
Mengapa Root memiliki lebih banyak proses?

Layanan Sistem: root mengelola semua layanan latar belakang (daemons) yang diperlukan agar sistem operasi bisa berfungsi, seperti manajemen jaringan, logging, penjadwalan tugas (cron), dan keamanan.

Hak Akses: Banyak proses inti sistem membutuhkan hak akses tinggi yang hanya dimiliki oleh root untuk berinteraksi langsung dengan hardware. Sedangkan user biasa hanya menjalankan proses yang berkaitan dengan aplikasinya sendiri.

3. 
<img src="Screenshot 2026-04-05 204604.png" width="70%">
Mengapa sebagian besar proses berada dalam kondisi ini?

Efisiensi Sumber Daya: Kondisi S (Interruptible Sleep) berarti proses tersebut sedang "menunggu". Ia menunggu event tertentu (seperti input keyboard dari kamu, data dari jaringan, atau instruksi dari kernel).

Tidak Membebani CPU: Daripada terus-menerus menggunakan CPU saat tidak ada kerjaan (yang akan membuat laptop/server panas), proses akan "tidur". Begitu ada data atau tugas masuk, ia akan segera bangun dan kembali ke status R (Running).

### Latihan 6.B

### pertanyaan
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di
background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan
ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job.
Berapa job yang tersisa?

### jawaban
1. 
<img src="Screenshot 2026-04-05 211835.png" width="70%">

2. 
<img src="Screenshot 2026-04-05 211728.png" width="70%">

3. 
<img src="Screenshot 2026-04-05 211810.png" width="70%">

Job yang tersisa: Ada 3 job (dua dalam kondisi Stopped yaitu top & htop, dan satu Running yaitu sleep 300).

## Latihan 6.C

### pertanyaan
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice
+15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10.
Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim
SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

### jawaban
1. 
<img src="Screenshot 2026-04-05 212437.png" width="70%">

2. 
<img src="Screenshot 2026-04-05 212256.png" width="70%">
Siapa yang lebih diprioritaskan? Proses pertama (NI +10) yang akan lebih diprioritaskan oleh scheduler.

3. 
<img src="Screenshot 2026-04-05 212549.png" width="70%">