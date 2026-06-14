# Consumer Complaint Sentiment Analysis

Proyek ini menganalisis **Consumer Complaint Database** dari CFPB menggunakan **Apache Spark** untuk menangani dataset besar, melakukan eksplorasi data, analisis tren, visualisasi topik keluhan, word cloud, dan klasifikasi sentimen narasi keluhan.

Notebook ini dirancang untuk memproses data skala besar dengan pendekatan distributed processing, sehingga lebih cocok dibanding pendekatan pandas murni untuk dataset jutaan baris.

## Overview

Tujuan utama proyek ini adalah menjawab beberapa pertanyaan analisis:

1. Keluhan apa yang paling sering muncul?
2. Apakah jumlah keluhan meningkat atau menurun dari waktu ke waktu?
3. Jenis masalah apa yang paling sering dikeluhkan pelanggan?
4. Bagaimana sentimen narasi keluhan konsumen?

Pipeline yang digunakan mencakup:

- Pembacaan data CSV menggunakan Spark DataFrame
- Seleksi kolom dan pembersihan data awal
- Optimasi `repartition()` dan `persist()`
- Analisis frekuensi keluhan dan tren waktu
- Word cloud berbasis sample data
- Labeling sentimen menggunakan VADER
- Feature engineering dengan TF-IDF
- Training model klasifikasi dengan Logistic Regression dan Random Forest

## Fitur Utama

- Pemrosesan data besar dengan Apache Spark
- Cache dan checkpoint ke Parquet untuk mempercepat iterasi
- Sampling untuk tugas yang berat seperti word cloud dan labeling sentimen
- Visualisasi hasil analisis ke file gambar
- Perbandingan performa dua model machine learning

## Teknologi yang Digunakan

- Python
- Apache Spark / PySpark
- pandas
- NumPy
- Matplotlib
- Seaborn
- WordCloud
- VADER Sentiment
- PyArrow

## Struktur Proyek

Hasil eksekusi notebook akan menyimpan artefak proyek ke folder seperti:

- `checkpoints/` untuk file Parquet dan hasil intermediate
- `models/` untuk model Spark ML yang sudah dilatih
- `visualizations/` untuk output grafik dan gambar

## Cara Menjalankan Proyek

### 1. Siapkan Python Environment

Disarankan memakai virtual environment.

```bash
python -m venv .venv
source .venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install pyspark==3.4.1 wordcloud vaderSentiment pyarrow matplotlib seaborn pandas numpy
```

### 3. Siapkan Dataset

Pastikan file dataset `complaints.csv` tersedia di path yang sesuai dengan konfigurasi di notebook.

Di notebook ini, variabel `DATA_PATH` masih mengarah ke path lokal Windows. Jika kamu menjalankan di macOS, Linux, atau Colab, sesuaikan path tersebut terlebih dahulu.

### 4. Jalankan Notebook

Buka notebook `Consumer_Complaint_Sentiment_Analysis (1).ipynb` lalu jalankan cell secara berurutan dari atas ke bawah.

Jika memakai Jupyter Notebook atau VS Code:

```bash
jupyter notebook
```

atau

```bash
code .
```

### 5. Lihat Output

Setelah selesai, hasil berikut akan tersedia:

- grafik top complaint categories
- tren keluhan bulanan dan tahunan
- visualisasi issue/sub-issue
- word cloud dari narasi keluhan
- distribusi sentimen
- confusion matrix dan evaluasi model
- model tersimpan di folder `models/`

## Catatan Penting

- Notebook ini memakai Spark, jadi performa tergantung RAM, jumlah core, dan konfigurasi environment.
- Beberapa tahap memakai `toPandas()` dan `collect()` untuk hasil agregasi kecil. Itu aman untuk top-N data, tetapi tidak ideal untuk output yang sangat besar.
- Untuk Word Cloud dan sentimen, notebook memakai sampling agar proses lebih ringan.

## Output yang Dihasilkan

- `01_top_complaints.png`
- `02_complaint_trend.png`
- `03_issue_analysis.png`
- `04_wordcloud.png`
- `05_sentiment_distribution.png`
- `06_cm_tfidf_lr.png`
- `07_cm_tfidf_rf.png`
- `08_model_comparison.png`
- `09_optimization.png`

## Kesimpulan

Proyek ini menunjukkan bagaimana Spark dapat dipakai untuk analisis sentimen dan eksplorasi dataset besar secara efisien, mulai dari data loading, preprocessing, analisis statistik, hingga machine learning.

Jika ingin, README ini masih bisa dikembangkan dengan:

- badge GitHub
- deskripsi dataset yang lebih formal
- contoh screenshot hasil visualisasi
- bagian `Requirements` dan `License`
