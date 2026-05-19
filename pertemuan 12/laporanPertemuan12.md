# Laporan pertemuan 12 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 10.1 Melihat Penggunaan Memori

<img src="Screenshot 2026-05-19 195957.png" width="70%">

jawaban analisis
1. Persentase Tersedia: 84,2% (1.6GiB / 1.9GiB). Sistem sangat sehat karena jauh di atas ambang batas 10%.
2. Swap: 0B (Used). Kernel tidak memindahkan data ke disk karena RAM masih sangat longgar.
3. Buff/Cache: Sinkron. Nilai 756MiB adalah gabungan dari Buffers (31MB) dan Cached (706MB) untuk efisiensi sistem.

## Studi Kasus 10.1 Server Lambat karena Memori

<img src="Screenshot 2026-05-19 200501.png" width="70%">

jawaban analisis
1. Memori Tersedia: Nilai avail Mem adalah 1609.1 MiB (sekitar 1.6 GB) dari total 2 GB. Ini tidak kecil; sistem masih memiliki banyak cadangan memori dan tidak sedang kekurangan RAM.
2. Penggunaan Swap: Kolom used pada baris Swap adalah 0.0, yang berarti kernel tidak menggunakan swap. Performa server tetap terjaga karena seluruh proses berjalan langsung di RAM fisik.
3. Proses Terbesar (%MEM): Proses dengan %MEM terbesar adalah systemd (PID 1) dengan penggunaan sebesar 0.7%. Karena angkanya sangat kecil, tidak ada proses yang saat ini membebani server atau menyebabkan kelambatan.

## Praktikum 10.2 Mengamati Aktivitas Paging

<img src="Screenshot 2026-05-19 200756.png" width="70%">

jawaban analisis
1. Nilai si (swap-in) dan so (swap-out): Pada kelima baris, nilainya adalah 0. Ini menandakan sistem dalam kondisi normal dan RAM masih sangat mencukupi sehingga tidak ada data yang perlu dipindahkan ke disk.
2. Aktivitas Swap: Karena nilainya tetap 0 secara konsisten, tidak ada aktivitas swap yang terdeteksi. Performa sistem tetap terjaga secara optimal.
3. Memory Pressure: Sistem tidak sedang mengalami memory pressure. Hal ini diperkuat dengan nilai si dan so yang tidak muncul sama sekali di setiap interval waktu pengamatan.
4. Kondisi RAM Keseluruhan:

    - free: Tersedia sekitar 1.031.664 KB (~1 GB) RAM yang benar-benar kosong.

    - buff: Digunakan sekitar 32.168 KB sebagai penyangga operasional sistem.

## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File

<img src="Screenshot 2026-05-19 201948.png" width="70%">

jawaban analisis
1. Nilai Swappiness Default
Nilai Default: Berdasarkan output cat pertama, nilainya adalah 60.

    Arti bagi Kernel: Nilai 60 adalah standar pada Linux. Artinya, kernel akan mulai memindahkan data yang jarang digunakan dari RAM ke Swap secara moderat (tidak terlalu agresif, tapi juga tidak terlalu pasif) untuk menjaga keseimbangan antara performa dan ketersediaan RAM.
2. Perubahan Nilai ke 10

    Ya, pada output cat kedua, nilai sudah berhasil berubah menjadi 10.

    Dengan nilai 10, kernel akan menjadi lebih enggan menggunakan Swap. Kernel akan berusaha memaksimalkan penggunaan RAM fisik sebisa mungkin dan hanya akan menggunakan Swap jika kondisi RAM benar-benar sangat mendesak. Hal ini biasanya dipilih untuk meningkatkan performa pada sistem dengan RAM yang cukup.
3. Status /swapfile-week10
Apakah muncul di swapon --show? Tidak, entri tersebut tidak muncul (output kosong).

    Penyebab: Terjadi kesalahan pada langkah pertama. 

    Solusi: Karena filenya belum pernah terbentuk, perintah chmod, mkswap, dan swapon selanjutnya menghasilkan pesan error "No such file or

## Praktikum 10.4 Monitoring Memory

<img src="Screenshot 2026-05-19 202720.png" width="70%">
<img src="Screenshot 2026-05-19 202655.png" width="70%">

jawaban analisis
1. Proses yang berada di urutan pertama pada output ps aux adalah snapd.

    - %MEM: 2.0%

    - RSS: 40.764 KB
2. Konversi RSS ke MB

    40.764 KB/1024 = 39,8 MB
    
    Analisis Kewajaran: Nilai sekitar 40 MB untuk layanan sistem seperti snapd (pengelola paket Snap di Ubuntu) adalah sangat wajar. Layanan ini bertugas mengelola aplikasi di latar belakang, sehingga penggunaan memori di bawah 50 MB termasuk ringan.
3. VSZ (Virtual Memory Size) selalu lebih besar dari RSS (Resident Set Size) karena alasan berikut:

    VSZ: Mencakup seluruh memori yang bisa diakses oleh proses, termasuk library yang dibagikan (shared libraries), memori yang dialokasikan tapi belum dipakai, dan data yang ada di swap.

    RSS: Hanya mencakup memori fisik (RAM) yang benar-benar sedang digunakan saat ini.

    Analogi sederhananya: VSZ adalah ukuran seluruh lemari buku yang dipesan, sedangkan RSS adalah jumlah buku yang benar-benar sedang Anda baca di atas meja.
4. Ya, urutan tersebut konsisten.

    Di tampilan top, proses systemd (PID 1) terlihat menggunakan 0.7% memori.

    Di tampilan ps aux, systemd berada di urutan bawah dengan nilai yang sama (0.6% - 0.7%).

    Perbedaan kecil pada urutan teratas (seperti munculnya snapd di ps) terjadi karena ps aux memberikan snapshot statis pada saat perintah dijalankan, sementara top diperbarui secara real-time. Namun, secara keseluruhan, data persentase memori di antara keduanya sinkron.

## Praktikum 10.5 Script Monitor Memori

<img src="Screenshot 2026-05-19 203730.png" width="70%">

jawaban analisis
1. Mekanisme: Skrip menggunakan kombinasi free dan awk untuk menghitung rasio memori.

    Detail Kolom: $7 adalah kolom available (memori yang siap digunakan segera) dan $2 adalah total RAM.

    Hasil: Pada gambar, perhitungan menghasilkan 81%. Karena 81 tidak lebih kecil dari 20 (THRESHOLD), maka status yang muncul adalah "(normal)"
2. Analisis Kondisi if
Logika: if [ "$AVAIL" -lt "$THRESHOLD" ]

    Eksekusi: Saat ini $AVAIL (81) dibandingkan dengan 20. Karena 81 tidak kurang dari 20, blok else dijalankan, sehingga pesan peringatan "KRITIS" tidak muncul.
3. Perubahan Output: Status memori akan berubah dari "(normal)" menjadi "(KRITIS)" atau memicu pesan peringatan di dalam blok if.

    Alasan: Nilai memori tersedia saat ini adalah 81%. Secara logika matematika:

    81 < 90 adalah BENAR (True).

    Kesimpulan: Karena persentase tersedia (81%) sekarang berada di bawah ambang batas baru (90%), skrip menganggap sistem dalam keadaan kekurangan memori, meskipun secara riil RAM 1.6 GiB masih sangat mencukupi.

## Studi Kasus 10.2 Gagal Akses File

<img src="Screenshot 2026-05-19 204304.png" width="70%">

jawaban analisis
1. Saat menjalankan perintah chmod 000 app.conf, menghapus seluruh hak akses (read, write, execute) untuk semua pengguna, termasuk kita sendiri sebagai pemilik file.

    Mengapa gagal? Perintah cat memerlukan akses baca (read).

    System Call yang gagal: Saat cat dijalankan, program tersebut memanggil open() system call. Karena bit permission diatur ke 000, kernel menolak permintaan tersebut dan mengembalikan error EACCES (Permission denied) sebelum file sempat dibaca.
2. Kedua error ini terjadi pada tahap yang berbeda dalam proses kernel mencari file:

    Permission denied: File ada, tetapi identitas Anda tidak memiliki kunci (izin) yang cukup untuk membukanya. Kernel memblokir akses di lapisan keamanan.

    No such file or directory: File tidak ditemukan di dalam struktur direktori. Jika Anda melakukan rm app.conf, entri file tersebut dihapus dari inode tabel, sehingga saat cat memanggil open(), kernel melaporkan bahwa target tidak ada.
3. Angka 644 adalah representasi oktal dari hak akses yang dibagi menjadi tiga kelompok (Owner, Group, Others)

## Praktikum 10.6 Mengamati System Call dengan strace

<img src="Screenshot 2026-05-19 204714.png" width="70%">
<img src="Screenshot 2026-05-19 204800.png" width="70%">

jawaban analisis
1. 4 system call yang teridentifikasi beserta fungsinya:

    - openat: Membuka file atau direktori. Terlihat mencoba membuka library sistem seperti libc.so.6.

    - mmap: Memetakan file atau perangkat ke dalam memori. Digunakan untuk memuat isi library ke dalam alamat memori proses agar bisa dieksekusi.

    - read: Membaca data dari file descriptor. Digunakan untuk membaca header file ELF guna memastikan kecocokan arsitektur.

    - close: Menutup file descriptor yang sudah tidak digunakan lagi untuk membebaskan sumber daya.
2. Berdasarkan ringkasan strace -c, mmap adalah yang paling sering dipanggil (18 kali pada perintah pertama).

    Mengapa? Karena setiap kali program ls berjalan, ia harus memuat banyak library pendukung (shared libraries). Setiap library membutuhkan beberapa kali panggilan mmap untuk memetakan bagian teks (kode), data, dan buffer ke dalam memori fisik.
3. Ya, terdapat errors pada beberapa system call (misalnya access, statx, dan arch_prctl).

    Apakah program bermasalah? Tidak, ini adalah bagian normal dari logika program.

    Saat sebuah program berjalan, ia sering kali mencoba mencari library atau file konfigurasi di beberapa lokasi berbeda (search path). Jika tidak ditemukan di lokasi pertama (ENOENT - No such file or directory), kernel mengembalikan error, dan program akan mencoba mencarinya di lokasi berikutnya.
4. Terdapat perbedaan jumlah total system call (dari 80 naik menjadi 115).

    Faktor Penyebab: Perbedaannya terletak pada isi direktori yang dibaca. Direktori /etc memiliki jumlah file dan sub-direktori yang jauh lebih banyak daripada direktori kerja Anda saat ini.

    Dampak: Kernel harus melakukan lebih banyak panggilan getdents64 (untuk membaca entri direktori) dan newfstatat atau statx (untuk mengambil informasi detail/atribut setiap file) agar ls bisa menampilkan daftar lengkapnya.

## 1.6 Tugas Praktikum

### Tugas 10.1 Audit Penggunaan Memori Sistem

<img src="Screenshot 2026-05-19 210248.png" width="70%">

jawaban analisis
1. Persentase Tersedia: 78,9% (1.5GiB / 1.9GiB). Sistem dalam kondisi Sangat Normal karena ketersediaan memori jauh di atas ambang batas 10%.
2. Analisis Buff/Cache: Tidak dihitung sebagai memori terpakai karena kernel dapat menghapus data ini secara instan dan memberikannya ke aplikasi jika dibutuhkan. Fungsinya hanya sebagai percepatan akses disk.
3. Status Swap: SwapTotal = 0 kB dan SwapFree = 0 kB. Artinya,tidak memiliki area Swap yang aktif sama sekali.

### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi

<img src="Screenshot 2026-05-19 210634.png" width="70%">

jawaban analisis
1. Proses Urutan Pertama:

    - Nama Proses: snapd

    - %MEM: 2.0%

    - RSS: 40764 KB
2. Konversi RSS ke MB:

    Perhitungan: 40764 KB/1024 = 39,8 MB
    
    Kewajaran: Sangat wajar. Sebagai layanan sistem pengelola paket Snap di Ubuntu, penggunaan memori sekitar 40 MB tergolong ringan dan normal.
3. Total %MEM 5 Proses Teratas:

    Data: 2.0% (snapd) + 1.8% (fwupd) + 1.3% (multipathd) + 1.0% (unattended-upgr) + 0.9% (networkd-dispa).

    Hasil: 7.0%.

    Analisis: Kelima proses utama tersebut secara bersama-sama hanya menggunakan 7% dari total RAM sistem

### Tugas 10.3 Membuat dan Memverifikasi Swap File

<img src="Screenshot 2026-05-19 211552.png" width="70%">

jawaban analisis
1. Meskipun output perintah tersebut tidak ditampilkan secara eksplisit di screenshot terakhir, berdasarkan perintah yang berhasil dijalankan, kolomnya akan berisi:

    NAME: /swapfile-tugas-week10

    TYPE: file

    SIZE: 256M

    USED: 0B (karena RAM masih sangat longgar).
2. Ya, nilai total pada baris Swap akan bertambah menjadi 256 MiB.
Sebelumnya, pada percobaan pertama(image_406949.png), nilai Swap adalah 0B. Setelah perintah sudo swapon /swapfile-tugas-week10 berhasil dijalankan tanpa error, sistem akan langsung mengenali ruang tambahan tersebut sebagai memori virtual cadangan.
3. Izin akses (permission) sangat krusial untuk file swap karena file ini berisi "salinan" data yang ada di RAM.

    Pentingnya 600 (-rw-------): Izin ini memastikan hanya root yang dapat membaca atau menulis ke file swap.

    Risiko 644 (-rw-r--r--): Jika diatur ke 644, pengguna lain di sistem (Others) dapat membaca isi file swap tersebut. Karena swap menyimpan data aplikasi yang sedang berjalan, informasi sensitif seperti password yang sedang diketik, kunci enkripsi, atau data pribadi pengguna bisa bocor dan dibaca dalam bentuk teks mentah oleh pihak yang tidak berwenang.

### Tugas 10.4 Analisis System Call dengan strace

<img src="Screenshot 2026-05-19 211949.png" width="70%">

jawaban analisis
1. 5 System Call Utama:

    - mmap: Memetakan file ke memori (memuat library).

    - close: Menutup file descriptor yang terbuka.

    - openat: Membuka file atau direktori dengan jalur relatif.

    - read: Membaca konten dari file.

    - write: Menampilkan hasil ke layar/terminal.
2. Paling Sering Dipanggil: mmap (18 kali). Ini karena program perlu memetakan banyak komponen library sistem agar bisa berjalan dengan benar.
3. Analisis Error: Terdapat error pada access, statfs, dan arch_prctl. Hal ini normal karena program sering mencoba mencari file di beberapa lokasi berbeda sebelum menemukan yang tepat. Program tetap berjalan sukses tanpa kendala.

### Tugas 10.5 Studi Kasus Diagnosa Server Lambat

<img src="Screenshot 2026-05-19 212802.png" width="70%">

jawaban analisis
1. Peran Fungsi Skrip:

    cek_memori: Menghitung ketersediaan RAM.

    cek_swap: Memeriksa penggunaan memori virtual.

    cek_proses: Mencari aplikasi paling boros memori.

    cek_paging: Memantau perpindahan data RAM ke disk.

    ringkasan: Menyimpulkan status akhir sistem.

    Tujuan: Pemisahan fungsi dilakukan agar kode lebih terstruktur (modular) dan mudah dikelola.
2. Kondisi Sistem: Normal. Penggunaan RAM masih jauh di bawah ambang batas (tersedia ~80%) dan Swap tidak digunakan sama sekali.
3. tee vs Redirection (>): tee memungkinkan output tampil di layar terminal sekaligus tersimpan di file laporan. Redirection biasa (>) hanya menyimpan ke file tanpa menampilkan apa pun di layar.
4. Aktivitas Paging: Tidak ada (nilai si dan so adalah 0). Implikasinya, performa server sangat cepat karena kernel tidak perlu membuang waktu untuk mengakses disk yang lambat.