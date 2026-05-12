# Laporan pertemuan 11 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 9.1 — Permissions

<img src="Screenshot 2026-05-06 105546.png" width="70%">
<img src="Screenshot 2026-05-06 105625.png" width="70%">

Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?

Tantangan

Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan
perubahan output ls -l sebelum dan sesudahnya.

jawaban
1. Karena chmod 600 → -rw-------
    Hanya owner yang punya akses, group & others = 0 izin.
2. - 600 : -rw------- → hanya owner (privat)
    - 755 : -rwxr-xr-x → semua bisa baca & execute, hanya owner bisa edit
3. Default file = 666
    666 - 027 = 640 : -rw-r-----
    Others tidak dapat akses

tantangan

<img src="Screenshot 2026-05-06 110846.png" width="70%">

- Kolom owner berubah: hafidza : root
- Kolom group berubah: hafidza : root
- Permission (rw-r-----) tidak berubah

## Praktikum 9.2 — ACL

<img src="Screenshot 2026-05-06 112014.png" width="70%">
<img src="Screenshot 2026-05-06 112058.png" width="70%">

Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?

Tantangan

Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah
itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.

jawaban
1. Karena belum ada ACL tambahan.
File masih pakai permission biasa (chmod), jadi hanya:

    - owner
    - group
    - others
2. - ls -l:Ada tanda + artinya ada ACL tambahan
    - getfacl:Menampilkan detail ACL yang tidak terlihat di ls -l
3. -d = default ACL (warisan)

    Jadi setiap file baru di folder shared otomatis ikut rule itu.

tantangan

<img src="Screenshot 2026-05-06 112058.png" width="70%">

- Tidak ada user:userA
- Ada group:readonly-group:r--

## Praktikum 9.3A — Membuat dan Mengelola User

<img src="Screenshot 2026-05-06 114215.png" width="70%">

Pertanyaan:
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
2. Bagaimana status passwd -S userB berubah saat akun di-lock?

jawaban
1. perbedaannya: daftar groups bertambah (userA masuk group baru)
2. - P = Password aktif (bisa login)
    - L = Locked (tidak bisa login pakai password)

## Praktikum 9.3B — Group Management

<img src="Screenshot 2026-05-06 115107.png" width="70%">

Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?
2. Mengapa -a pada usermod -aG penting?

jawaban
1. - id userA
    Menampilkan UID, GID, dan semua group
    - groups userA
    Hanya menampilkan nama group saja
2. -a = append (menambahkan),Dengan -a Group lama tetap ada, ditambah group baru,-a itu penting supaya tidak menghapus group sebelumnya.

## Praktikum 9.3C — Password Aging Policy

<img src="Screenshot 2026-05-12 125917.png" width="70%">

Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?

jawaban
1. - Last password change: Terakhir ganti password (6 Mei 2026).

    - Password expires: Tanggal wajib ganti password (5 Juli 2026).

    - Min/Max days: Jeda minimal (1 hari) dan maksimal (60 hari) antar penggantian password.

    - Warning: Peringatan muncul 7 hari sebelum kedaluwarsa.
2. - Huruf L (Locked): Akun terkunci (hasil dari passwd -l).

    - Huruf P (Password): Akun aktif/bisa digunakan (hasil dari passwd -u).
3. Keduanya berfungsi memaksa user ganti password saat login berikutnya.

    - chage -d 0: Mengubah tanggal "last change" ke angka 0 (1 Jan 1970) agar sistem menganggap password sudah sangat usang.

    - passwd -e: Cara instan (shortcut) untuk langsung membuat password kedaluwarsa (expire).

## Praktikum 9.4 — Konfigurasi sudo

<img src="Screenshot 2026-05-12 131247.png" width="70%">

Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
3. Informasi apa saja yang dicatat di log sudo?

jawaban
1. Menyimpan aturan di direktori /etc/sudoers.d/ adalah best practice karena:

    - Modularitas: Memudahkan pengelolaan. Anda bisa menghapus akses user cukup dengan menghapus satu file saja tanpa menyentuh konfigurasi utama.

    - Keamanan: Mengurangi risiko kesalahan sintaks pada file utama /etc/sudoers yang bisa menyebabkan seluruh sistem kehilangan akses sudo.

    - Update Sistem: File konfigurasi utama tidak akan tertimpa atau konflik saat ada pembaruan paket sistem operasi.
2. Semua perintah di log itu masih perlu password (autentikasi).

    Buktinya: Di screenshot pertama, saat kamu ketik sudo chage..., sistem langsung minta [sudo] password for hafidza
3. Timestamp: Waktu kejadian (contoh: May 12 05:57:22).

    - Hostname: Nama server (ubuntu-server-lab).

    - User Asal: User yang menjalankan perintah (hafidza).

    - Terminal (TTY): Jalur akses yang digunakan (tty1 untuk login fisik/lokal atau pts/0 untuk SSH/remote).

    - Working Directory (PWD): Lokasi folder saat perintah dijalankan (/home/hafidza).

    - Target User: Identitas user yang dipinjam (USER=root).

    - Command (COMMAND): Perintah lengkap yang dijalankan (contoh: /usr/bin/chage -l userA).

## Praktikum 9.5 — Disk Quota

<img src="Screenshot 2026-05-12 132117.png" width="70%">

Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?

jawaban
1. - Soft Limit: Merupakan ambang batas peringatan.masih diizinkan menulis data ke disk, namun akan menerima notifikasi bahwa kuota hampir habis. Terdapat masa tenggang (grace period) sebelum pembatasan menjadi absolut.

    - Hard Limit: Merupakan batas maksimal yang bersifat mutlak. Sistem akan langsung menghentikan proses penulisan data (write) apabila angka ini tercapai, sehingga tidak ada data tambahan yang dapat disimpan.
2. Penggunaan file .img yang dimuat sebagai loopback bertujuan untuk:

    - Isolasi Risiko: Menghindari risiko sistem utama crash atau hang jika terjadi kesalahan konfigurasi kuota pada partisi root atau /home.

    - Efisiensi Praktikum: Memungkinkan simulasi manajemen kuota dalam skala kecil (misalnya 100MB sesuai perintah dd Anda) tanpa perlu melakukan partisi ulang pada hard drive fisik.
3. Perintah repquota -a menampilkan tabel yang berisi daftar pengguna (seperti userA).

    - Terdapat nilai statistik pada kolom used (kapasitas terpakai), serta kolom soft dan hard yang telah terkonfigurasi (tidak bernilai 0).

    - Munculnya status masa tenggang pada kolom grace apabila penggunaan data telah melewati soft limit.

## Latihan Latihan 9.A — Audit dan Kolaborasi

<img src="Screenshot 2026-05-12 132639.png" width="70%">
<img src="Screenshot 2026-05-12 132706.png" width="70%">
<img src="Screenshot 2026-05-12 132851.png" width="70%">

## Latihan Latihan 9.B — Kebijakan Akun dan Quota

<img src="Screenshot 2026-05-12 133249.png" width="70%">
<img src="Screenshot 2026-05-12 133410.png" width="70%">