
# 🎬 Sistem Rekomendasi Film (Content-Based Filtering)

Proyek ini bertujuan untuk membangun sistem rekomendasi film menggunakan pendekatan **Content-Based Filtering** berbasis TF-IDF dan Cosine Similarity. Sistem akan merekomendasikan film berdasarkan kemiripan konten (judul dan deskripsi film), tanpa mempertimbangkan preferensi pengguna lain.

---

## 📌 Project Overview

### 📖 Latar Belakang
Masyarakat saat ini dihadapkan pada ribuan pilihan film dengan berbagai genre. Tanpa sistem rekomendasi, pengguna sering kebingungan memilih film yang sesuai preferensi mereka. Pendekatan content-based filtering membantu merekomendasikan film berdasarkan kesamaan deskripsi, genre, atau kata kunci dari film yang disukai sebelumnya.

Sistem ini bermanfaat untuk:
- Platform streaming yang ingin meningkatkan pengalaman pengguna.
- Aplikasi pencari film atau pengulas film.
- Pengguna individu yang ingin rekomendasi otomatis.

### 🔗 Sumber Referensi
- [Netflix Research](https://research.netflix.com/)
- [Towards Data Science: Content-Based Recommenders](https://towardsdatascience.com/content-based-recommender-systems-1c3c72ed7c6)

---

## 💼 Business Understanding

### ❓ Problem Statements
Bagaimana membangun sistem yang mampu memberikan rekomendasi film serupa berdasarkan deskripsi dan genre dari film yang disukai pengguna?

### 🎯 Goals
- Menghasilkan sistem rekomendasi berbasis konten yang sederhana dan akurat.
- Menyajikan 10 film teratas yang relevan berdasarkan input pengguna.

### 🧩 Solution Approach
- **Content-Based Filtering** menggunakan:
  - TF-IDF untuk ekstraksi fitur dari teks deskripsi film.
  - Cosine Similarity untuk menghitung kesamaan antar film.
- Collaborative Filtering tidak digunakan dalam proyek ini.

---

## 🧾 Data Understanding

### 📊 Dataset
Data diambil dari berbagai genre film, masing-masing dalam file CSV terpisah.

### 📥 Sumber Data:
Dataset tersedia dalam repositori GitHub:

```python
urls = [
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Action.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Adventure.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Animation.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Comedy.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Crime.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Drama.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Fantasy.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Horror.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Mystery.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Music.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Romance.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Sci-Fi.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/Thriller.csv',
    'https://raw.githubusercontent.com/Rahmathidayat4299/dataset-movie-recomendation/master/War.csv'
]
```

### 📑 Fitur Utama
- `Title`: Judul film
- `Overview`: Sinopsis atau deskripsi film
- `Genre`: Genre film (berdasarkan nama file)

### 📈 EDA Singkat
- Visualisasi distribusi film berdasarkan genre
- Frekuensi kata kunci dari sinopsis film
- Panjang rata-rata sinopsis per genre

---

## 🧹 Data Preparation

### 🔧 Tahapan
1. Penggabungan seluruh file CSV ke dalam satu DataFrame.
2. Pembersihan data: menghapus baris kosong dan duplikat.
3. Pembuatan fitur gabungan dari kolom `Title` dan `Overview`.
4. TF-IDF vectorization dari teks gabungan.

### 💡 Alasan:
- TF-IDF memerlukan teks bersih untuk hasil representasi vektor yang akurat.
- Pembersihan data meningkatkan kualitas hasil rekomendasi.

---

## 🧠 Modeling and Result

### 🔍 Pendekatan:
- Mengubah teks sinopsis film menjadi vektor TF-IDF.
- Menghitung Cosine Similarity antar film berdasarkan vektor.
- Menampilkan 10 film paling mirip dengan input film.

### 📋 Contoh Output:
Input: `"The Matrix"`  
Rekomendasi:
1. The Matrix Reloaded  
2. The Matrix Revolutions  
3. Inception  
4. Equilibrium  
...

### ⚖️ Kelebihan & Kekurangan
| Content-Based Filtering |
|-------------------------|
| ✅ Tidak memerlukan data pengguna lain |
| ✅ Cepat dan sederhana implementasinya |
| ❌ Rekomendasi terbatas pada fitur konten |
| ❌ Tidak bisa menyarankan film dari genre baru yang belum dilihat pengguna |

---

## 📈 Evaluation

### 📏 Metrik Evaluasi
- **Manual Inspection** (validasi kualitatif kesamaan hasil)
- **Precision@10** (jika tersedia data relevansi)

### 📐 Formula:
- **Cosine Similarity**:
  \[
  \cos(\theta) = \frac{A \cdot B}{||A|| \times ||B||}
  \]

---

## 🚀 Cara Menjalankan

```bash
# 1. Clone project
git clone https://github.com/username/movie-content-recommender.git
cd movie-content-recommender

# 2. Install library
pip install -r requirements.txt

# 3. Jalankan script
python app.py
```

---

## 👨‍💻 Teknologi
- Python (Pandas, Scikit-learn)
- TF-IDF Vectorizer
- Cosine Similarity
- Matplotlib & Seaborn (opsional)

---
