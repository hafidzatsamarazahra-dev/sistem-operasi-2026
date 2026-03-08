# Laporan pertemuan 2 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## TUGAS PENDAHULUAN:

### pertanyaan
Jawablah pertanyaan-pertanyaan di bawah ini :
1.	Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.
2.	Apa yang dimaksud perintah-perintah manipulasi file :	cp, mv dan rm (sertakan format yang digunakan)
3.	Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link
(indirect).
4.	Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

### jawaban
1. - pwd:Menampilkan direktori aktif saat ini.

    - cd:Berpindah direktori.

    - mkdir:Membuat direktori baru.

    - rmdir:Menghapus direktori kosong.
2. - cp untuk Menyalin file/folder.

        Format: cp sumber tujuan

   - mv untuk Memindahkan / mengganti nama file.

        Format: mv sumber tujuan

    - rm untuk Menghapus file/folder.

        Format: rm nama_file
3. - Hard Link : Terhubung langsung ke data file asli. Jika file asli dihapus, link masih bisa digunakan. Tidak bisa lintas partisi.

   - Soft Link : Shortcut ke file asli. Jika file asli dihapus, link rusak. Bisa lintas partisi.
4. - file : Menampilkan tipe file.

    - find : Mencari file berdasarkan lokasi/kriteria.

    - which : Menampilkan lokasi program.

    - locate : Mencari file dengan database sistem.

    - grep : Mencari teks dalam file.

## PERCOBAAN:

### pertanyaan
1.	Login sebagai user.
2.	Bukalah Console Terminal dan lakukan percobaan-percobaan di bawah ini. Perhatikan hasilnya.
3.	Selesaikan soal-soal latihan

### jawaban Percobaan 1 : Direktory
1. 
<img src="Screenshot 2026-03-07 195851.png" width="70%">

2. 
<img src="Screenshot 2026-03-07 200013.png" width="70%">

3. 
<img src="Screenshot 2026-03-07 200347.png" width="70%">

4. 
<img src="Screenshot 2026-03-07 195558.png" width="70%">

Alasannya:
Direktori B tidak kosong, sehingga rmdir tidak bisa menghapusnya.

<img src="Screenshot 2026-03-07 200711.png" width="70%">
<img src="Screenshot 2026-03-07 200624.png" width="70%">
<img src="Screenshot 2026-03-07 200651.png" width="70%">

5. 
<img src="Screenshot 2026-03-07 201147.png" width="70%">

Kesimpulan penyebab error:

 -Path direktori salah penulisan

 -Struktur direktori tidak sesuai dengan yang ada di sistem

 -Linux sangat sensitif terhadap penulisan path

### jawaban Percobaan 2 : Manipulasi file
1. 
<img src="Screenshot 2026-03-07 201610.png" width="70%">

2. 
<img src="Screenshot 2026-03-07 201917.png" width="70%">

3. 
<img src="Screenshot 2026-03-07 204933.png" width="70%">

### jawaban Percobaan 3 : Symbolic Link

<img src="Screenshot 2026-03-07 205219.png" width="70%">
<img src="Screenshot 2026-03-07 205411.png" width="70%">

### jawaban Percobaan 4 : Melihat Isi File

<img src="Screenshot 2026-03-07 205610.png" width="70%">

### jawaban Percobaan 5 : Mencari file

<img src="Screenshot 2026-03-07 205916.png" width="70%">

### jawaban Percobaan 6 : Mencari text pada file

<img src="Screenshot 2026-03-07 205942.png" width="70%">

## LATIHAN:
1. 
<img src="Screenshot 2026-03-08 134710.png" width="70%">
<img src="Screenshot 2026-03-08 134847.png" width="70%">
<img src="Screenshot 2026-03-08 134908.png" width="70%">
<img src="Screenshot 2026-03-08 134926.png" width="70%">
<img src="Screenshot 2026-03-08 135002.png" width="70%">
<img src="Screenshot 2026-03-08 135018.png" width="70%">

2. 
<img src="Screenshot 2026-03-08 135316.png" width="70%">
<img src="Screenshot 2026-03-08 135337.png" width="70%">
<img src="Screenshot 2026-03-08 135352.png" width="70%">
<img src="Screenshot 2026-03-08 135448.png" width="70%">

3. 
<img src="Screenshot 2026-03-08 135817.png" width="70%">

4. 
<img src="Screenshot 2026-03-08 135916.png" width="70%">
<img src="Screenshot 2026-03-08 135927.png" width="70%">
<img src="Screenshot 2026-03-08 135940.png" width="70%">
<img src="Screenshot 2026-03-08 140018.png" width="70%">

5-15.
<img src="Screenshot 2026-03-08 140626.png" width="70%">

## LAPORAN RESMI:

1. Analisa Hasil Percobaan

    a. Analisa hasil tampilan
        Pada praktikum ini digunakan perintah dasar Linux seperti cd, ls, pwd, cat, mkdir, rmdir, cp, mv, ln, dan rm untuk menelusuri struktur file system.
        Perintah pwd menampilkan direktori aktif, ls menampilkan isi direktori, dan cd digunakan untuk berpindah direktori.
        Perintah cat menampilkan isi file, mkdir membuat direktori baru, cp menyalin file, mv memindahkan file, dan rm menghapus file atau direktori.
        Dari percobaan ini dapat dipahami bahwa sistem file Linux berbentuk hierarki yang dimulai dari root (/).
    b. Pohon struktur file dan direktori
        /

        ├── bin
        
        ├── boot
        
        ├── dev
        
        ├── etc
        
        ├── home
        
        │   └── user
        
        │       ├── play
        
        │       └── work
        
        ├── proc
        
        ├── sbin
        
        ├── tmp
        
        └── usr
        
            └── bin
    c. Pesan error
        Error dapat terjadi karena:

        -Permission denied : tidak memiliki izin akses.

        -No such file or directory : file atau direktori tidak ditemukan.

        -Directory not empty : direktori tidak bisa dihapus karena masih berisi file.

2. Analisa Latihan
    Pada latihan dilakukan navigasi direktori, melihat isi file sistem, membuat dan menghapus direktori, serta membuat symbolic link. Hasilnya menunjukkan bagaimana Linux mengelola file dan direktori serta hubungan antar file dalam sistem.

3. kesimpulan
    Dari praktikum ini dapat disimpulkan bahwa sistem operasi Linux memiliki struktur file berbentuk hierarki. Pengguna dapat mengelola file dan direktori menggunakan berbagai perintah dasar seperti cd, ls, pwd, cp, mv, mkdir, dan rm untuk navigasi dan manajemen file.