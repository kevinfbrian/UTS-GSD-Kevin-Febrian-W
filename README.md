# E-Commerce Graph Recommendation System (RetailRocket)

Proyek ini mengimplementasikan sistem rekomendasi produk berbasis graf (Graph-Based Recommender System) menggunakan dataset RetailRocket, Neo4j, dan Python. Pendekatan yang digunakan adalah Item-Based Collaborative Filtering dengan pemodelan ruang vektor (Vector Space Modelling) dan algoritma k-Nearest Neighbors (k-NN).

## Ringkasan Proyek

Sistem ini mentransformasikan data transaksi dan interaksi pengguna e-commerce dari bentuk relasional/tabular menjadi struktur graf unipartit dan bipartite. Melalui proyeksi ini, dilakukan perhitungan kesamaan produk (Cosine Similarity) yang dituliskan kembali (write-back) ke dalam basis data graf untuk menghasilkan rekomendasi item yang relevan secara real-time.

## Struktur Direktori

* `README.md` : Berkas dokumentasi utama proyek.
* `UTS GSD_Kevin Febrian W_025.ipynb` : Jupyter Notebook berisi alur kerja lengkap dari persiapan data, pembuatan graf di Neo4j, ekstraksi VSM, hingga evaluasi rekomendasi.
* `events_filtered.zip` : Arsip dataset interaksi e-commerce yang telah difilter berdasarkan rentang waktu.
* `requirements.txt` : Daftar dependensi pustaka Python yang diperlukan.

## Prasyarat dan Lingkungan Kerja

* Python 3.10 atau versi lebih baru
* Neo4j Database Server (Local Instance Desktop atau Community Edition)
* Protokol Bolt aktif pada port 7687

## Panduan Instalasi dan Penggunaan

1. Clone repositori ini ke direktori lokal:
git clone [https://github.com/username/repository-name.git](https://github.com/username/repository-name.git)
cd repository-name
2. Ekstrak berkas dataset:
Pastikan berkas `events_filtered.zip` diekstrak ke direktori utama sehingga menghasilkan berkas `events_filtered.csv`.
3. Buat dan aktifkan lingkungan virtual:
python -m venv .venv
source .venv/bin/activate  # Untuk Linux/macOS
.venv\Scripts\activate     # Untuk Windows
4. Pasang seluruh dependensi yang dibutuhkan:
pip install -r requirements.txt
5. Pastikan layanan Neo4j telah berjalan dan sesuaikan kredensial koneksi (URI, Username, Password) di dalam berkas notebook:
URI = "bolt://127.0.0.1:7687"
AUTH = ("neo4j", "password_anda")
6. Buka dan jalankan berkas `UTS GSD_Kevin Febrian W_025.ipynb` secara berurutan menggunakan Jupyter Notebook atau VS Code.

## Metodologi dan Alur Kerja

1. Ingesti Data dan Konstruksi Graf
* Pembuatan simpul Visitor dan Item.
* Pembentukan relasi interaksi: VIEWED, ADDED_TO_CART, dan BOUGHT.
* Pembuatan indeks unik pada Visitor(visitorId) dan Item(itemId) untuk mengoptimalkan kinerja query Cypher.


2. Pemodelan Ruang Vektor (VSM)
* Konstruksi matriks interaksi User-Item.
* Transpose matriks untuk mendapatkan VSM Item-Item.
* Analisis keterpencilan matriks (Sparsity) dan visualisasi sub-graf menggunakan NetworkX.


3. Perhitungan Kesamaan dan Write-Back
* Perhitungan Cosine Similarity pada simpul Item yang aktif.
* Eliminasi nilai self-similarity pada diagonal utama.
* Penulisan kembali pasangan item dengan skor kesamaan tertinggi ke basis data Neo4j menggunakan relasi :SIMILAR.


4. Rekomendasi k-NN dan Evaluasi
* Pengambilan item k-Nearest Neighbors berbasis relasi :SIMILAR.
* Evaluasi performa sistem rekomendasi menggunakan metrik Hit@5 dan NDCG@5 pada split data pengujian.



## Hasil Evaluasi

* Graf hasil proyeksi berhasil menyimpan keterhubungan antar-item secara efisien tanpa membebani kapasitas memori.
* Metrik Hit@5 dan NDCG@5 mengonfirmasi bahwa pendekatan Item-Based Collaborative Filtering memberikan urutan rekomendasi yang presisi untuk pengguna aktif.
