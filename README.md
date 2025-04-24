
# Movie Recommendation System - Content-Based Filtering

## Deskripsi Proyek
Proyek ini bertujuan untuk membuat sistem rekomendasi film menggunakan pendekatan Content-Based Filtering. Sistem ini memanfaatkan metadata film seperti judul, genre, dan rating untuk memberikan rekomendasi film yang mirip berdasarkan konten film tersebut.

## Struktur Data
Data film diambil dari berbagai genre film yang tersedia di GitHub. Setiap file CSV berisi data mengenai film dengan kolom-kolom seperti:
- **name**: Judul film
- **year**: Tahun rilis
- **rating**: Rating film
- **num_raters**: Jumlah rating
- **num_reviews**: Jumlah ulasan
- **genres**: Genre film (beberapa genre dapat dipisahkan dengan tanda semicolon)

## Langkah-langkah
1. **Impor Paket dan Library**:
   - Menggunakan berbagai pustaka seperti Pandas, NumPy, Scikit-learn, dan Matplotlib untuk analisis data, preprocessing, dan visualisasi.
   
2. **Pemuatan dan Penggabungan Data**:
   - Data film diambil dari repositori GitHub yang menyimpan berbagai genre film dan digabungkan menjadi satu dataset.

3. **Pemahaman Data**:
   - Data dieksplorasi untuk mengecek informasi dasar seperti ukuran dataset, tipe data, dan missing values.
   - Outlier dan korelasi antara fitur numerik juga diperiksa.

4. **Persiapan Data**:
   - Duplikasi data dihapus, dan kolom-kolom yang tidak relevan (seperti tanggal rilis dan URL ulasan) dihapus.
   - Kolom genre di-encode menggunakan OneHotEncoder untuk mengubah genre menjadi format yang dapat diproses oleh model.

5. **Ekstraksi Fitur dengan TF-IDF**:
   - Fitur film diekstrak dari kombinasi kolom 'title', 'genres', dan 'rating'. 
   - TF-IDF (Term Frequency-Inverse Document Frequency) digunakan untuk mewakili konten film dalam bentuk matriks numerik.

6. **Bangun Model**:
   - Sistem rekomendasi dibangun menggunakan teknik Content-Based Filtering berdasarkan kemiripan konten film. Cosine similarity digunakan untuk mengukur kesamaan antara film berdasarkan fitur yang diekstrak.

7. **Inferensi Model**:
   - Fungsi `recommend_movies` digunakan untuk memberikan rekomendasi film berdasarkan judul film yang diberikan.

## Penggunaan
Untuk memberikan rekomendasi film berdasarkan judul, Anda dapat menggunakan fungsi `recommend_movies`. Contoh:

```python
recommend_movies("Inception")
```

Ini akan mengembalikan daftar film yang serupa dengan "Inception".

## Instalasi dan Persyaratan
Pastikan Anda menginstal pustaka berikut sebelum menjalankan kode:
- `numpy`
- `pandas`
- `scikit-learn`
- `matplotlib`
- `seaborn`

Anda dapat menginstalnya menggunakan pip:

```
pip install numpy pandas scikit-learn matplotlib seaborn
```

## Penyimpanan dan Pengolahan Data
Data yang digunakan dalam proyek ini tersedia di GitHub dan akan diunduh secara otomatis ke dalam DataFrame pandas. Anda juga dapat menyimpan data gabungan ini dalam file CSV untuk penggunaan lebih lanjut.

## Kontribusi
Jika Anda memiliki saran atau ingin berkontribusi pada proyek ini, silakan ajukan pull request atau hubungi saya.

## Lisensi
Proyek ini dilisensikan di bawah [Lisensi MIT](https://opensource.org/licenses/MIT).
