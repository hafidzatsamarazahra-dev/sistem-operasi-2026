# Laporan pertemuan 10 sistem operasi

<h4>Nama : Hafidza Tsamara Zahra<h4>
<h4>NIM : 254107020034<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 10.1 Melihat Penggunaan Memori

<img src="Screenshot 2026-05-03 182439.png" width="70%">

## Studi Kasus 10.1 Server Lambat karena Memori

<img src="Screenshot 2026-05-03 182926.png" width="70%">

## Praktikum 10.2 Mengamati Aktivitas Paging

<img src="Screenshot 2026-05-03 183152.png" width="70%">

## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File

<img src="Screenshot 2026-05-03 193829.png" width="70%">

## Praktikum 10.4 Monitoring Memory

<img src="Screenshot 2026-05-03 212555.png" width="70%">

## Praktikum 10.5 Script Monitor Memori

<img src="Screenshot 2026-05-04 104915.png" width="70%">
<img src="Screenshot 2026-05-04 105057.png" width="70%">

## Studi Kasus 10.2 Gagal Akses File

<img src="Screenshot 2026-05-04 105545.png" width="70%">

## Praktikum 10.6 Mengamati System Call dengan strace

<img src="Screenshot 2026-05-04 110637.png" width="70%">
<img src="Screenshot 2026-05-04 110741.png" width="70%">

## 1.6 Tugas Praktikum

### Tugas 10.1 Audit Penggunaan Memori Sistem

<img src="Screenshot 2026-05-04 203748.png" width="70%">

Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah
sistem dalam kondisi normal?
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut
pandang ketersediaan untuk aplikasi?
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?

jawaban
1. memori tersedia sekitar 84%. Ini kondisi normal (bahkan sangat lega), karena sebagian besar RAM masih bisa digunakan aplikasi.
2. Karena:
- buff/cache adalah memori yang dipakai sistem untuk cache file dan buffering
- Tujuannya untuk mempercepat akses data
- Jika aplikasi butuh RAM, cache ini bisa langsung dilepaskan (reclaimable)
3. SwapTotal: 0 kB

    SwapFree: 0 kB

    Artinya:

    Sistem tidak menggunakan swap sama sekali.    Tidak ada ruang swap yang dialokasikan

## Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi

<img src="Screenshot 2026-05-04 204811.png" width="70%">

Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka
gunakan bersama?

jawaban
1. Yang paling atas itu:
    - /usr/lib/snapd/snapd
    - %MEM = 1.7%
    - RSS = 35132 KB
2. 35132 ÷ 1024 ≈ 34.3 MB

    Jadi sekitar 34 MB
    Nilai tersebut tergolong wajar, karena penggunaan memori oleh proses sistem umumnya berada pada kisaran puluhan MB
3. Nilai %MEM dari lima proses teratas adalah:
    1.7% + 1.3% + 1.0% + 0.9% + 0.7% = 5.6%

    Dengan demikian, kelima proses tersebut secara bersama-sama menggunakan sekitar 5.6% dari total RAM.

## Tugas 10.3 Membuat dan Memverifikasi Swap File

<img src="Screenshot 2026-05-04 205827.png" width="70%">

Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?

jawaban
1. Output swapon --show umumnya memiliki beberapa kolom utama:

    - NAME : menunjukkan lokasi file atau partisi swap (misalnya /swapfile-tugas-week10)
    - TYPE : jenis swap yang digunakan, biasanya file atau partition
    - SIZE : kapasitas total swap yang tersedia (misalnya 256M)
    - USED : jumlah swap yang sedang digunakan oleh sistem
2. Jika proses pembuatan dan aktivasi swap berhasil, maka:

    - Nilai Swap total pada output free -h akan bertambah sebesar ±256 MB
    - Jika belum bertambah, kemungkinan:
        - swap belum berhasil diaktifkan (swapon gagal), atau
        - terjadi kesalahan pada langkah konfigurasi sebelumnya
3. Permission 600 penting karena hanya root yang bisa mengakses swap file, sehingga data di dalamnya tetap aman.
Jika diatur 644, user lain bisa membaca isi swap, sehingga berisiko terjadi kebocoran data sensitif.

## Tugas 10.4 Analisis System Call dengan strace

<img src="Screenshot 2026-05-04 210449.png" width="70%">
<img src="Screenshot 2026-05-04 210513.png" width="70%">

analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi
singkatnya.
2. System call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal
meskipun ada kegagalan tersebut?

jawaban
1. - read() : membaca data dari file descriptor
    - write() : menulis data ke file descriptor
    - open() / openat() : membuka file atau resource
    - close() : menutup file descriptor
    - stat() / fstat() → mengambil informasi metadata file
    - mmap() : memetakan file atau memori ke address space proses

2. Biasanya yang paling sering adalah read(), write(), atau openat().

    Alasannya:

    Program sering melakukan input/output (I/O)
    Banyak akses file, library, dan konfigurasi sistem
    Setiap operasi kecil (baca/tulis) akan memanggil system call tersebut

3. Jika terdapat nilai error lebih dari 0, artinya ada system call yang gagal
    Namun, program tetap bisa berjalan normal jika:
    error tersebut tidak kritis
    atau sudah ditangani oleh sistem/program (misalnya fallback)

## Tugas 10.5 Studi Kasus Diagnosa Server Lambat

<img src="Screenshot 2026-05-05 172703.png" width="70%">
<img src="Screenshot 2026-05-05 172809.png" width="70%">

analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses,
cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi
terpisah?
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis?
Jelaskan berdasarkan nilai threshold yang digunakan script.
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa >
"$LAPORAN"? Apa keuntungannya?
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa
implikasinya terhadap performa server?

jawaban
1. - cek_memori: Memeriksa ketersediaan RAM fisik.

    - cek_swap: Melihat penggunaan memori virtual (swap) pada disk.

    - cek_proses: Menampilkan daftar proses yang paling banyak memakan RAM.

    - cek_paging: Memantau lalu lintas data antara RAM dan swap (si/so).

    ringkasan: Memberikan kesimpulan akhir status sistem.

    Alasan: Agar kode lebih modular, mudah diperbaiki, dan laporan tersusun rapi per kategori.
2. Status: Normal.

    Analisis: Output Ringkasan menyatakan "Memori: normal" dan "Swap: tidak digunakan". Nilai free pada vmstat masih besar (~1.4 GB) dan swpd menunjukkan angka 0, yang berarti beban masih di bawah ambang batas kritis.
3. Mekanisme: tee mengirim output ke dua arah sekaligus: layar terminal dan file laporan.

    Keuntungan: Administrator bisa memantau proses secara langsung (real-time) sambil tetap memiliki salinan permanen di file diagnosa-server-lambat.txt.
4. Data: Nilai si (swap-in) dan so (swap-out) adalah 0.

    Implikasi: Sangat Baik. Tidak ada data yang terpaksa dipindahkan ke disk karena RAM penuh. Server bekerja dengan kecepatan maksimal memori tanpa hambatan I/O disk yang lambat.