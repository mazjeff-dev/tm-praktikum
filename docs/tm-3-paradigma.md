# TM-3 — Perbandingan 4 Paradigma API

## Kasus

Dashboard membutuhkan tiga data:
- Total jadwal
- Daftar jadwal
- Tagihan

## Perbandingan

### 1. REST

Pada REST, dashboard dapat membutuhkan beberapa request untuk mengambil data yang berbeda.

Contohnya:
- GET /api/v1/jadwal/jumlah-jadwal
- GET /api/v1/jadwal
- GET /api/v1/tagihan

Jika ketiga data berasal dari endpoint berbeda, maka diperlukan sekitar 3 request.

Kelebihan:
- Sederhana dan mudah dipahami.
- Endpoint jelas.
- Cocok untuk operasi CRUD.

Kekurangan:
- Dashboard dapat membutuhkan beberapa request.
- Data yang diterima mengikuti struktur endpoint.

### 2. GraphQL

GraphQL dapat mengambil beberapa data yang dibutuhkan dashboard melalui satu request.

Contohnya menggunakan query seperti `dashboardTrend`.

Dengan satu request, client dapat meminta total jadwal, daftar jadwal, dan tagihan sesuai kebutuhan.

Kelebihan:
- Dapat mengambil beberapa data dalam satu request.
- Client dapat menentukan data yang dibutuhkan.

Kekurangan:
- Implementasi lebih kompleks dibanding REST.
- Membutuhkan server GraphQL.

### 3. gRPC

gRPC dapat digunakan untuk komunikasi antar-service.

Contohnya service dashboard meminta data jadwal dan tagihan dari service lain melalui komunikasi internal.

Kelebihan:
- Cocok untuk komunikasi antar-service.
- Efisien untuk komunikasi internal.

Kekurangan:
- Tidak sesederhana REST untuk client web biasa.
- Membutuhkan konfigurasi dan struktur service.

### 4. WebSocket / Polling

WebSocket atau polling dapat digunakan ketika dashboard membutuhkan pembaruan data secara berkala atau mendekati real-time.

Contohnya angka total jadwal pada dashboard diperbarui ketika terjadi perubahan data.

Kelebihan:
- Cocok untuk data yang perlu diperbarui secara berkala atau live.
- Client dapat memperoleh pembaruan tanpa melakukan refresh halaman secara manual.

Kekurangan:
- Implementasi lebih kompleks.
- Untuk polling, client harus melakukan request berulang.

## Pilihan

Untuk kasus dashboard yang membutuhkan total jadwal, daftar jadwal, dan tagihan, saya memilih **GraphQL** karena beberapa data dapat diminta dalam satu request melalui query `dashboardTrend`.

Pilihan dapat diganti ke REST apabila kebutuhan aplikasi lebih sederhana dan endpoint REST yang tersedia sudah mencukupi.

WebSocket/polling lebih sesuai apabila kebutuhan utama berubah menjadi pembaruan angka secara live.

gRPC lebih sesuai apabila kebutuhan utamanya adalah komunikasi antar-service.

## Kesimpulan

REST, GraphQL, gRPC, dan WebSocket/polling memiliki kegunaan yang berbeda. REST cocok untuk API berbasis endpoint, GraphQL cocok untuk mengambil beberapa data sesuai kebutuhan client, gRPC cocok untuk komunikasi antar-service, sedangkan WebSocket/polling cocok untuk pembaruan data secara berkala atau live.