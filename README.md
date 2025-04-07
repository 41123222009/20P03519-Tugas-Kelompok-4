# Machine Learning Kelompok 4

## Dataset

Dataset yang digunakan adalah dataset `ckd-dataset-v2.csv`. Dataset `ckd-dataset-v2.csv` berisi data mengenai pasien yang diduga mengalami Chronic Kidney Disease (CKD), dengan total 200 entri dan 27 kolom. Berikut adalah deskripsi setiap kolom:
1. `bp (Diastolic)` (*int64*) - Tekanan darah diastolik pasien, dikodekan sebagai 0 (normal) dan 1 (tinggi).  
2. `bp limit` (*int64*) - Indikator apakah tekanan darah melewati batas normal.  
3. `sg` (*object*) - Nilai berat jenis urin dalam bentuk interval (misalnya, "1.009 - 1.011").  
4. `al` (*object*) - Tingkat albumin dalam urin, bisa berupa nilai seperti `< 0`, `≥ 4`, dll.  
5. `class` (*object*) - Kategori status CKD: `ckd` (terkena) atau `notckd` (tidak terkena).  
6. `rbc` (*int64*) - Sel darah merah dalam urin: 0 (normal), 1 (tidak normal).  
7. `su` (*object*) - Kadar gula dalam urin, dalam format teks seperti `< 0`.  
8. `pc` (*int64*) - Jumlah sel nanah (pus cells) dalam urin: 0 (tidak ada), 1 (ada).  
9. `pcc` (*int64*) - Gumpalan sel nanah: 0 (tidak ada), 1 (ada).  
10. `ba` (*int64*) - Kehadiran bakteri dalam urin: 0 (tidak), 1 (ada).  
11. `bgr` (*object*) - Kadar glukosa dalam darah (bentuk rentang nilai sebagai teks).  
12. `bu` (*object*) - Kadar urea dalam darah, dicatat dalam format teks numerik.  
13. `sod` (*object*) - Kadar natrium dalam darah, dalam bentuk teks angka.  
14. `sc` (*object*) - Kadar kreatinin dalam serum, nilai berbentuk string angka.  
15. `pot` (*object*) - Kadar kalium dalam darah.  
16. `hemo` (*object*) - Tingkat hemoglobin pasien.  
17. `pcv` (*object*) - Volume sel darah yang dipadatkan, dalam bentuk teks numerik.  
18. `rbcc` (*object*) - Jumlah sel darah merah, juga dicatat sebagai teks numerik.  
19. `wbcc` (*object*) - Jumlah sel darah putih dalam darah pasien.  
20. `htn` (*int64*) - Status hipertensi: 0 (tidak), 1 (ya).  
21. `dm` (*int64*) - Status diabetes: 0 (tidak), 1 (ya).  
22. `cad` (*int64*) - Riwayat penyakit jantung koroner: 0 (tidak), 1 (ya).  
23. `appet` (*int64*) - Nafsu makan: 0 (baik), 1 (buruk).  
24. `pe` (*int64*) - Pembengkakan (edema): 0 (tidak), 1 (ya).  
25. `ane` (*int64*) - Anemia: 0 (tidak), 1 (ya).  
26. `grf` (*object*) - Laju filtrasi glomerulus (GFR), dalam interval nilai sebagai teks.  
27. `age` (*object*) - Kelompok usia pasien, misalnya `< 12`, `12 - 20`, dst.

## 1. Eksplorasi Data

### *Missing Values*

Berdasarkan hasil analisis tidak ditemukan nilai yang hilang (*missing values*) dalam dataset. Ini berarti dataset bersih dan tidak memerlukan penanganan tambahan untuk mengatasi missing values.

### Visualisasi Data

#### A. Distiribusi Kelompok Usia berdasarkan Status CKD

<img src="Images/Image1.png">

Grafik tersebut menunjukkan distribusi kelompok usia pasien berdasarkan status penyakit ginjal kronis (CKD). Dari grafik ini terlihat bahwa jumlah pasien dengan CKD (ditandai dengan batang berwarna hijau) cenderung meningkat seiring bertambahnya usia. Peningkatan yang signifikan mulai terlihat pada kelompok usia 43–51 tahun dan mencapai puncaknya pada kelompok usia 59–66 tahun. Setelah itu, meskipun sedikit menurun, jumlah pasien CKD tetap tinggi pada kelompok usia 66–74 tahun. Sementara itu, pasien tanpa CKD (ditandai dengan batang berwarna oranye) lebih banyak ditemukan pada kelompok usia yang lebih muda, terutama pada rentang usia 27–35 tahun. Jumlah pasien non-CKD kemudian menurun secara bertahap pada kelompok usia yang lebih tua. Berdasarkan pola ini, dapat disimpulkan bahwa CKD lebih umum terjadi pada individu dengan usia lanjut, sedangkan individu yang lebih muda cenderung tidak menderita CKD. Distribusi ini mencerminkan pentingnya perhatian dan pencegahan CKD pada kelompok usia menengah ke atas.

#### B. Distribusi CKD berdasarkan Kombinasi Risiko (Hipertensi, Diabetes, CAD)

<img src="Images/Image2.png">

Grafik tersebut menunjukkan distribusi penyakit ginjal kronis (CKD) berdasarkan kombinasi faktor risiko yaitu hipertensi (htn), diabetes (dm), dan penyakit jantung koroner (CAD). Sumbu X menunjukkan berbagai kombinasi risiko dalam format biner (`0` untuk tidak memiliki risiko, `1` untuk memiliki risiko), misalnya `0-0-0` berarti pasien tidak memiliki ketiga risiko, sedangkan `1-1-0` berarti pasien memiliki hipertensi dan diabetes, tetapi tidak memiliki CAD. Sumbu Y menunjukkan jumlah pasien dalam setiap kategori kombinasi risiko, dengan warna hijau untuk pasien CKD dan oranye untuk pasien non-CKD.

Dari grafik ini terlihat bahwa jumlah pasien terbanyak berada pada kombinasi risiko `0-0-0`, yang berarti tidak memiliki hipertensi, diabetes, maupun CAD. Namun, sebagian besar dari mereka adalah pasien non-CKD. Sebaliknya, pada kombinasi risiko tertentu seperti `1-1-0` (hipertensi dan diabetes) dan `1-0-0` (hanya hipertensi), jumlah pasien CKD meningkat secara signifikan. Ini menunjukkan bahwa keberadaan hipertensi dan diabetes, terutama jika digabungkan, sangat berpengaruh terhadap risiko CKD. Sementara kombinasi seperti `0-1-0`, `0-0-1`, dan `0-1-1` menunjukkan jumlah pasien yang lebih sedikit secara keseluruhan, tetapi sebagian besar dari mereka adalah penderita CKD.

Secara keseluruhan, grafik ini memperlihatkan bahwa CKD lebih umum terjadi pada pasien dengan satu atau lebih faktor risiko, khususnya hipertensi dan diabetes. Semakin banyak faktor risiko yang dimiliki, semakin tinggi pula kemungkinan seseorang menderita CKD. Temuan ini mempertegas pentingnya deteksi dan manajemen dini terhadap hipertensi dan diabetes untuk mencegah terjadinya CKD.

#### C. Distribusi Gejala Klinis pada Pasien CKD

<img src="Images/Image3.png">

Gambar tersebut menunjukkan distribusi gejala klinis pada pasien dengan penyakit ginjal kronis (CKD) dalam bentuk tiga diagram lingkaran. Gejala yang ditampilkan meliputi anemia, edema (pembengkakan), dan nafsu makan buruk. Dari diagram pertama, diketahui bahwa sebanyak 75% pasien CKD tidak mengalami anemia, sementara 25% sisanya mengalami gejala tersebut. Pada gejala edema, 72,7% pasien tidak mengalaminya, sedangkan 27,3% mengalami edema. Sementara itu, pada gejala nafsu makan buruk, tercatat 68,8% pasien tidak mengalami gangguan ini, dan 31,2% pasien mengalaminya. Berdasarkan data ini, dapat disimpulkan bahwa sebagian besar pasien CKD tidak menunjukkan gejala-gejala klinis tersebut, namun tetap terdapat proporsi yang signifikan, terutama pada gejala nafsu makan buruk, yang menunjukkan angka tertinggi di antara ketiganya. 

## 2. Preprocessing Data

### Encoding Fitur Kategorikal

Encoding fitur kategorikal dilakukan menggunakan LabelEncoder dari pustaka `sklearn.preprocessing`. Dalam tahap ini, beberapa kolom yang berisi data kategorikal seperti `'sg'`, `'al'`, `'class'`, `'su'`, `'bgr'`, dan lainnya diubah menjadi format numerik. Proses ini dilakukan dengan menerapkan `LabelEncoder().fit_transform` pada setiap kolom yang bersifat kategorikal. Hasilnya, semua nilai kategorikal dalam DataFrame telah dikonversi menjadi angka, sehingga data siap digunakan untuk proses analisis lebih lanjut atau pemodelan machine learning yang membutuhkan input numerik.

### Data Training & Data Testing

Pembagian data menjadi data training dan data testing dilakukane menggunakan fungsi `train_test_split` dari pustaka `sklearn.model_selection`. Pertama, fitur-fitur (variabel independen) disimpan dalam variabel `X`, sedangkan label (variabel target) disimpan dalam variabel `y`, yaitu kolom `'class'`. Kemudian, data dibagi menjadi 80% untuk pelatihan (`X_train`, `y_train`) dan 20% untuk pengujian (`X_test`, `y_test`). Parameter `random_state=42` digunakan untuk memastikan hasil pembagian data konsisten setiap kali kode dijalankan. Langkah ini penting agar model dapat dilatih dan dievaluasi secara adil.

## 3. Processing Data

Proses pelatihan dan evaluasi dilakukan menggunakan beberapa model machine learning, yaitu Logistic Regression, Decision Tree, Random Forest, SVM, KNN, dan MLP Neural Network. Masing-masing model kemudian dilatih menggunakan data training (`X_train`, `y_train`) dan diuji pada data testing (`X_test`). Prediksi hasil model dibandingkan dengan data aktual untuk menghitung metrik evaluasi, yaitu accuracy, precision, recall, dan F1 score. Nilai-nilai ini disimpan dalam sebuah list `evaluation_results` untuk dianalisis lebih lanjut. Proses ini bertujuan untuk membandingkan performa tiap model secara objektif.

## 4. Evaluasi Model

### Metric Evaluasi Model

| Model               | Accuracy | Precision | Recall | F1 Score |
|---------------------|----------|-----------|--------|----------|
| Logistic Regression | 0,975    | 1,000     | 0,9333 | 0,9655   |
| Decision Tree       | 0,925    | 0,8333    | 1,000  | 0,9091   |
| Random Forest       | 1,000    | 1,000     | 1,000  | 1,000    |
| SVM                 | 0,975    | 1,000     | 0,9333 | 0,9655   |
| KNN                 | 0,975    | 0,9375    | 1,000  | 0,9677   |
| MLP Neural Network  | 0,975    | 1,000     | 0,9333 | 0,9655   |

Berdasarkan hasil yang evaluasi, model Random Forest menunjukkan performa terbaik dengan skor sempurna (1.0) di semua metrik evaluasi, yang berarti model ini mampu mengklasifikasikan data uji dengan sangat akurat tanpa kesalahan. Model lain seperti Logistic Regression, SVM, KNN, dan MLP Neural Network memiliki akurasi yang sama sebesar 0,975, namun terdapat sedikit perbedaan pada nilai recall dan F1 score, yang menunjukkan variasi kecil dalam kemampuan masing-masing model dalam mengenali kelas positif. Sementara itu, model Decision Tree memiliki performa yang paling rendah di antara semua model, dengan akurasi 0,925 dan precision 0,8333, yang mengindikasikan adanya kecenderungan menghasilkan prediksi positif yang salah. Secara keseluruhan, Random Forest menjadi pilihan paling optimal untuk tugas klasifikasi pada data ini.

### Confusion Matrix

<img src="Images/Image4.png">

Berdasarkan hasil yang ditampilkan, model berhasil mengklasifikasikan seluruh data dengan sempurna. Sebanyak 25 data dengan label aktual negatif berhasil diprediksi sebagai negatif, dan 15 data dengan label aktual positif berhasil diprediksi sebagai positif. Tidak terdapat kesalahan klasifikasi, baik berupa false positive maupun false negative. Hal ini menunjukkan bahwa model Random Forest memiliki performa yang sangat baik dalam membedakan antara kelas positif dan negatif, dengan akurasi dan presisi yang sempurna dalam pengujian ini.

### Kurva ROC

<img src="Images/Image5.png">

Kurva ROC (Receiver Operating Characteristic) dari model Random Forest yang digunakan untuk menilai kemampuan model dalam membedakan antara kelas positif dan negatif. Kurva ROC menunjukkan hubungan antara True Positive Rate (TPR) dan False Positive Rate (FPR). Berdasarkan grafik, kurva ROC model berada di sudut kiri atas grafik dan membentuk garis hampir tegak lurus dengan sumbu x, yang menandakan performa klasifikasi yang sangat baik. Nilai AUC (Area Under Curve) sebesar 1.00 mengindikasikan bahwa model memiliki kemampuan sempurna dalam membedakan kedua kelas tanpa kesalahan. Semakin mendekati angka 1.0, semakin tinggi kemampuan diskriminatif model, dan dalam kasus ini, model Random Forest menunjukkan performa optimal dalam klasifikasi.

### Feature Importance

<img src="Images/Image6.png">

Feature importance menggambarkan seberapa besar kontribusi masing-masing fitur (variabel) terhadap performa model dalam melakukan prediksi. Dari grafik, terlihat bahwa fitur pcv (packed cell volume) memiliki pengaruh terbesar, yakni sebesar 21,05%, diikuti oleh sg (specific gravity) dan htn (hypertension) yang masing-masing memberikan kontribusi sebesar 13,30% dan 9,92%. Fitur-fitur lain seperti rbcc (red blood cell count), hemo (hemoglobin), dm (diabetes mellitus), dan al (albumin) juga memberikan kontribusi yang signifikan terhadap model.

Sementara itu, fitur-fitur seperti cad (coronary artery disease), ba (bacteria), dan pot (potassium) memberikan kontribusi yang sangat kecil atau bahkan nol, masing-masing kurang dari 0,1%. Informasi ini sangat berguna dalam proses seleksi fitur karena membantu dalam memfokuskan analisis dan pengambilan keputusan pada fitur-fitur yang paling relevan terhadap diagnosis penyakit ginjal kronis.

## 5. Kesimpulan

Berdasarkan hasil evaluasi terhadap beberapa model klasifikasi, Random Forest terbukti menjadi model dengan performa terbaik. Model ini berhasil mencapai skor sempurna (1.0) pada seluruh metrik evaluasi, termasuk akurasi, precision, recall, dan F1 score, serta tidak menghasilkan kesalahan klasifikasi sama sekali. Hal ini didukung oleh hasil confusion matrix yang menunjukkan bahwa seluruh data uji berhasil diklasifikasikan dengan benar, tanpa adanya false positive maupun false negative.

Kinerja optimal dari Random Forest juga tercermin pada kurva ROC, di mana model menunjukkan kemampuan diskriminatif yang sangat tinggi dengan nilai AUC sebesar 1.0, yang berarti model mampu membedakan kelas positif dan negatif secara sempurna.

Dari analisis feature importance, diketahui bahwa fitur packed cell volume (pcv) merupakan kontributor paling signifikan terhadap performa model, diikuti oleh specific gravity (sg) dan hypertension (htn). Sebaliknya, fitur seperti coronary artery disease (cad), bacteria (ba), dan potassium (pot) memberikan kontribusi yang sangat kecil atau tidak signifikan. Informasi ini sangat bermanfaat untuk proses seleksi fitur dalam pengembangan model yang lebih efisien dan interpretatif.

Secara keseluruhan, model Random Forest direkomendasikan sebagai pilihan utama untuk tugas klasifikasi penyakit ginjal kronis pada dataset ini, baik dari segi akurasi, kestabilan prediksi, maupun interpretabilitas fitur yang digunakan.
