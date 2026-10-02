# TM-4 — HTTP Client + DevTools

## Base URL

https://silab.ft.unira.ac.id/api/v1

## A. Thunder Client — GET Base

Request:

GET https://silab.ft.unira.ac.id/api/v1

Hasil pengujian:

- Method: GET
- Status Code: 200 OK
- Response: HTML pemberitahuan bahwa SILAB telah berpindah ke ATLAS.
- Status dan message JSON tidak tersedia karena response berupa HTML.

Bukti screenshot:

docs/bukti-tm-4/get-base.png

## B. DevTools Network

Halaman yang dibuka:

https://silab.ft.unira.ac.id/jadwal

Pada DevTools Network ditemukan request:

Request URL:
https://silab.ft.unira.ac.id/api/v1/graphql

Request Method:
POST

Status Code:
200 OK

Request tersebut menggunakan endpoint GraphQL pada path `/api/v1/graphql`.

Bukti screenshot:

docs/bukti-tm-4/devtools-network.png

## C. curl

Perintah yang digunakan:

curl.exe -i https://silab.ft.unira.ac.id/api/v1/salah-ketik

Hasil pengujian:

HTTP/1.1 404 Not Found

Response:

{
  "status": false,
  "message": "Api atau berkas tidak ditemukan"
}

Hasil tersebut menunjukkan bahwa endpoint `/api/v1/salah-ketik` tidak ditemukan oleh server.

Bukti screenshot:

docs/bukti-tm-4/curl-salah-ketik.png

## Perbedaan curl -s dan curl -i

1. `curl -s` atau silent mode menyembunyikan progress meter sehingga output menjadi lebih bersih.

2. `curl -i` menampilkan header HTTP bersama dengan response body.

3. `curl -i` lebih berguna untuk memeriksa informasi HTTP seperti status code dan header response.

## Kesimpulan

Pengujian menggunakan Thunder Client, DevTools Network, dan curl menunjukkan cara memeriksa request dan response HTTP menggunakan beberapa alat.

Thunder Client digunakan untuk menguji endpoint secara langsung. DevTools Network digunakan untuk melihat request yang dilakukan oleh halaman web. Sedangkan curl digunakan untuk melihat response HTTP beserta header-nya.

Berdasarkan pengujian aktual, GET `/api/v1` menghasilkan `200 OK`, request `/api/v1/graphql` menghasilkan `200 OK`, dan endpoint `/api/v1/salah-ketik` menghasilkan `404 Not Found`.