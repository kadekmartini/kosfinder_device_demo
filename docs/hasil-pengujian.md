# HASIL PENGUJIAN KOSFINDER DEVICE DEMO

## 1. Identitas Pengujian

| Keterangan | Isian |
|---|---|
| Nama aplikasi | KosFinder Device Demo |
| Nama mahasiswa | Kadek Martini Aristianti |
| NIM | 2415051004 |
| Kelas | PTI 5C |
| Platform | Android |
| Framework | Flutter |
| Project | kosfinder_device_demo |
| Perangkat pengujian | Samsung Galaxy A24 |
| Tanggal pengujian | 20 November 2026 |

## 2. Pengujian Fitur Utama

Pengujian fitur utama dilakukan untuk memastikan kamera, galeri, GPS, dan penyimpanan draft lokal dapat berfungsi sesuai dengan kebutuhan aplikasi.

| No. | Kasus Pengujian | Hasil yang Diharapkan | Status |
|---|---|---|---|
| 1 | Foto melalui kamera | Pratinjau foto tampil dan foto tersimpan secara permanen di penyimpanan aplikasi. | Berhasil |
| 2 | Foto melalui galeri | Foto yang dipilih dari galeri berhasil ditampilkan pada aplikasi. | Berhasil |
| 3 | Membatalkan pemilihan galeri | Aplikasi tetap berjalan dengan normal dan foto sebelumnya tidak berubah. | Berhasil |
| 4 | Izin kamera atau galeri tidak tersedia | Aplikasi menampilkan pesan kesalahan dan tidak mengalami crash. | Berhasil |
| 5 | GPS diberikan | Koordinat latitude dan longitude berhasil ditampilkan pada aplikasi. | Berhasil |
| 6 | Izin GPS ditolak | Aplikasi menampilkan pesan izin lokasi ditolak dan draft lokal tetap dapat disimpan. | Berhasil |
| 7 | GPS dinonaktifkan | Aplikasi menampilkan pesan bahwa layanan lokasi tidak aktif dan menyediakan akses menuju pengaturan lokasi. | Berhasil |
| 8 | Aplikasi ditutup dan dibuka kembali | Nama kos, foto, dan koordinat yang telah disimpan berhasil dipulihkan. | Berhasil |
| 9 | Perangkat tanpa internet | Penyimpanan draft lokal tetap berfungsi meskipun perangkat tidak memiliki koneksi internet. | Berhasil |

## 3. Pengujian Pengayaan Supabase Storage

Pengujian Supabase Storage dilakukan untuk memastikan aplikasi dapat mengunggah foto ke penyimpanan cloud menggunakan Anonymous Sign-In dan kebijakan Row Level Security (RLS).

| No. | Kasus Pengujian | Hasil yang Diharapkan | Status |
|---|---|---|---|
| 10 | Upload foto berhasil | Foto berhasil diunggah dan muncul pada bucket `kosfinder-demo` di dalam folder UID pengguna. Aplikasi menampilkan lokasi objek dan URL foto. | Berhasil |
| 11 | Upload ketika offline | Proses upload gagal dengan pesan kesalahan, tetapi draft lokal tetap tersedia dan tidak terhapus. | Berhasil |

## 4. Pengujian Sensor Accelerometer (Opsional)

Pengujian sensor accelerometer dilakukan untuk memastikan aplikasi dapat membaca perubahan percepatan perangkat melalui sumbu X, Y, dan Z menggunakan plugin `sensors_plus`.

| No. | Kasus Pengujian | Hasil yang Diharapkan | Status |
|---|---|---|---|
| 12 | Sensor accelerometer | Nilai sumbu X, Y, dan Z ditampilkan serta mengalami perubahan ketika perangkat digerakkan. Jika sensor tidak tersedia, aplikasi menangani kondisi tersebut tanpa mengalami crash. | Berhasil |

## 5. Dokumentasi Prosedur Pengujian

### 5.1 Pengujian Kamera

1. Membuka aplikasi KosFinder Device Demo.
2. Mengisi nama kos pada kolom yang tersedia.
3. Menekan tombol Kamera.
4. Mengambil foto menggunakan kamera perangkat.
5. Memilih opsi untuk menggunakan foto.
6. Memastikan foto tampil pada halaman aplikasi dan tersimpan di penyimpanan permanen.

### 5.2 Pengujian Galeri

1. Membuka aplikasi KosFinder Device Demo.
2. Menekan tombol Galeri.
3. Memilih salah satu foto dengan format JPG, JPEG, atau PNG.
4. Memastikan foto berhasil ditampilkan pada aplikasi.

### 5.3 Pengujian Pembatalan Galeri

1. Membuka aplikasi KosFinder Device Demo.
2. Menekan tombol Galeri.
3. Membatalkan pemilihan foto tanpa memilih gambar.
4. Memastikan aplikasi tetap berjalan dan foto sebelumnya tidak berubah.

### 5.4 Pengujian Izin Kamera atau Galeri

1. Membuka pengaturan izin aplikasi KosFinder pada perangkat.
2. Mengatur akses kamera atau akses yang relevan menjadi tidak diizinkan.
3. Kembali ke aplikasi.
4. Mencoba menggunakan fitur kamera atau galeri.
5. Memastikan aplikasi menangani kondisi tersebut dengan pesan yang sesuai dan tidak mengalami crash.

### 5.5 Pengujian GPS dengan Izin Diberikan

1. Membuka aplikasi KosFinder Device Demo.
2. Memastikan layanan lokasi perangkat aktif.
3. Menekan tombol Ambil Koordinat GPS.
4. Memberikan izin lokasi ketika sistem meminta persetujuan.
5. Memastikan koordinat latitude dan longitude tampil pada aplikasi.

### 5.6 Pengujian Izin GPS Ditolak

1. Membuka pengaturan izin lokasi aplikasi KosFinder.
2. Mengatur izin lokasi menjadi tidak diizinkan.
3. Kembali ke aplikasi.
4. Menekan tombol Ambil Koordinat GPS.
5. Memastikan aplikasi menampilkan pesan izin lokasi ditolak.
6. Memastikan fitur penyimpanan draft lokal tetap dapat digunakan.

### 5.7 Pengujian GPS Dinonaktifkan

1. Memastikan izin lokasi aplikasi tetap diberikan.
2. Menonaktifkan layanan Lokasi melalui pengaturan perangkat.
3. Kembali ke aplikasi KosFinder.
4. Menekan tombol Ambil Koordinat GPS.
5. Memastikan aplikasi menampilkan pesan bahwa layanan lokasi tidak aktif.
6. Memastikan tombol untuk membuka pengaturan lokasi tersedia.

### 5.8 Pengujian Pemulihan Draft Lokal

1. Mengisi nama kos pada aplikasi.
2. Memilih atau mengambil foto.
3. Mengambil koordinat GPS apabila tersedia.
4. Menekan tombol Simpan Draft Lokal.
5. Menutup aplikasi sepenuhnya.
6. Membuka kembali aplikasi KosFinder.
7. Memastikan nama kos, foto, dan koordinat sebelumnya berhasil dipulihkan.

### 5.9 Pengujian Penyimpanan Tanpa Internet

1. Menonaktifkan koneksi Wi-Fi dan data seluler perangkat.
2. Membuka aplikasi KosFinder dalam mode lokal.
3. Mengisi nama kos.
4. Memilih foto dari galeri atau kamera.
5. Menekan tombol Simpan Draft Lokal.
6. Memastikan draft berhasil disimpan meskipun perangkat tidak memiliki koneksi internet.

### 5.10 Pengujian Upload Supabase Berhasil

1. Mengaktifkan koneksi internet perangkat.
2. Menjalankan aplikasi dengan konfigurasi Supabase.
3. Memastikan aplikasi menampilkan mode lokal + Supabase.
4. Mengisi nama kos dan memilih foto.
5. Menekan tombol Upload Foto ke Supabase.
6. Memastikan aplikasi menampilkan pesan upload berhasil.
7. Membuka dashboard Supabase.
8. Memeriksa bucket `kosfinder-demo` dan memastikan foto muncul pada folder UID pengguna.

### 5.11 Pengujian Upload Supabase Ketika Offline

1. Menjalankan aplikasi dengan konfigurasi Supabase.
2. Memastikan perangkat memiliki draft lokal yang sudah tersimpan.
3. Menonaktifkan koneksi internet perangkat.
4. Menekan tombol Upload Foto ke Supabase.
5. Memastikan aplikasi menampilkan pesan kegagalan upload.
6. Memastikan draft lokal tetap tersedia dan tidak terhapus.

### 5.12 Pengujian Sensor Accelerometer

1. Membuka aplikasi KosFinder Device Demo.
2. Menekan ikon sensor pada bagian kanan atas halaman utama.
3. Memastikan halaman Demo Accelerometer terbuka.
4. Mengamati nilai sumbu X, Y, dan Z ketika perangkat dalam keadaan diam.
5. Menggerakkan perangkat secara perlahan ke beberapa arah.
6. Mengamati perubahan nilai percepatan pada setiap sumbu.
7. Memastikan aplikasi tetap berjalan dengan normal.

## 6. Kesimpulan Pengujian

Berdasarkan hasil pengujian yang telah dilakukan pada perangkat Samsung Galaxy A24, aplikasi KosFinder Device Demo berhasil menjalankan seluruh fitur yang diuji sesuai dengan hasil yang diharapkan.

Fitur kamera dan galeri berhasil digunakan untuk mengambil serta memilih foto. Fitur GPS berhasil memperoleh koordinat perangkat dan menangani kondisi ketika izin lokasi ditolak maupun layanan lokasi dinonaktifkan.

Penyimpanan draft lokal berhasil menyimpan nama kos, foto, dan koordinat serta memulihkan data ketika aplikasi dibuka kembali. Penyimpanan lokal juga tetap berfungsi ketika perangkat tidak memiliki koneksi internet.

Pada bagian pengayaan, fitur Supabase Storage berhasil melakukan upload foto dan menangani kegagalan upload ketika perangkat offline tanpa menghilangkan draft lokal. Fitur accelerometer juga berhasil membaca perubahan nilai percepatan pada sumbu X, Y, dan Z.

Dengan demikian, implementasi fitur utama dan pengayaan pada KosFinder Device Demo telah berjalan sesuai dengan kebutuhan praktikum Worksheet 10 – Advanced Mobile Features & Device Integration.