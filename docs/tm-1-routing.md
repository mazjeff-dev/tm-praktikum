# TM-1 — Peta Routing Pribadi

## Entity: Kamar

Tugas ini memetakan kontrak routing entity Kamar pada tiga lapisan aplikasi,
yaitu API, SvelteKit, ATLAS SPA, dan Flutter.

| METHOD + API | SvelteKit File | ATLAS SPA | Flutter Name + Args | US-XX |
|---|---|---|---|---|
| GET /api/v1/kamar | routes/kamar/+page.svelte | /kamar | KamarPage() | US-01 |
| GET /api/v1/kamar/:id | routes/kamar/[id]/+page.svelte | /kamar/:id | KamarDetailPage(id) | US-02 |
| POST /api/v1/kamar | routes/kamar/baru/+page.svelte | /kamar/baru | KamarCreatePage() | US-03 |
| PUT /api/v1/kamar/:id | routes/kamar/[id]/edit/+page.svelte | /kamar/:id/edit | KamarEditPage(id) | US-04 |
| DELETE /api/v1/kamar/:id | routes/kamar/[id]/+page.svelte | /kamar/:id | deleteKamar(id) | US-05 |

## Authorization

Route yang membutuhkan akses terhadap data tertentu menggunakan pemeriksaan
authorize atau canAccess sesuai kebutuhan pengguna.

Untuk route yang menggunakan parameter `[id]`, nilai ID berasal dari parameter
URL. Route `/baru` digunakan untuk membuat data baru dan tidak menggunakan
`[id]`.

## Catatan

Prefix API menggunakan `/api/v1`.

Parameter dinamis menggunakan `:id` pada API dan `[id]` pada struktur route
SvelteKit.

Route `/baru` digunakan untuk halaman pembuatan data baru sehingga tidak
tertukar dengan route `/kamar/:id`.