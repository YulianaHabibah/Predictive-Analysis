# Proyek House Rental Price Prediction

#### Disusun oleh : 
Nama : Yuliana Habibah

ID   : MC015D5X1091

## Domain Proyek

### Latar Belakang

Hunian seperti rumah atau apartemen merupakan kebutuhan esensial manusia sebagai tempat berlindung dan menetap. Nilai dari suatu properti sangat dipengaruhi oleh karakteristiknya, seperti lokasi, luas bangunan, jumlah kamar tidur dan kamar mandi, keberadaan perabotan, serta fitur-fitur lainnya yang menunjang kenyamanan dan fungsi.

Harga sewa suatu hunian umumnya ditentukan berdasarkan nilai-nilai tersebut. Namun, penentuan harga secara manual seringkali tidak akurat karena dipengaruhi oleh berbagai faktor yang kompleks dan fluktuatif. Untuk mengurangi ketidakpastian ini, perusahaan penyewaan perlu membangun sistem prediksi yang mampu memperkirakan harga sewa ideal berdasarkan karakteristik properti.

### Mengapa masalah ini harus diselesaikan?

+ Penetapan harga sewa yang tidak tepat dapat menimbulkan kerugian, baik bagi pemilik properti yang kehilangan potensi pendapatan maupun bagi penyewa yang membayar lebih dari nilai sebenarnya.

+ Sistem prediksi harga sewa yang akurat dapat mengurangi subjektivitas dan kesalahan manusia dalam menentukan harga.

+ Model prediktif berbasis machine learning mampu mengolah berbagai variabel penting secara efisien dan menghasilkan estimasi harga yang lebih adil dan kompetitif.

+ Dengan adanya sistem ini, perusahaan penyewaan properti dapat mengambil keputusan strategis berdasarkan data, bukan asumsi.

+ Efisiensi pasar akan meningkat karena harga yang ditawarkan cenderung mencerminkan nilai aktual properti sesuai permintaan dan kondisi pasar.


Referensi : 

[Analisis Prediksi Harga Rumah Sesuai Spesifikasi Menggunakan Multiple Linear Regression](https://ejournal.upnvj.ac.id/index.php/informatik/article/download/3635/1498)

[Predicting property prices with machine learning algorithms](https://www.tandfonline.com/doi/full/10.1080/09599916.2020.1832558)


## Business Understanding

### Problem Statement

+ Faktor-faktor apa saja yang memiliki pengaruh terbesar terhadap besaran harga sewa rumah atau apartemen?
+ Langkah-langkah apa yang perlu dilakukan untuk mempersiapkan data agar dapat dipelajari secara optimal oleh model machine learning?
+ Bagaimana estimasi harga sewa rumah di pasaran jika dilihat dari karakteristik properti tertentu?

### Goals

+ Mengidentifikasi faktor utama yang memengaruhi harga sewa rumah atau apartemen.
+ Menyusun dan membersihkan data agar siap digunakan dalam proses pelatihan model.
+ Mengembangkan model machine learning untuk memprediksi harga sewa secara akurat berdasarkan atribut properti tertentu.

### Solution Statement

1. Melakukan analisis data secara univariat dan multivariat, dilengkapi dengan visualisasi untuk memahami karakteristik data, hubungan antar fitur, serta mendeteksi outlier sebelum data diproses lebih lanjut untuk pelatihan model.
2. Mempersiapkan data dan membangun model regresi prediktif menggunakan algoritma K-Nearest Neighbors, Random Forest, dan AdaBoost, termasuk melakukan hyperparameter tuning melalui metode grid search untuk mengoptimalkan performa model.


## Data Understanding & Removing Outlier

Dataset yang digunakan dalam proyek ini berisi informasi mengenai harga sewa properti di India, mencakup berbagai karakteristik hunian. Dataset tersedia dalam format CSV dan dapat diakses melalui [Kaggle : House Rent Prediction Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset).

Berikut informasi pada dataset :

+ Berjumlah 4.746 entri dengan 12 fitur.
+ Terdiri dari 4 fitur numerik (tipe int64) dan 8 fitur kategorik (tipe object).
+ Seluruh data lengkap tanpa nilai yang hilang (missing value).

### Variable - variable pada dataset

+ Posted On = Tanggal ketika informasi properti dipublikasikan.
+ BHK= Jumlah total ruangan inti dalam hunian, termasuk kamar tidur, ruang tengah, dan dapur.
+ Rent= Besarnya biaya sewa untuk rumah atau apartemen.
+ Size= uas bangunan dalam satuan kaki persegi (sqft).
+ Floor= nformasi mengenai lantai tempat properti berada dan total jumlah lantai bangunan.
+ Area Type=  Kategori ukuran area properti, seperti Super Area, Carpet Area, atau Build Area.
+ Area Locality=  Nama atau lokasi spesifik properti berada.
+ City= Kota tempat properti tersebut berada.
+ Furnishing Status= SStatus kelengkapan perabot, mencakup Furnished, Semi-Furnished, atau Unfurnished.
+ Tenant Preferred=  Jenis penyewa yang diutamakan oleh pemilik atau agen properti.
+ Bathroom= Jumlah kamar mandi yang tersedia.
+ Point of Contact= nformasi kontak yang dapat dihubungi terkait properti.

Fitur Posted On dan Point of Contact dianggap tidak memiliki pengaruh terhadap harga sewa, sehingga kedua atribut ini dihapus dari pemrosesan data guna meningkatkan efektivitas model prediktif.

### Univariate Analysis

Univariate Analysis merupakan proses analisis data dengan memeriksa masing-masing fitur secara individual untuk memahami distribusi, karakteristik, serta potensi anomali dalam data tersebut tanpa mempertimbangkan hubungan antar fitur lainnya.
#### Analisis jumlah nilai unique pada setiap fitur kategorik

Fitur kategorikal seperti *City*, *Furnishing Status*, dan *Tenant Preferred* menunjukkan distribusi sampel yang relatif seimbang di antara masing-masing kategori, sehingga tidak menimbulkan dominasi kelas tertentu dalam data.
![Cuplikan layar 2025-06-09 071445](https://github.com/user-attachments/assets/f89300e9-6172-4daf-9af6-6394495e5955)

![Cuplikan layar 2025-06-09 071846](https://github.com/user-attachments/assets/12123993-1dcf-4b56-bce3-6aeb29621b2f)

![Cuplikan layar 2025-06-09 072016](https://github.com/user-attachments/assets/a261e433-9566-4418-aa4d-6bf80fac09f7)


#### Analisis sebaran pada setiap fitur numerik


![Cuplikan layar 2025-06-09 072644](https://github.com/user-attachments/assets/86819057-49d1-4054-9864-a33ef8593a3c)


Berdasarkan grafik di atas, dapat disimpulkan bahwa sebagian besar rumah memiliki 1 hingga 3 BHK serta 1 hingga 3 kamar mandi. Selain itu, mayoritas rumah memiliki luas bangunan di bawah 2000 sqft. Rentang harga sewa yang tercatat dalam data sangat lebar, mulai dari 1200 hingga 3.500.000. Namun, rata-rata harga sewa hanya sebesar 35.003, yang menunjukkan adanya distribusi harga yang tidak merata. Kondisi distribusi seperti ini dapat memengaruhi kinerja model dalam melakukan prediksi secara akurat.


### Multivariate Analysis

Multivariate Analysis menunjukkan hubungan antara dua atau lebih fitur dalam data.

#### Analisis fitur numerik

+ Fitur *Size* dan *BHK* dianalisis lebih lanjut karena ditemukan ketidakwajaran, seperti rumah dengan 1 BHK yang hanya memiliki luas 100 sqft, yang dinilai tidak realistis. Oleh karena itu, ditetapkan batas minimum kelayakan, yaitu 300 sqft per BHK. Seluruh data yang berada di bawah ambang batas ini dianggap sebagai outlier dan dihapus dari dataset. Proses pembersihan ini menyebabkan pengurangan jumlah sampel sebanyak 548 data.

+ Fitur *Size* dan *Rent* dianalisis lebih lanjut dengan membuat fitur turunan baru bernama *Price\_per\_sqft*, yang merepresentasikan harga sewa per satuan luas (sqft). Pembuatan fitur ini bertujuan untuk mempermudah deteksi outlier harga sewa berdasarkan luas bangunan, sehingga anomali harga per sqft yang tidak wajar dapat diidentifikasi dan ditangani dengan lebih efektif.

 ![Cuplikan layar 2025-06-09 073523](https://github.com/user-attachments/assets/ea49266e-1ce3-46df-8ec1-631f97040aad)
 

Dari hasil tersebut, ditemukan bahwa terdapat nilai ekstrem seperti harga sewa 571 per sqft yang terlalu rendah dan 1.400.000 per sqft yang sangat tinggi. Untuk menangani outlier tersebut, dilakukan penghapusan data berdasarkan rata-rata (*mean*) dan satu standar deviasi, yang dihitung secara spesifik untuk masing-masing kota. Pendekatan ini memungkinkan penyesuaian yang lebih kontekstual terhadap kondisi pasar lokal. Proses ini mengakibatkan pengurangan jumlah sampel sebanyak 497.


+ Fitur *Bathroom* dan *BHK* dianalisis karena terdapat kasus yang tidak lazim, seperti rumah dengan 2 BHK memiliki 4 kamar mandi. Untuk menjaga konsistensi logis, ditetapkan batas bahwa jumlah kamar mandi tidak boleh melebihi jumlah BHK ditambah 2. Penerapan aturan ini menghasilkan penghapusan 3 sampel dari dataset.
  
+ Kolerasi antara semua fitur numerik
![Cuplikan layar 2025-06-09 073919](https://github.com/user-attachments/assets/7f5e26d4-0a75-431f-83eb-d0dc22a13a8f)

 Visualisasi korelasi antar fitur numerik menunjukkan bahwa fitur BHK, Size, dan Bathroom memiliki korelasi yang rendah terhadap variabel target Rent. Hal ini kemungkinan disebabkan oleh keterbatasan jumlah data dalam penelitian ini. Namun, ditemukan korelasi yang cukup kuat antara BHK dan Bathroom dengan Size, yang sejalan dengan hasil pembersihan data dan penghapusan outlier yang telah dilakukan sebelumnya.

#### Analisis fitur kategorik

Analisis ini dilakukan untuk melihat kolerasi antara fitur kategorik dengan fitur target (Rent).

+ Fitur Area Type
![Cuplikan layar 2025-06-09 074218](https://github.com/user-attachments/assets/b53fa7a9-c114-44ea-83da-07f9734045c2)

  Fitur *Area Type* menunjukkan pengaruh yang minimal terhadap rata-rata harga sewa, sehingga kontribusinya terhadap prediksi harga sewa relatif kecil.


+ Fitur City
 ![Cuplikan layar 2025-06-09 074414](https://github.com/user-attachments/assets/41e47765-dfe9-4cb3-9a36-7f76eb350ede)

 Fitur *City* memberikan pengaruh yang signifikan terhadap rata-rata harga sewa, terutama untuk properti yang terletak di Mumbai. Hal ini terlihat dari sebaran harga sewa tertinggi yang didominasi oleh rumah-rumah di Mumbai, yang merupakan kota dengan biaya hidup tertinggi di India, diikuti oleh Delhi.

+ Fitur Furnishing Status
 ![Cuplikan layar 2025-06-09 074801](https://github.com/user-attachments/assets/67dd5113-7310-4bda-b289-ccc9e4d21379)
  Fitur Furnishing Status berpengaruh signifikan terhadap rata-rata harga sewa, karena rumah dengan perabot lengkap biasanya dihargai lebih tinggi dibanding yang tanpa perabot.


+ Fitur Tenant Preferred
![Cuplikan layar 2025-06-09 075044](https://github.com/user-attachments/assets/afe354b1-9ab2-4520-941c-95f338e29ca3)

  Fitur Tenant Preferred cukup berpengaruh terhadap rata-rata harga sewa, terlihat dari grafik bahwa rumah yang direkomendasikan untuk keluarga memiliki harga sewa rata-rata lebih tinggi dibandingkan yang lain.

## Data preparation

1. **One Hot Encoding**

One hot encoding adalah teknik mengubah data kategorik menjadi format numerik dengan membuat kolom baru untuk setiap kategori, yang berisi nilai 0 atau 1. Pada proyek ini, fitur yang diubah menjadi numerik adalah Area Type, City, Furnishing Status, dan Tenant Preferred.

2. **Train Test Split**

Train test split adalah proses pembagian data menjadi data latih dan data uji. Data latih digunakan untuk membangun model, sementara data uji dipakai untuk mengevaluasi performa model. Dataset proyek ini berjumlah 3696, dibagi menjadi 3511 data latih dan 185 data uji.

3. **Normalisasi**

Agar algoritma machine learning bekerja lebih efektif dan efisien, data perlu distandarisasi ke skala yang seragam. Proyek ini menggunakan teknik normalisasi Standarisasi melalui `sklearn.preprocessing.StandardScaler`.

## Modeling

### Algoritma

* **K-Nearest Neighbour (KNN)**
  KNN memprediksi nilai dengan membandingkan jarak sampel ke k tetangga terdekat dari data latih. Model dibangun menggunakan `sklearn.neighbors.KNeighborsRegressor` dengan data `X_train` dan `y_train`. Parameter utama:

  * `n_neighbors`: jumlah tetangga terdekat yang digunakan.

* **Random Forest**
  Random Forest adalah metode ensemble yang membangun banyak decision tree selama pelatihan. Pada proyek ini digunakan `sklearn.ensemble.RandomForestRegressor` dengan `X_train` dan `y_train`. Parameter utama:

  * `n_estimators`: jumlah pohon keputusan maksimal.
  * `max_depth`: kedalaman maksimal setiap pohon.
  * `random_state`: pengontrol seed acak untuk reproduksibilitas.

* **AdaBoost**
  AdaBoost (Adaptive Boosting) adalah metode ensemble yang menggabungkan beberapa model sederhana (weak learners), biasanya decision stumps (pohon dengan satu split), untuk membentuk model kuat. Proyek ini menggunakan `sklearn.ensemble.AdaBoostRegressor` dengan `X_train` dan `y_train`. Parameter utama:

  * `n_estimators`: jumlah estimator maksimal untuk boosting.
  * `learning_rate`: memperkuat kontribusi setiap regressor.
  * `random_state`: pengontrol seed acak untuk konsistensi hasil.



+ **Hyperparameter Tuning (Grid Search)**
  Hyperparameter tuning adalah proses mencari kombinasi parameter terbaik untuk membangun model yang optimal. Pada proyek ini, teknik yang digunakan adalah grid search. Berikut hasil Grid Search yang diperoleh.

![Cuplikan layar 2025-06-09 082944](https://github.com/user-attachments/assets/ec666f50-2469-42ef-90da-934d7e9e0c81)

## Evaluation

Metrik evaluasi yang digunakan dalam proyek ini adalah akurasi dan mean squared error (MSE). Akurasi mengukur sejauh mana prediksi sesuai dengan nilai asli (y\_test), sedangkan MSE menghitung rata-rata kuadrat selisih antara nilai aktual dan prediksi untuk menilai besarnya error model. Berikut adalah rumus MSE:

![Cuplikan layar 2025-06-09 080254](https://github.com/user-attachments/assets/2606a74f-1a1a-4569-b815-f38932ef38a5)


Berikut hasil evaluasi pada proyek ini :

+ Akurasi
  | model    | accuracy |
  |----------|----------|
  | knn      | 0.726986 |
  | boosting | 0.898556 |
  | rf       |0.932057 |

+ Mean Squared Error (MSE)
 
![Cuplikan layar 2025-06-09 080617](https://github.com/user-attachments/assets/ddb2acac-8285-419e-9b11-cf6ea67f56e9)

Dari hasil evaluasi, terlihat bahwa model Random Forest menunjukkan performa terbaik dibandingkan algoritma lain yang digunakan dalam proyek ini. Model ini memiliki akurasi yang lebih tinggi, artinya prediksi yang dihasilkan lebih mendekati nilai sebenarnya (y\_test). Selain itu, tingkat error-nya—diukur menggunakan mean squared error (MSE)—juga lebih rendah, menandakan kesalahan prediksi lebih kecil dan model lebih andal. Dengan kata lain, Random Forest mampu menangkap pola data dengan lebih baik sehingga menghasilkan prediksi yang lebih akurat dan konsisten dibandingkan K-Nearest Neighbour dan AdaBoost pada dataset ini.

