Berikut adalah draf file `README.md` yang lengkap, terstruktur, dan profesional untuk repositori GitHub proyek UTS Graph Analytics ini:

```markdown
# 🛒 RetailRocket Graph Analytics & Recommendation System

Proyek ini berfokus pada pembangunan database graf, analisis jaringan interaksi e-commerce, serta implementasi sistem rekomendasi produk (*Item-based Collaborative Filtering*) menggunakan **Neo4j**, **Python**, dan dataset **RetailRocket**.

---

## 📌 Fitur Utama

- **Data Pipeline & Ingestion**: Pengolahan dataset RetailRocket dan *batch import* berbasis pola `FOREACH` Cypher ke Neo4j.
- **Graph Indexing & Constraints**: Penerapan *unique constraints* pada simpul `:Visitor` dan `:Item` untuk efisiensi kueri.
- **Vector Space Modelling (VSM)**: Proyeksi ruang vektor interaksi pengguna-produk (*User-Item*) dan *Item Co-occurrence*.
- **Similarity Computation**: Perhitungan *Cosine Similarity* menggunakan Scikit-Learn dan penulisan kembali (*write back*) relasi `:SIMILAR` ke dalam database Neo4j.
- **Graph-based Recommendation Engine**: Algoritma $k$-Nearest Neighbors (KNN) berbasis *Item-Item Collaborative Filtering*.
- **Evaluation Metrics**: Evaluasi performa sistem rekomendasi menggunakan metrik **Hit@5** dan **NDCG@5**.

---

## 🛠️ Teknologi & Dependensi

* **Database**: Neo4j (Local Instance / Bolt Protocol)
* **Language**: Python 3.12+
* **Libraries**:
  * `neo4j` (Official Python Driver 5.x)
  * `pandas`, `numpy`
  * `scipy` (Sparse Matrix Operations)
  * `scikit-learn` (Cosine Similarity)
  * `networkx`, `matplotlib` (Graph Visualization)

---

## 📂 Struktur Repositori

```text
├── archive/                   # Dataset mentah RetailRocket (CSV)
├── events_filtered.csv        # Dataset interaksi yang sudah difilter
├── import_retailrocket.ipynb  # Main Jupyter Notebook (Modul 1.1 - 2.2)
├── driver.py                  # Modul koneksi Neo4j Driver
├── requirements.txt           # Daftar dependensi Python
└── README.md                  # Dokumentasi Proyek

```

---

## 🚀 Panduan Memulai (*Quick Start*)

### 1. Prasyarat System

* **Neo4j Desktop / Server** sudah berjalan di lokal (`bolt://127.0.0.1:7687`).
* Python versi 3.10 atau yang lebih baru.

### 2. Setup Virtual Environment & Dependensi

```bash
# Clone repositori
git clone [https://github.com/username/retailrocket-graph-analytics.git](https://github.com/username/retailrocket-graph-analytics.git)
cd retailrocket-graph-analytics

# Buat virtual environment
python -m venv .venv

# Aktivasi virtual environment
# Windows:
.venv\Scripts\activate
# Linux/MacOS:
source .venv/bin/activate

# Install dependensi
pip install -r requirements.txt

```

### 3. Konfigurasi Database

Pastikan kredensial Neo4j pada notebook atau `driver.py` telah disesuaikan dengan instans lokal kamu:

```python
URI = "bolt://127.0.0.1:7687"
AUTH = ("neo4j", "password_kamu")

```

---

## 📊 Ringkasan Subgraph & Komposisi Data

Setelah impor data dan pembersihan simpul residual, berikut adalah komposisi akhir jaringan di Neo4j:

| Tipe Simpul (*Node*) | Total Nodes | Tipe Relasi (*Edge*) | Total Relations |
| --- | --- | --- | --- |
| **`Visitor`** | 804,234 | **`VIEWED`** | 4,443,520 |
| **`Item`** | 183,860 | **`ADDED_TO_CART`** | 113,371 |
|  |  | **`BOUGHT`** | 36,909 |
|  |  | **`SIMILAR`** | 31 |

---

## 📈 Metrik Evaluasi Sistem Rekomendasi

Sistem rekomendasi diuji menggunakan strategi evaluasi berbasis temporal (P1 untuk *training* dan P2 untuk *testing*):

* **Hit@5**: Mengukur presisi ketersediaan minimal satu item relevan pada Top-5 rekomendasi.
* **NDCG@5**: Mengukur efektivitas peringkat (*ranking quality*) item yang direkomendasikan.

---

## 📝 Lisensi & Penulis

* **Penulis**: Kevin Febrian Widhiarta
* **Program Studi**: Sains Data - Universitas Negeri Surabaya (UNESA)

```

```
