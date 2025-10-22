Tentu, saya bisa membuatkan file `README.md` untuk proyek Anda berdasarkan file-file yang telah disediakan.

Berikut adalah isi file `README.md` yang mencakup semua poin yang Anda minta:

-----

# API Manajemen Obat (Responsi Modul 1)

## 1\. Deskripsi Umum Proyek

Proyek ini adalah sebuah RESTful API sederhana yang dibangun menggunakan **Node.js** dan **Express.js** untuk mengelola data inventaris obat di sebuah apotek atau fasilitas kesehatan. API ini terhubung ke database **Supabase** untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada tiga sumber daya utama: Obat-obatan (`medications`), Kategori Obat (`categories`), dan Pemasok (`suppliers`).

Proyek ini dikonfigurasi untuk *deployment* di **Vercel**.

## 2\. Tujuan dan Fitur Utama

Tujuan utama dari API ini adalah untuk menyediakan serangkaian *endpoint* yang terstruktur untuk mengelola data yang saling terkait.

Fitur utama meliputi:

  * **Manajemen Obat (`/api/medications`):**
      * Menambah data obat baru (termasuk SKU, nama, deskripsi, harga, kuantitas).
      * Melihat daftar semua obat.
      * Melihat detail spesifik obat berdasarkan ID (termasuk data kategori dan pemasok terkait).
      * Memperbarui data obat.
      * Menghapus data obat.
  * **Manajemen Kategori (`/api/categories`):**
      * Menambah kategori obat baru.
      * Melihat semua kategori.
      * Melihat detail kategori berdasarkan ID.
      * Memperbarui nama kategori.
      * Menghapus kategori.
  * **Manajemen Pemasok (`/api/suppliers`):**
      * Menambah data pemasok baru.
      * Melihat semua pemasok.
      * Melihat detail pemasok berdasarkan ID.
      * Memperbarui data pemasok.
      * Menghapus data pemasok.

## 3\. Struktur Data

API ini mengelola 3 tabel utama di Supabase:

### `categories`

| Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, digenerasi otomatis oleh Supabase. |
| `name` | `text` | Nama kategori (misal: "Obat Keras", "Vitamin"). |

### `suppliers`

| Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, digenerasi otomatis oleh Supabase. |
| `name` | `text` | Nama perusahaan pemasok. |
| `email` | `text` | Email kontak pemasok. |
| `phone` | `text` | Nomor telepon kontak pemasok. |

### `medications`

| Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, digenerasi otomatis oleh Supabase. |
| `sku` | `text` | *Stock Keeping Unit* unik untuk obat. |
| `name` | `text` | Nama obat (misal: "Paracetamol 500mg"). |
| `description` | `text` | Deskripsi singkat obat. |
| `price` | `number` | Harga obat. |
| `quantity` | `number` | Jumlah stok obat. |
| `category_id` | `uuid` | Foreign Key ke tabel `categories`. |
| `supplier_id` | `uuid` | Foreign Key ke tabel `suppliers`. |

## 4\. Langkah Instalasi dan Menjalankan

### Prasyarat

  * [Node.js](https://nodejs.org/) (v18 atau lebih baru direkomendasikan).
  * Akun [Supabase](https://supabase.com/) untuk mendapatkan URL dan Key.

### Instalasi Lokal

1.  **Clone repositori ini:**

    ```bash
    git clone [URL_REPOSITORI_ANDA]
    cd [NAMA_FOLDER_PROYEK]
    ```

2.  **Install dependensi:**

    ```bash
    npm install
    ```

3.  **Konfigurasi Environment Variables:**

      * Buat file `.env` di *root* proyek dengan menyalin dari `.env.example`.
      * Isi file `.env` dengan kredensial Supabase Anda:
        ```ini
        SUPABASE_URL=URL_SUPABASE_ANDA
        SUPABASE_KEY=API_KEY_SUPABASE_ANDA
        PORT=3000
        ```

4.  **Menjalankan API (Mode Development):**

      * Skrip ini akan menggunakan `nodemon` untuk me-restart server secara otomatis saat ada perubahan file.

    <!-- end list -->

    ```bash
    npm run dev
    ```

    Server akan berjalan di `http://localhost:3000`.

5.  **Menjalankan API (Mode Produksi):**

    ```bash
    npm start
    ```

## 5\. Dokumentasi API (Contoh Request & Response)

Berikut adalah contoh penggunaan *endpoint* utama.

**Base URL (Lokal):** `http://localhost:3000`
**Base URL (Vercel):** `https://create-api-medication-if5f.vercel.app`

-----

### Kategori (`/api/categories`)

#### `POST /api/categories`

Membuat kategori baru.

  * **Request Body:**

    ```json
    {
      "name": "Vitamin dan Suplemen"
    }
    ```

  * **Response (201 Created):**

    ```json
    {
      "id": "a1b2c3d4-xxxx-xxxx-xxxx-fakerandomid",
      "created_at": "2024-10-20T10:30:00.123456+00:00",
      "name": "Vitamin dan Suplemen"
    }
    ```

-----

### Pemasok (`/api/suppliers`)

#### `POST /api/suppliers`

Membuat pemasok baru.

  * **Request Body:**

    ```json
    {
      "name": "PT. Kimia Farma",
      "email": "kontak@kimiafarma.co.id",
      "phone": "081234567890"
    }
    ```

  * **Response (201 Created):**

    ```json
    {
      "id": "b2c3d4e5-xxxx-xxxx-xxxx-fakerandomid",
      "created_at": "2024-10-20T10:35:00.123456+00:00",
      "name": "PT. Kimia Farma",
      "email": "kontak@kimiafarma.co.id",
      "phone": "081234567890"
    }
    ```

-----

### Obat (`/api/medications`)

#### `POST /api/medications`

Membuat data obat baru.

  * **Request Body:**

    ```json
    {
      "sku": "MED-001",
      "name": "Paracetamol 500mg",
      "description": "Obat penurun panas dan pereda nyeri",
      "price": 15000,
      "quantity": 100,
      "category_id": "a1b2c3d4-xxxx-xxxx-xxxx-fakerandomid",
      "supplier_id": "b2c3d4e5-xxxx-xxxx-xxxx-fakerandomid"
    }
    ```

  * **Response (201 Created):**

    ```json
    {
      "id": "c3d4e5f6-xxxx-xxxx-xxxx-fakerandomid",
      "created_at": "2024-10-20T10:40:00.123456+00:00",
      "sku": "MED-001",
      "name": "Paracetamol 500mg",
      "description": "Obat penurun panas dan pereda nyeri",
      "price": 15000,
      "quantity": 100,
      "category_id": "a1b2c3d4-xxxx-xxxx-xxxx-fakerandomid",
      "supplier_id": "b2c3d4e5-xxxx-xxxx-xxxx-fakerandomid"
    }
    ```

#### `GET /api/medications/:id`

Mendapatkan detail obat, kategori, dan pemasoknya (join).

  * **Request URL:** `GET /api/medications/c3d4e5f6-xxxx-xxxx-xxxx-fakerandomid`

  * **Response (200 OK):**

    ```json
    {
      "id": "c3d4e5f6-xxxx-xxxx-xxxx-fakerandomid",
      "sku": "MED-001",
      "name": "Paracetamol 500mg",
      "description": "Obat penurun panas dan pereda nyeri",
      "price": 15000,
      "quantity": 100,
      "categories": {
        "id": "a1b2c3d4-xxxx-xxxx-xxxx-fakerandomid",
        "name": "Obat Keras"
      },
      "suppliers": {
        "id": "b2c3d4e5-xxxx-xxxx-xxxx-fakerandomid",
        "name": "PT. Kimia Farma",
        "email": "kontak@kimiafarma.co.id",
        "phone": "081234567890"
      }
    }
    ```

## 6\. Link Deploy (Vercel)

API ini telah di-deploy ke Vercel dan dapat diakses melalui URL berikut:

**[[https://create-api-medication-if5f.vercel.app](https://www.google.com/url?sa=E&source=gmail&q=https://create-api-medication-if5f.vercel.app)](https://vercel.com/letsdothis-projects/responsi-modul-1-prak-ppb-qgp1)**

(Catatan: Link diambil dari file koleksi Postman yang disediakan).

