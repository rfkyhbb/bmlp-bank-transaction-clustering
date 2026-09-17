# Segmentasi Nasabah Bank & Prediksi Cluster

Clustering nasabah bank berdasarkan pola transaksi menggunakan **K-Means**, dilanjutkan dengan model klasifikasi (**Decision Tree** & **Random Forest**) untuk memprediksi cluster nasabah baru tanpa perlu menjalankan ulang proses clustering dari awal.

## Dataset
Data transaksi nasabah bank (2.537 baris sebelum cleaning), mencakup detail transaksi (jumlah, tipe, durasi), data demografis nasabah (usia, lokasi, pekerjaan), serta metadata identitas (ID transaksi/akun/perangkat, IP address, tanggal — dibuang saat preprocessing).

## Metodologi
1. **EDA** — statistik deskriptif, matriks korelasi, distribusi tiap fitur numerik
2. **Preprocessing** — handling missing values & duplikat, drop kolom identifier, label encoding fitur kategorikal, outlier removal (metode IQR), feature scaling (StandardScaler)
3. **Clustering** — K-Means, jumlah cluster ditentukan via Elbow Method (Silhouette Score)
4. **Interpretasi Cluster** — analisis karakteristik tiap cluster berdasarkan agregasi statistik (mean/min/max)
5. **Klasifikasi** — Decision Tree & Random Forest, dievaluasi dengan accuracy/precision/recall/F1-score

## ⚠️ Catatan & Keterbatasan
- Elbow Method tidak menunjukkan titik siku yang tegas (silhouette score turun monoton seiring k bertambah) — dataset ini kemungkinan tidak memiliki struktur cluster natural yang kuat. k=2 dipilih berdasarkan skor silhouette tertinggi.
- Cluster yang terbentuk didominasi oleh fitur `Location`, bukan kombinasi pola perilaku transaksi — akibat *scale imbalance*: kolom hasil `LabelEncoder` (termasuk `Location`, rentang 0–42) tidak ikut ter-*scale* bersama fitur numerik asli sebelum training K-Means.
- Karena `Location` juga dipakai sebagai fitur prediksi, akurasi 100% pada model klasifikasi **bukan indikasi performa model yang unggul** — melainkan konsekuensi *trivial recoverability*, karena target (cluster) pada dasarnya identik secara fungsional dengan `Location` itu sendiri.
- Project ini dikerjakan sebagai submission Dicoding *Belajar Machine Learning untuk Pemula*, mengikuti kriteria penilaian bertingkat (Basic/Skilled/Advanced) yang telah ditentukan.

## Tools
Python · pandas · scikit-learn · yellowbrick · seaborn · matplotlib

## Struktur File
```
├── [Clustering]_Submission_Akhir_BMLP_Rifky_Habibie.ipynb
├── [Klasifikasi]_Submission_Akhir_BMLP_Rifky_Habibie.ipynb
├── model_clustering.h5
├── decision_tree_model.h5
├── explore_RandomForest_classification.h5
└── data_clustering.csv
```
