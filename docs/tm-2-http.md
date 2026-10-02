# TM-2 — Kartu HTTP Method + Code

## Base URL

```text
https://silab.ft.unira.ac.id/api/v1
```

## 1. GET /api/v1

- Method: GET
- URL: https://silab.ft.unira.ac.id/api/v1
- Status Code: 200 OK
- Status: tidak tersedia karena response berupa HTML
- Message: tidak tersedia karena response berupa HTML
- Response: Halaman pemberitahuan bahwa SILAB telah berpindah ke ATLAS.
- Siapa yang salah: Tidak ada, request berhasil mendapatkan response dari server.
- Aksi perbaikan: Tidak diperlukan. Server memberikan informasi bahwa layanan SILAB telah berpindah ke ATLAS.

## 2. GET /jadwal/jumlah-jadwal

- Method: GET
- URL: https://silab.ft.unira.ac.id/api/v1/jadwal/jumlah-jadwal
- Status Code: 401 Unauthorized
- Status: false
- Message: "Akses tidak diizinkan!"
- Siapa yang salah: Client/pengguna karena akses belum diizinkan.
- Aksi perbaikan: Periksa autentikasi/otorisasi dan gunakan kredensial atau token yang sesuai jika endpoint membutuhkannya.

## 3. POST /jadwal

- Method: POST
- URL: https://silab.ft.unira.ac.id/api/v1/jadwal
- Status Code: 401 Unauthorized
- Status: false
- Message: "Akses tidak diizinkan!"
- Siapa yang salah: Client/pengguna karena akses belum diizinkan.
- Aksi perbaikan: Periksa autentikasi/otorisasi dan gunakan kredensial atau token yang sesuai jika endpoint membutuhkannya.

## 4. GET /api/v1/xxx

- Method: GET
- URL: https://silab.ft.unira.ac.id/api/v1/xxx
- Status Code: 404 Not Found
- Status: false
- Message: "Api atau berkas tidak ditemukan"
- Siapa yang salah: Client karena URL atau endpoint yang diminta tidak ditemukan.
- Aksi perbaikan: Periksa kembali URL dan gunakan endpoint API yang benar.

## 5. POST GraphQL

- Method: POST
- URL: https://api.unira.ac.id/graphql
- Status Code: 200 OK
- Status: tidak tersedia pada response
- Message: tidak tersedia pada response
- Response:
  {"data":{"hello":"UNIRA GRAPHQL API"}}
- Siapa yang salah: Tidak ada, request berhasil diproses oleh server.
- Aksi perbaikan: Tidak diperlukan karena request berhasil.

## Pengujian Tambahan — GET /jadwal/abc

- Method: GET
- URL: https://silab.ft.unira.ac.id/api/v1/jadwal/abc
- Status Code: 404 Not Found
- Status: false
- Message: "Api atau berkas tidak ditemukan"
- Siapa yang salah: Client karena endpoint yang diminta tidak ditemukan.
- Aksi perbaikan: Periksa kembali URL dan endpoint yang digunakan.

## Pengujian Tambahan — GET /salah-ketik

- Method: GET
- URL: https://silab.ft.unira.ac.id/api/v1/salah-ketik
- Status Code: 404 Not Found
- Status: false
- Message: "Api atau berkas tidak ditemukan"
- Siapa yang salah: Client karena endpoint yang diminta tidak ditemukan.
- Aksi perbaikan: Periksa kembali URL dan endpoint yang digunakan.

## Ringkasan HTTP Status Code

| Kode | Kategori | Hasil Pengujian | Siapa yang salah | Aksi perbaikan |
|---|---|---|---|---|
| 200 | Success | GET /api/v1 dan POST GraphQL | Tidak ada | Tidak diperlukan |
| 201 | Success | Belum diperoleh dari pengujian API SILAB | - | - |
| 400 | Client Error | Belum diperoleh dari pengujian API SILAB | - | - |
| 401–403 | Authorization | GET /jadwal/jumlah-jadwal dan POST /jadwal → 401 | Client/pengguna | Periksa autentikasi/otorisasi |
| 500 | Server Error | Belum diperoleh dari pengujian API SILAB | - | - |

## Catatan Hasil Pengujian

Hasil pengujian dicatat berdasarkan response aktual yang diperoleh dari Thunder Client.

Pada pengujian API SILAB, request yang menggunakan endpoint yang tidak ditemukan menghasilkan status `404 Not Found`, bukan `400` atau `500`.

Status `201`, `400`, dan `500` belum diperoleh dari pengujian API SILAB pada tahap ini sehingga tidak dibuat-buat sebagai hasil pengujian.

Modul praktikum menyediakan contoh API Express lokal yang dapat menghasilkan `201 Created` untuk POST data valid dan `400` untuk input tertentu. Perilaku API latihan lokal tersebut berbeda dengan response API SILAB yang diuji pada tugas ini.

## Bukti Pengujian

Screenshot hasil pengujian dilampirkan sebagai bukti:

1. GET /api/v1 → 200 OK
2. GET /jadwal/jumlah-jadwal → 401 Unauthorized
3. POST /jadwal → 401 Unauthorized
4. GET /api/v1/xxx → 404 Not Found
5. POST GraphQL → 200 OK
6. GET /api/v1/jadwal/abc → 404 Not Found
7. GET /api/v1/salah-ketik → 404 Not Found