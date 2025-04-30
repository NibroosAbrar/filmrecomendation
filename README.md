# 🎬 Movie Recommendation System

Sistem rekomendasi film berbasis konten menggunakan dataset IMDb yang berisi informasi genre, deskripsi, dan rating film. Proyek ini dirancang untuk membantu pengguna menemukan film yang sesuai dengan preferensinya melalui analisis kesamaan konten.

---

## 📝 Project Overview

Dalam era digital, platform streaming menyediakan ribuan judul film, menjadikan proses pencarian tontonan yang sesuai menjadi tantangan. Sistem rekomendasi muncul sebagai solusi untuk menyaring dan menyarankan film yang relevan bagi pengguna.

Menurut *Statista (2023)*, lebih dari 70% pengguna platform streaming bergantung pada rekomendasi otomatis untuk menemukan konten baru. Dengan demikian, sistem rekomendasi yang baik dapat meningkatkan kepuasan pengguna dan durasi menonton. Proyek ini berfokus pada pengembangan sistem rekomendasi berbasis konten (content-based filtering), yang memanfaatkan deskripsi dan genre film untuk memberikan saran yang dipersonalisasi.

---

## 💼 Business Understanding

### 🔍 Problem Statement

- Bagaimana cara memberikan rekomendasi film yang relevan berdasarkan kemiripan konten film seperti genre dan sinopsis?

### 🎯 Goals

- Mengembangkan sistem rekomendasi berbasis konten yang dapat menyarankan film serupa berdasarkan genre dan deskripsi sinopsis.
- Memberikan rekomendasi top-N film yang paling relevan bagi pengguna.

### 🛠️ Solution Approach

- **Content-Based Filtering**  
  Sistem membandingkan fitur konten film seperti `genres` dan `sinopsis` menggunakan teknik TF-IDF (Term Frequency–Inverse Document Frequency) dan Cosine Similarity untuk mengukur tingkat kesamaan antarfilm. Film dengan nilai kesamaan tertinggi kemudian direkomendasikan kepada pengguna.

---

## 📊 Data Understanding

### 📥 Sumber Data

Dataset diambil dari:  
🔗 [IMDb Movie Dataset - GitHub](https://github.com/Rahmathidayat4299/dataset-movie-recomendation)

### 📐 Informasi Data

- Jumlah data: **1400 entri**
- Format: CSV
- Fitur:
  - `name`: Judul film
  - `year`: Tahun rilis
  - `movie_rated`: Kategori usia (misal: PG-13, R)
  - `run_length`: Durasi film
  - `genres`: Genre film
  - `release_date`: Tanggal rilis
  - `rating`: Skor rating pengguna
  - `num_raters`: jumlah penilaian
  - `num_reviews`: Jumlah ulasan
  - `review_url`: Link ulasan

### 📈 Visualisasi Data

Beberapa visualisasi eksploratif digunakan untuk memahami distribusi dan hubungan antarfitur:

#### 🎞️ Distribusi Genre

```python
# Visualisasi genre terbanyak
import matplotlib.pyplot as plt
import seaborn as sns

genre_counts = df['genres'].value_counts().head(10)
sns.barplot(x=genre_counts.values, y=genre_counts.index)
plt.title("Top 10 Genre Paling Umum")
plt.xlabel("Jumlah Film")
plt.ylabel("Genre")
plt.show()
```

#### ⭐ Distribusi Rating

```python
sns.histplot(df['rating'], bins=10, kde=True)
plt.title("Distribusi Rating Film")
plt.xlabel("Rating")
plt.ylabel("Jumlah Film")
plt.show()
```

---

## 🧹 Data Preparation

Tahapan ini bertujuan untuk menyiapkan data agar optimal digunakan oleh model rekomendasi. Berikut adalah langkah-langkah preprocessing yang dilakukan:

### 1. Menghapus Data Duplikat
- Menggunakan `df.drop_duplicates()` untuk menghapus entri dengan nilai duplikat pada kolom `name`, `genres`, dan `description`.

### 2. Menghapus Kolom yang Tidak Relevan
- Menghapus kolom seperti `review_url`, `release_date`, dan `run_length` menggunakan `df.drop()` karena tidak berkontribusi pada sistem rekomendasi.

### 3. Encoding Kolom Genres
- Menggunakan `OneHotEncoder` dari scikit-learn.
- Melakukan `fit_transform` pada kolom `genres` dan menggabungkannya kembali ke DataFrame asli menggunakan `concat`.

### 4. Ekstraksi Fitur Teks (TF-IDF)
- Menggabungkan kolom `name`, `genres`, dan `description` menjadi satu kolom teks gabungan bernama `features`.
- Menggunakan `TfidfVectorizer` untuk mengubah teks pada kolom `features` menjadi representasi numerik.

### 5. Menangani Missing Values (Secara Implisit)
- Mengonversi kolom `name`, `genres`, dan `description` menjadi string menggunakan `astype(str)` untuk menghindari error ketika memproses data yang mengandung nilai kosong.

### 6. Memastikan Kolom Name sebagai String
- Menggunakan `notnull()` dan `astype(str)` untuk memastikan bahwa kolom `name` tidak kosong dan bertipe string.


---

## 🤖 Modeling and Result

### 🔍 Pendekatan

Menggunakan algoritma **TF-IDF + Cosine Similarity** untuk menghitung kesamaan antar film berdasarkan konten mereka. Model akan merekomendasikan film yang paling mirip dengan film pilihan pengguna.

### ✅ Hasil Rekomendasi (Top-5)

Contoh output sistem:

```
Film input: Avatar

Top 5 rekomendasi:
1. Thor
2. Fantastic Four
3. The Mummy
4. Aquaman
5. Warcraft

```

### 📌 Kelebihan & Kekurangan

| Aspek | Penjelasan |
|-------|------------|
| ✅ Kelebihan | Tidak membutuhkan interaksi pengguna lain, cepat digunakan pada dataset kecil |
| ❌ Kekurangan | Tidak bisa menyarankan film baru yang berbeda dari histori pengguna, terbatas pada informasi konten |

---


## 📏 Evaluation

### 📐 Metrik Evaluasi

- **Cosine Similarity Score**: Ukuran kesamaan antara film input dan rekomendasi.
- **Precision@K** (jika ada ground truth pengguna): Mengukur seberapa relevan top-K rekomendasi.

### 🧮 Rumus Cosine Similarity:

$$\text{Cosine Similarity} = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$

Dimana:  
- $\mathbf{A}$ dan $\mathbf{B}$ adalah vektor TF-IDF dari dua film.  
- $\|\mathbf{A}\|$ dan $\|\mathbf{B}\|$ adalah norma (magnitudo) dari masing-masing vektor.  
- $\mathbf{A} \cdot \mathbf{B}$ adalah hasil dot product dari vektor tersebut.

### 📊 Hasil Evaluasi

```bash
<ipython-input-85-1bd521b417d7>:6: FutureWarning: Series.__getitem__ treating keys as positions is deprecated.
  idx = int(idx[0]) if len(idx) > 0 else None
Precision@10: 0.0136
Recall@10: 0.0789
Average Cosine Similarity Score: 0.3091
```

### 🧾 Evaluasi dan Keterkaitan dengan Business Understanding

#### 1. 🎯 Apakah model menjawab problem statement?
**Problem statement**: Bagaimana cara memberikan rekomendasi film yang relevan berdasarkan kemiripan konten seperti genre dan sinopsis?

✅ Ya, model berhasil menjawab permasalahan tersebut.  
Dengan TF-IDF dan Cosine Similarity, sistem berhasil memberikan film yang mirip secara konten berdasarkan input pengguna.

#### 2. 🥅 Apakah model mencapai goals proyek?
- Mengembangkan sistem rekomendasi berbasis konten.
- Memberikan rekomendasi top-N film yang paling relevan.

**Evaluasi menunjukkan**:
- Precision@10: 0.0136
- Recall@10: 0.0789
- Cosine Similarity Score: 0.3091

Meskipun precision dan recall masih rendah, sistem tetap memberikan hasil relevan secara kualitatif.

#### 3. 🧠 Apakah solusi yang dirancang berdampak terhadap kebutuhan bisnis?
✅ Ya, karena sistem:
- Tidak membutuhkan data interaksi pengguna.
- Cocok untuk dataset kecil-menengah.
- Mudah dipahami dan diimplementasikan.

📌 Rekomendasi:
- Gunakan Word Embedding (Word2Vec/BERT) untuk vektorisasi yang lebih kontekstual.
- Gabungkan dengan metode collaborative filtering jika data pengguna tersedia.

### ✅ Kesimpulan Evaluasi

Sistem sudah menjawab tujuan bisnis, meskipun akurasi kuantitatif masih dapat ditingkatkan. Relevansi konten tetap dapat dipertahankan, dan pendekatan content-based efektif sebagai baseline.

