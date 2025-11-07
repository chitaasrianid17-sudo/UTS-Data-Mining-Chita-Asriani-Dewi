# UTS-Data-Mining-Chita-Asriani-Dewi
UTS Data Mining- Analisis Model Untuk Klasifikasi Dataset Wine Quality
# 🧠 Klasifikasi Kualitas Data Menggunakan Random Forest dan Ensemble Learning

## 📋 Deskripsi Proyek
Proyek ini merupakan bagian dari **Ujian Tengah Semester (UTS)** untuk mata kuliah *Machine Learning*.  
Tujuan proyek ini adalah membangun model klasifikasi untuk memprediksi **kualitas data** berdasarkan fitur numerik menggunakan algoritma **Random Forest**, **Gradient Boosting**, serta pendekatan **Ensemble Model (Voting Classifier)**.

Proses dilakukan secara sistematis, mulai dari pembersihan data, eksplorasi, pembuatan fitur baru (*feature engineering*), pelatihan model, tuning parameter, hingga evaluasi performa model menggunakan metrik evaluasi seperti *accuracy*, *precision*, *recall*, *f1-score*, dan *AUC*.

---

## 🧩 Dataset
- **Data Training:** `data_training.csv`  
- **Data Testing:** `data_testing.csv`  

Dataset berisi fitur-fitur numerik yang menggambarkan karakteristik data (misalnya kandungan kimia), dengan label target berupa `quality`.  
Beberapa fitur baru dibuat untuk memperkaya informasi melalui proses **feature engineering**, yaitu:
- `acidity_ratio` = perbandingan antara fixed acidity dan volatile acidity  
- `density_alcohol_ratio` = perbandingan antara density dan alcohol  
- `total_acidity` = total dari fixed acidity, citric acid, dan volatile acidity  

---

## ⚙️ Tahapan Proses

### 1️⃣ Data Cleaning
- Mengecek *missing values* dan menghapus kolom yang tidak informatif (fitur dengan satu nilai unik atau korelasi sangat tinggi > 0.9).  
- Menyiapkan data training (`X`, `y`) dan data testing (`X_test`).

### 2️⃣ Feature Engineering
- Menambahkan fitur baru untuk meningkatkan kualitas representasi data.

### 3️⃣ Standardisasi Data
- Melakukan *StandardScaler* agar semua fitur memiliki skala yang sebanding.

### 4️⃣ Pembagian Data & Penyeimbangan Kelas
- Data dibagi menjadi **80% training** dan **20% validation** menggunakan `train_test_split` dengan *stratify*.  
- Diterapkan **SMOTE** hanya pada data training untuk menangani ketidakseimbangan kelas.

### 5️⃣ Hyperparameter Tuning
- Menggunakan **GridSearchCV** untuk mencari kombinasi parameter terbaik dari *Random Forest* dengan *class_weight = balanced*.

### 6️⃣ Ensemble Model
- Menggabungkan dua model terbaik (**Random Forest** dan **Gradient Boosting**) menggunakan **Voting Classifier (soft voting)** agar hasil prediksi lebih stabil dan akurat.

### 7️⃣ Evaluasi Model
- Mengukur performa model menggunakan metrik:
  - Accuracy  
  - Precision  
  - Recall  
  - F1-Score  
  - AUC  
- Ditampilkan dalam bentuk **confusion matrix**, **ROC curve**, dan **grafik evaluasi**.

---

## 📊 Hasil dan Interpretasi

### 🎯 Evaluasi Model Ensemble (RF + GB)

| Metrik | Nilai | Persentase |
|:-------|:-------|:-----------|
| Accuracy | 0.558 | 55.8% |
| Precision | 0.352 | 35.2% |
| Recall | 0.326 | 32.6% |
| F1-Score | 0.336 | 33.6% |
| AUC | 0.778 | 77.8% |

**Interpretasi:**  
- Nilai *AUC* yang tinggi (0.778) menunjukkan kemampuan model cukup baik dalam membedakan antar kelas.  
- Nilai *accuracy* masih moderat (0.558), menunjukkan masih terdapat ruang untuk perbaikan, misalnya dengan tuning tambahan atau seleksi fitur lebih optimal.

---

### 🌲 Feature Importance (Random Forest)

Fitur paling berpengaruh dalam menentukan hasil prediksi:

| Peringkat | Fitur | Importance |
|:-----------|:------|:------------|
| 1 | acidity_ratio | tertinggi |
| 2 | sulphates | tinggi |
| 3 | volatile acidity | tinggi |
| 4 | alcohol | menengah |
| 5 | density_alcohol_ratio | menengah |

**Interpretasi:**  
Fitur seperti `acidity_ratio`, `sulphates`, dan `volatile acidity` memiliki kontribusi terbesar dalam klasifikasi kualitas, sedangkan `residual sugar` dan `total_acidity` berperan lebih kecil.

---

### 🧩 Validasi dengan Stratified K-Fold

**Interpretasi:**  
Cross-validation menunjukkan bahwa model memiliki tingkat akurasi rata-rata sebesar **64.53%** di berbagai subset data.  
Hal ini berarti model cukup stabil dan tidak terlalu bergantung pada pembagian data tertentu.

---

## 🧾 Kesimpulan
- Model Random Forest dan Ensemble Learning memberikan performa cukup stabil dengan AUC tinggi.  
- Fitur hasil *feature engineering* seperti `acidity_ratio` terbukti penting dalam meningkatkan kualitas prediksi.  
- Proses tuning dan balancing data menggunakan SMOTE berhasil menyeimbangkan distribusi kelas.  
- Masih ada potensi peningkatan akurasi dengan optimasi parameter lebih lanjut atau menambah jumlah data latih.

---

