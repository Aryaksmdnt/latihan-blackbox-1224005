# Dokumen Test Case: Form Pendaftaran Online

**Teknik:** Equivalence Partitioning (EP) dan Boundary Value Analysis (BVA)  
**Mata kuliah:** Implementasi Pengujian Perangkat Lunak (Pertemuan 5)  
**Penyusun:** Arya Kusuma Dinata (1224005)

## Spesifikasi

| Field | Validasi |
|---|---|
| Nama | 3-100 karakter |
| Email | Format email valid |
| No. HP | 10-13 digit, diawali 08 |
| Tanggal Lahir | Format YYYY-MM-DD, umur minimal 17 tahun |
| Password | Minimal 8 karakter, huruf besar, huruf kecil, angka, simbol |
| Konfirmasi Password | Harus sama dengan password |

> Asumsi: tanggal acuan "hari ini" = 2026-10-17; tiap test case hanya menguji satu field, field lain memakai data baseline valid; teks pesan error adalah contoh perilaku yang diharapkan.

## 1. Equivalence Partitioning

| Field | Partisi | Kategori | Kondisi | Contoh Nilai |
|---|---|---|---|---|
| Nama | P1 | Valid | 3 - 100 karakter | `"Arya Kusuma Dinata"` |
| Nama | P2 | Invalid | < 3 karakter | `"Ab"` |
| Nama | P3 | Invalid | > 100 karakter | `"A" x 101 (101 karakter)` |
| Nama | P4 | Invalid | Kosong | `"" (kosong)` |
| Email | P1 | Valid | Format email valid | `"arya@example.com"` |
| Email | P2 | Invalid | Tanpa @ | `"aryaexample.com"` |
| Email | P3 | Invalid | Tanpa domain | `"arya@"` |
| Email | P4 | Invalid | Tanpa nama pengguna | `"@example.com"` |
| Email | P5 | Invalid | Kosong | `"" (kosong)` |
| No. HP | P1 | Valid | 10-13 digit, diawali 08 | `"081234567890"` |
| No. HP | P2 | Invalid | < 10 digit | `"08123456"` |
| No. HP | P3 | Invalid | > 13 digit | `"081234567890123"` |
| No. HP | P4 | Invalid | Tidak diawali 08 | `"071234567890"` |
| No. HP | P5 | Invalid | Mengandung non-digit | `"0812345abc90"` |
| No. HP | P6 | Invalid | Kosong | `"" (kosong)` |
| Tanggal Lahir | P1 | Valid | Format YYYY-MM-DD, umur >= 17 tahun | `"2000-05-20"` |
| Tanggal Lahir | P2 | Invalid | Format benar, umur < 17 tahun | `"2015-01-01"` |
| Tanggal Lahir | P3 | Invalid | Format salah | `"20-05-2000"` |
| Tanggal Lahir | P4 | Invalid | Tanggal tidak ada di kalender | `"2000-02-30"` |
| Tanggal Lahir | P5 | Invalid | Tanggal di masa depan | `"2030-01-01"` |
| Tanggal Lahir | P6 | Invalid | Kosong | `"" (kosong)` |
| Password | P1 | Valid | >= 8 karakter, besar + kecil + angka + simbol | `"Pass@1234"` |
| Password | P2 | Invalid | < 8 karakter | `"Pa@1234"` |
| Password | P3 | Invalid | Tanpa huruf besar | `"pass@1234"` |
| Password | P4 | Invalid | Tanpa huruf kecil | `"PASS@1234"` |
| Password | P5 | Invalid | Tanpa angka | `"Pass@word"` |
| Password | P6 | Invalid | Tanpa simbol | `"Pass12345"` |
| Password | P7 | Invalid | Kosong | `"" (kosong)` |
| Konfirmasi Password | P1 | Valid | Sama persis dengan password | `"Pass@1234"` |
| Konfirmasi Password | P2 | Invalid | Berbeda dengan password | `"Pass@12345"` |
| Konfirmasi Password | P3 | Invalid | Beda huruf besar/kecil | `"pass@1234"` |
| Konfirmasi Password | P4 | Invalid | Kosong | `"" (kosong)` |

## 2. Boundary Value Analysis

| Field | Boundary | Nilai Uji | Kategori | Expected Output |
|---|---|---|---|---|
| Nama | min-1 | `"Ab" (2 karakter)` | Invalid | Ditolak: Nama minimal 3 karakter |
| Nama | min | `"Abc" (3 karakter)` | Valid | Diterima |
| Nama | min+1 | `"Abcd" (4 karakter)` | Valid | Diterima |
| Nama | max-1 | `"A" x 99 (99 karakter) (99 karakter)` | Valid | Diterima |
| Nama | max | `"A" x 100 (100 karakter) (100 karakter)` | Valid | Diterima |
| Nama | max+1 | `"A" x 101 (101 karakter) (101 karakter)` | Invalid | Ditolak: Nama maksimal 100 karakter |
| No. HP | min-1 | `"081234567" (9 digit)` | Invalid | Ditolak: No. HP minimal 10 digit |
| No. HP | min | `"0812345678" (10 digit)` | Valid | Diterima |
| No. HP | min+1 | `"08123456789" (11 digit)` | Valid | Diterima |
| No. HP | max-1 | `"081234567890" (12 digit)` | Valid | Diterima |
| No. HP | max | `"0812345678901" (13 digit)` | Valid | Diterima |
| No. HP | max+1 | `"08123456789012" (14 digit)` | Invalid | Ditolak: No. HP maksimal 13 digit |
| Tanggal Lahir | min-1 | `"2009-10-18" (16 thn 364 hari)` | Invalid | Ditolak: Umur minimal 17 tahun |
| Tanggal Lahir | min | `"2009-10-17" (tepat 17 thn)` | Valid | Diterima |
| Tanggal Lahir | min+1 | `"2009-10-16" (17 thn 1 hari)` | Valid | Diterima |
| Password | min-1 | `"Pa@1234" (7 karakter)` | Invalid | Ditolak: Password minimal 8 karakter |
| Password | min | `"Pass@123" (8 karakter)` | Valid | Diterima |
| Password | min+1 | `"Pass@1234" (9 karakter)` | Valid | Diterima |

## 3. Test Case Lengkap (40 test case)

**Data baseline (valid):** Nama = "Arya Kusuma Dinata"; Email = "arya@example.com"; No. HP = "081234567890"; Tanggal Lahir = "2000-05-20"; Password = "Pass@1234"; Konfirmasi Password = "Pass@1234". Untuk test case field Password, Konfirmasi Password diisi sama dengan Password yang diuji.

| No | Field | Teknik | Data Uji | Kategori | Expected Output |
|---|---|---|---|---|---|
| TC-01 | Semua field | EP | Semua field = data baseline valid | Valid | Registrasi berhasil |
| TC-02 | Nama | BVA | Nama = "Ab" | Invalid | Ditolak: Nama minimal 3 karakter |
| TC-03 | Nama | BVA | Nama = "Abc" | Valid | Registrasi berhasil |
| TC-04 | Nama | BVA | Nama = "Abcd" | Valid | Registrasi berhasil |
| TC-05 | Nama | BVA | Nama = "A" x 99 (99 karakter) | Valid | Registrasi berhasil |
| TC-06 | Nama | BVA | Nama = "A" x 100 (100 karakter) | Valid | Registrasi berhasil |
| TC-07 | Nama | BVA | Nama = "A" x 101 (101 karakter) | Invalid | Ditolak: Nama maksimal 100 karakter |
| TC-08 | Nama | EP | Nama = "" (kosong) | Invalid | Ditolak: Nama wajib diisi |
| TC-09 | Email | EP | Email = "aryaexample.com" | Invalid | Ditolak: Format email tidak valid |
| TC-10 | Email | EP | Email = "arya@" | Invalid | Ditolak: Format email tidak valid |
| TC-11 | Email | EP | Email = "@example.com" | Invalid | Ditolak: Format email tidak valid |
| TC-12 | Email | EP | Email = "" (kosong) | Invalid | Ditolak: Email wajib diisi |
| TC-13 | No. HP | BVA | No. HP = "081234567" | Invalid | Ditolak: No. HP minimal 10 digit |
| TC-14 | No. HP | BVA | No. HP = "0812345678" | Valid | Registrasi berhasil |
| TC-15 | No. HP | BVA | No. HP = "08123456789" | Valid | Registrasi berhasil |
| TC-16 | No. HP | BVA | No. HP = "081234567890" | Valid | Registrasi berhasil |
| TC-17 | No. HP | BVA | No. HP = "0812345678901" | Valid | Registrasi berhasil |
| TC-18 | No. HP | BVA | No. HP = "08123456789012" | Invalid | Ditolak: No. HP maksimal 13 digit |
| TC-19 | No. HP | EP | No. HP = "071234567890" | Invalid | Ditolak: No. HP harus diawali 08 |
| TC-20 | No. HP | EP | No. HP = "0812345abc90" | Invalid | Ditolak: No. HP hanya boleh angka |
| TC-21 | No. HP | EP | No. HP = "" (kosong) | Invalid | Ditolak: No. HP wajib diisi |
| TC-22 | Tanggal Lahir | BVA | Tanggal Lahir = "2009-10-18" | Invalid | Ditolak: Umur minimal 17 tahun |
| TC-23 | Tanggal Lahir | BVA | Tanggal Lahir = "2009-10-17" | Valid | Registrasi berhasil |
| TC-24 | Tanggal Lahir | BVA | Tanggal Lahir = "2009-10-16" | Valid | Registrasi berhasil |
| TC-25 | Tanggal Lahir | EP | Tanggal Lahir = "2015-01-01" | Invalid | Ditolak: Umur minimal 17 tahun |
| TC-26 | Tanggal Lahir | EP | Tanggal Lahir = "20-05-2000" | Invalid | Ditolak: Format tanggal lahir harus YYYY-MM-DD |
| TC-27 | Tanggal Lahir | EP | Tanggal Lahir = "2000-02-30" | Invalid | Ditolak: Tanggal lahir tidak valid |
| TC-28 | Tanggal Lahir | EP | Tanggal Lahir = "2030-01-01" | Invalid | Ditolak: Tanggal lahir tidak boleh di masa depan |
| TC-29 | Tanggal Lahir | EP | Tanggal Lahir = "" (kosong) | Invalid | Ditolak: Tanggal lahir wajib diisi |
| TC-30 | Password | BVA | Password = "Pa@1234" | Invalid | Ditolak: Password minimal 8 karakter |
| TC-31 | Password | BVA | Password = "Pass@123" | Valid | Registrasi berhasil |
| TC-32 | Password | BVA | Password = "Pass@1234" | Valid | Registrasi berhasil |
| TC-33 | Password | EP | Password = "pass@1234" | Invalid | Ditolak: Password harus mengandung huruf besar |
| TC-34 | Password | EP | Password = "PASS@1234" | Invalid | Ditolak: Password harus mengandung huruf kecil |
| TC-35 | Password | EP | Password = "Pass@word" | Invalid | Ditolak: Password harus mengandung angka |
| TC-36 | Password | EP | Password = "Pass12345" | Invalid | Ditolak: Password harus mengandung simbol |
| TC-37 | Password | EP | Password = "" (kosong) | Invalid | Ditolak: Password wajib diisi |
| TC-38 | Konfirmasi Password | EP | Konfirmasi Password = "Pass@12345" | Invalid | Ditolak: Konfirmasi password harus sama dengan password |
| TC-39 | Konfirmasi Password | EP | Konfirmasi Password = "pass@1234" | Invalid | Ditolak: Konfirmasi password harus sama dengan password |
| TC-40 | Konfirmasi Password | EP | Konfirmasi Password = "" (kosong) | Invalid | Ditolak: Konfirmasi password wajib diisi |
