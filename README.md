# KosFinder Device Demo

KosFinder Device Demo merupakan aplikasi latihan berbasis Flutter untuk mempelajari integrasi fitur perangkat mobile, meliputi kamera, galeri, GPS, penyimpanan lokal, dan Supabase Storage.

Project ini dibuat secara mandiri untuk memenuhi praktikum Worksheet 10 – Advanced Mobile Features & Device Integration. .

## Fitur Aplikasi

### 1. Kamera dan Galeri
- Mengambil foto menggunakan kamera perangkat.
- Memilih foto melalui galeri.
- Menampilkan foto yang telah dipilih.
- Membatasi format foto menjadi JPG, JPEG, dan PNG.
- Membatasi ukuran foto maksimal 5 MB.
- Menyalin foto ke penyimpanan permanen aplikasi.

### 2. GPS dan Runtime Permission
- Mengambil koordinat latitude dan longitude perangkat.
- Memeriksa status layanan GPS.
- Meminta izin lokasi ketika pengguna menekan tombol GPS.
- Menangani izin lokasi yang ditolak.
- Menangani izin lokasi yang ditolak secara permanen.
- Memberikan akses ke pengaturan lokasi atau izin aplikasi sesuai kondisi.

### 3. Penyimpanan Draft Lokal
- Menyimpan nama kos.
- Menyimpan path foto.
- Menyimpan koordinat GPS.
- Menyimpan metadata dalam format JSON menggunakan SharedPreferences.
- Menyimpan foto secara permanen menggunakan Application Documents Directory.
- Memulihkan data draft ketika aplikasi dibuka kembali.

### 4. Supabase Storage (Pengayaan)
- Menggunakan Anonymous Sign-In.
- Mengunggah foto ke Supabase Storage.
- Menggunakan bucket `kosfinder-demo`.
- Membatasi ukuran file maksimal 5 MB.
- Membatasi format MIME menjadi `image/jpeg` dan `image/png`.
- Menggunakan Row Level Security (RLS) untuk membatasi lokasi upload berdasarkan UID pengguna.

### 5. Demo Accelerometer (Pengayaan)
- Membaca nilai percepatan perangkat melalui `sensors_plus`.
- Menampilkan nilai sumbu X, Y, dan Z dalam satuan m/s².
- Menangani kondisi ketika sensor tidak tersedia.
- Menghentikan subscription ketika halaman sensor ditutup.

## Teknologi dan Dependencies

- Flutter
- Dart
- image_picker
- geolocator
- path_provider
- shared_preferences
- supabase_flutter
- sensors_plus

## Struktur Project

```text
kosfinder_device_demo/
├── android/
│   └── app/
│       └── src/
│           └── main/
│               └── AndroidManifest.xml
├── docs/
│   ├── screenshots/
│   └── hasil-pengujian.md
├── ios/
├── lib/
│   ├── main.dart
│   ├── cloud_config.dart
│   ├── pages/
│   │   ├── device_demo_page.dart
│   │   └── sensor_demo_page.dart
│   └── services/
│       ├── draft_repository.dart
│       ├── device_location_service.dart
│       └── photo_upload_service.dart
├── test/
│   └── widget_test.dart
├── .gitignore
├── .metadata
├── analysis_options.yaml
├── pubspec.yaml
├── pubspec.lock
└── README.md
```

## Persiapan Project

Pastikan Flutter SDK dan Android SDK sudah terpasang.

Masuk ke direktori project, kemudian jalankan:

```bash
flutter pub get
```

## Menjalankan Aplikasi dalam Mode Lokal

Untuk menjalankan aplikasi tanpa konfigurasi Supabase:

```bash
flutter run
```

Mode lokal menyediakan fitur kamera, galeri, GPS, dan penyimpanan draft tanpa memerlukan akun atau konfigurasi cloud.

## Konfigurasi Supabase Storage

Supabase digunakan sebagai pengayaan untuk fitur upload foto.

Konfigurasi yang diperlukan:

1. Membuat project Supabase.
2. Mengaktifkan Anonymous Sign-In.
3. Membuat bucket `kosfinder-demo`.
4. Mengaktifkan Public Bucket untuk foto demo nonprivat.
5. Mengatur batas ukuran file sebesar 5 MB.
6. Mengatur allowed MIME types menjadi `image/jpeg` dan `image/png`.
7. Menerapkan Storage RLS Policy untuk membatasi upload berdasarkan UID pengguna.

### Storage RLS Policy

```sql
drop policy if exists "ws10_demo_upload_own_folder" on storage.objects;

create policy "ws10_demo_upload_own_folder"
on storage.objects
for insert
to authenticated
with check (
  bucket_id = 'kosfinder-demo'
  and (storage.foldername(name))[1] = (select auth.uid()::text)
);
```

### Menghubungkan Supabase dengan Flutter

Jalankan aplikasi dengan Project URL dan Publishable Key milik project Supabase:

```bash
flutter run \
  --dart-define=SUPABASE_URL=https://YOUR_PROJECT.supabase.co \
  --dart-define=SUPABASE_PUBLISHABLE_KEY=YOUR_PUBLISHABLE_KEY
```

Ganti nilai tersebut dengan kredensial project masing-masing. Gunakan Publishable Key, bukan Secret Key atau service_role key.

Catatan: Public Bucket memungkinkan foto diakses oleh siapa pun yang memiliki URL. Gunakan foto demo yang tidak mengandung informasi pribadi.

## Pemeriksaan Project

Untuk memeriksa kode dan menjalankan pengujian Flutter:

```bash
flutter analyze
flutter test
```

## Rencana Pengujian Perangkat

Pengujian perangkat mencakup:

1. Mengambil foto melalui kamera.
2. Memilih foto melalui galeri.
3. Membatalkan pemilihan foto.
4. Menangani penolakan izin kamera atau galeri.
5. Mengambil koordinat GPS.
6. Menangani izin GPS yang ditolak.
7. Menangani layanan GPS yang dinonaktifkan.
8. Membuka kembali aplikasi dan memulihkan draft lokal.
9. Memastikan penyimpanan lokal tetap berfungsi tanpa internet.
10. Menguji upload foto ke Supabase.
11. Menguji kondisi upload ketika perangkat offline.
12. Menguji pembacaan accelerometer apabila pengayaan sensor digunakan.

## Repository GitHub

https://github.com/kadekmartini/kosfinder_device_demo

