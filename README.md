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
  - `description`: Sinopsis atau deskripsi film
  - `actors`: Aktor yang membintangi
  - `directors`: Sutradara

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

- **Text Cleaning**: Membersihkan deskripsi dari tanda baca, angka, dan kata tidak penting (stopwords).
- **TF-IDF Vectorization**: Mengubah teks deskripsi menjadi vektor numerik.
- **Feature Engineering**: Menggabungkan kolom genre dan nama menjadi satu fitur gabungan.
- **Normalisasi**: Menyesuaikan format data (misal: lowercase, strip whitespace).

📌 Proses ini penting untuk memastikan data dalam format yang sesuai agar algoritma rekomendasi dapat berjalan secara optimal.

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

## Mathematical Formula

### Cosine Similarity

\[
\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|}
\]

**Dimana:**

- \( A \) and \( B \) are the TF-IDF vectors of two products.
- \( \|A\| \) and \( \|B\| \) are the magnitudes (norms) of the vectors.
- \( A \cdot B \) is the dot product of the vectors.


Model dievaluasi secara kualitatif dengan melihat relevansi hasil terhadap film input.
