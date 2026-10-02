# TM-5 — Connector vs ORM

## 1. Kode Acuan dari Modul

File acuan:

`backend/src/routes/jadwal.js`

Route yang digunakan:

`GET /api/v1/jadwal/jumlah-jadwal`

Kode:

```javascript
router.get('/jumlah-jadwal', (_req, res) => {
  res.status(200).json({
    status: true,
    message: 'Jumlah jadwal berhasil dihitung',
    data: { total: jadwal.length },
  });
});

## 2. Versi Raw mysql2

Jika data jadwal sudah disimpan di database, perhitungan jumlah jadwal dapat dilakukan dengan query SQL menggunakan connector `mysql2`.

```javascript
const [rows] = await db.query(
  'SELECT COUNT(*) AS total FROM jadwal'
);

res.status(200).json({
  status: true,
  message: 'Jumlah jadwal berhasil dihitung',
  data: { total: rows[0].total },
});

## 3. Versi Prisma findMany()

Dengan Prisma ORM, data jadwal dapat diambil menggunakan method `findMany()`.

```javascript
const jadwal = await prisma.jadwal.findMany();

res.status(200).json({
  status: true,
  message: 'Jumlah jadwal berhasil dihitung',
  data: { total: jadwal.length },
});

## 4. Risiko SQL Injection pada Raw SQL

Penggunaan raw SQL dapat memiliki risiko SQL Injection apabila input dari pengguna langsung digabungkan ke dalam query SQL.

Contoh query yang berisiko:

```javascript
const sql = `SELECT * FROM jadwal WHERE nama = '${nama}'`;

## 5. Cara Prisma dan Sequelize Mengurangi Risiko SQL Injection

Prisma dan Sequelize menyediakan mekanisme query terstruktur dan parameterisasi sehingga input pengguna tidak perlu digabungkan secara langsung ke dalam string SQL.

Dengan pendekatan tersebut, nilai input pengguna diperlakukan sebagai data sehingga tidak mudah dianggap sebagai bagian dari perintah SQL.

Contoh penggunaan Prisma:

```javascript
const jadwal = await prisma.jadwal.findMany();

## 6. Perbandingan Raw mysql2 dan Prisma

| Aspek | Raw mysql2 | Prisma |
|---|---|---|
| Cara akses database | Menggunakan SQL secara langsung | Menggunakan ORM |
| Penulisan query | SQL ditulis oleh programmer | Menggunakan API/model Prisma |
| Abstraksi | Lebih rendah | Lebih tinggi |
| Contoh | `SELECT COUNT(*) FROM jadwal` | `prisma.jadwal.findMany()` |
| Pengelolaan input | Perlu memperhatikan parameterisasi | Dibantu oleh mekanisme Prisma |
| Kemudahan penggunaan | Membutuhkan pemahaman SQL | Lebih sederhana untuk operasi database tertentu |

Raw `mysql2` memberikan kontrol lebih langsung terhadap query SQL, sedangkan Prisma memberikan lapisan abstraksi ORM sehingga programmer dapat berinteraksi dengan database menggunakan model dan method Prisma.

## 7. Kesimpulan

Connector seperti `mysql2` digunakan untuk berkomunikasi secara langsung dengan database menggunakan query SQL. Sementara itu, Prisma merupakan ORM yang menyediakan lapisan abstraksi untuk mempermudah aplikasi dalam berinteraksi dengan database.

Pada contoh jumlah jadwal, kode awal pada modul masih menggunakan array `jadwal` dan menghitung jumlah data dengan `jadwal.length`.

Jika menggunakan database, operasi tersebut dapat dilakukan menggunakan raw SQL melalui `mysql2` atau menggunakan Prisma dengan method `findMany()`.

Raw SQL memberikan kontrol langsung terhadap query database, tetapi programmer perlu memperhatikan keamanan input dan risiko SQL Injection. Prisma dan Sequelize menyediakan mekanisme query terstruktur dan parameterisasi yang dapat membantu mengurangi risiko tersebut.

Dengan demikian, penggunaan connector dan ORM memiliki pendekatan yang berbeda dalam mengakses database, tetapi keduanya dapat digunakan untuk memenuhi kebutuhan aplikasi.