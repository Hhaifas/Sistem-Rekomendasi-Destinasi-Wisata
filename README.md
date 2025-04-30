# Laporan Proyek Machine Learning - Haifa Syabina

## Project Overview

Pariwisata merupakan salah satu sektor strategis dalam perekonomian suatu kota. Kota Yogyakarta adalah salah satu tujuan wisata yang menarik para wisatawan karena faktor sejarah dan kebudayaannya. 

Usai COVID 19 melanda, pemerintah berusaha memulihkan perekonomian daerah. Membangun kembali sektor wisata merupakan salah satu usaha pemerintah dalam memulihkan perekonomian daerah yang sempat turun pada saat COVID 19. Namun, dengan banyaknya tujuan wisata yang terdapat di Yogyakarta, hal tersebut menjadi perhatian karena pengunjung akan diberikan banyak informasi tempat wisata. Akan tetapi banyaknya informasi yang masuk terkadang tidak relevan dengan kesukaan pengunjung. Untuk menangani kebutuhan tersebut, sistem rekomendasi menjadisolusi relevan dan efektif untuk masalah ini. 

Dengan menggunakan teknik machine learning dan analisis perilaku pengguna, sistem dapat secara otomatis memberikan saran destinasi wisata berdasarkan preferensi pengguna, riwayat kunjungan, atau bahkan ulasan dari wisatawan lain. Pendekatan ini tidak hanya membantu wisatawan menemukan tempat yang sesuai, tetapi juga dapat meningkatkan penyebaran informasi dan eksposur terhadap destinasi yang kurang populer namun menarik.

Berdasarkan penelitian yang sudah dilakukan tentang sebuah sistem rekomendasi tempat wisata di Kota Semarang dengan
metode collaborative filtering telah terbentuknya sebuah sistem yang dapat mempermudah dan membantu wisatawan berdasarkan pemberian rating dari wisatawan lain. Sistem ini memungkinkan semua orang dapat memberikan rating di dalam sistem
tersebut sehingga memberikan rekomendasi tempat wisata di Kota Semarang. Sistem rekomendasi ini juga dapat mengenalkan
tempat wisata baru di Semarang sehingga diharapkan dapat memunculkan potensi wisata baru di Semarang (Cholil et al., 2023).

Referensi:
- Cholil, S.R dkk. (2023). Sistem Rekomendasi Tempat Wisata di Kota Semarang Menggunakan Metode Collaborative Filtering. JIKO (Jurnal Informatik dan Komputer), 7(1), 118-125. Available at https://media.neliti.com/media/publications/560301-sistem-rekomendasi-tempat-wisata-di-kota-274bc7b9.pdf. 

## Business Understanding

Di tengah maraknya kunjungan wisata dan informasi digital yang melimah, wisatawan mengalami kebingungan menentukan destiansi yang paling sesuai dengan minat mereka. Banyak wisatatan cenderung mengunjungi lokasi yang populer berdasarkan tren atau hasil pencarian pertama. Hal ini dapat menyebabkan ketimpangan wisatawan pada tempat wisata tertentu dan wisata yang tidak sesuai dengan yang diinginkan oleh wisatawan sehingga mengurangi pengalaman wisatawan. Selain itu, dampak tersebut dapat menghambat optimalisasi potensi ekonomi lokal secara meluruh.

### Problem Statements

- Informasi tempat wisata yang kurang relevan dengan preferensi individu
- Kurangnya variasi tujuan wisata
- Tidak merata kunjungan wisatawan yang datang ke wisata tertentu

### Goals

- Meningkatkan pengalaman pengunjung
  Pengunjung memiliki preferensi yang berbeda-beda. Dengan menyediakan sistem rekomendasi destinasi wisata yang sesuai dengan minat dan kebutuhan secara personal akan meningkatkan pengalaman pengunjung sehingga perjalanan wisata menjadi lebih menyenangkan. 
- Menyebarkan arus kunjungan 
  Salah satu tantangan dalam dunia pariwisata adalah konsentrasi kunjungan di lokasi tertentu, sementara destinasi lainnya cenderung sepi. Dengan menyebarkan arus kunjungan wisata maka potensi tempat wisata menjadi merata dan seimbang. 
- Mengoptimalkan promosi destinasi lokal
  Destinasi yang kurang dikenal bisa dimunculkan dalam rekomendasi pengguna dengan preferensi yang cocok. Hal ini lebih efektif dibandingkan promosi umum karena menyasar audiens yang sudah potensial tertarik, sehingga dapat meningkatkan tingkat kunjungan secara organik.
  
Teknologi yang akan digunakan berupa:
- Content-Based Filtering
  Metode ini akan menyarankan destinasi berdasarkan karakteristik yang mirip dengan tempat yang disukai pengunjung
- Collaborative Filtering
  Metode ini digunakan untuk menemukan destinasi baru berdasarkan preferensi pengunjung lain yang serupa sehingga rekomendasi yang akan dihasilkan lebih beragam.

## Data Understanding
Data yang digunakan adalah dataset [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data) yang didapatkan dari Kaggle. Dataset ini berisi 4 file, yaitu 
1. tourism_with_id.csv : berisi informasi tempat wisata di 5 kota besar di Indonesia yang berjumlah kurang lebih 400
   Variabel tourism_with_id.csv:
    - Place_Id : berisi unik dari Place_Name
    - Place_Name : berisi nama tempat 
    - Desription : berisi deskripsi dari nama tempat
    - Category : berisi kategori dari nama tempat
    - City : berisi kota setiap tempat wisata
    - Price : berisi harga tiket masuk
    - Rating : berisi rating setiap tempat wisata
    - Time_Minutes : 
    - Coordinate
    - Lat
2. user.csv : berisi dummy user untuk membuat fitur rekomendasi berdasarkan user
   Variabel user.csv:
   - User_Id : user id untuk tiap pengunjung
   - Location : asal kota tiap pengunjung
   - Age : umur tiap pengunjung
3. tourism_rating.csv : berisi rating-rating yang dibuat untuk sistem rekomendasi berbasis rating
   Variabel tourism_rating.csv
   - User_Id : berisi user id untuk tiap pengunjung
   - Place_Id : berisi id tempat untuk tempat yang dikunjungi oleh pengunjung
   - Place_Ratings : berisi penilaian atau rating yang diberikan oleh pengunjung berdasarkan tempat kunjungan mereka.
4. package_tourism.csv : berisi rekomendasi untuk tempat terdekat berdasarkan waktu, biaya, dan rating.
   Variabel package_tourism.csv:
   - Package : package id untuk tiap package
   - City : kota untuk tiap package
   - Place_Tourism1 : wisata 1
   - Place_Tourism2 : wisata 2
   - Place_Tourism3 : wisata 3
   - Place_Tourism4 : wisata 4
   - Place_Tourism5 : wisata 5

Namun penulis hanya mengambil 3 dataset teratas yaitu tourism_with_id.csv, user.csv, dan tourism_rating.csv. Selain itu hanya mengambil destinasi pada kota Yogyakarta karena proyek ini terbatas hanya pada satu kota tujuan saja. 

![image](asets/rating_destinasi.png)
Pada grafik tersebut menunjukan distribusi rating pada tiap destinasi. Menunjukkan rating berkisar antara 4-5 dengan 4.5 adalah rating paling banyak diberikan. 

![image](asets/jumlah_kategori_wisata.png)
Pada grafik tersebut wisata terbanyak di Yogyakarta adalah taman hiburan dengan persentase sebesar 28.6%. dilanjut kategori budaya sebesar 27%, kategori cagar budaya 23.8%, kategori Bahari 18.3%, dan pusat perbelanjaan sebesar 2.4%. 

![image](asets/harga_tiket.png)
Pada grafik tersebut menunjukkan harga tiket termahal di tempat wisata di Yogyakarta. Hasilnya Goa Jomblang adalah wisata dengan harga tiket termahal dengan harga Rp 500.000. 

![image](asets/destinasi_rating_terbanyak.png)
Pada grafik tersebut menunjukkan bahwa Sumur Gumuling adalah wisata yang banyak diulas oleh pengunjung

![image](asets/asal_pengunjung.png)
Pada grafik tersebut menunjukkan banyaknya pengunjung tiap kota asal. Pengunjung banyak berasal dari Bekasi. Madura dan Nganjuk adalah kota yang paling sedikit pengunjung ke Yogyakarta. 


## Data Preparation
Sebelum melakukan modeling, penulis melakukan preparation pada data yang akan digunakan. 
- Mengatasi Missing Value
  Pada data destination terdapat missing pada dua fitur. Fitur tersebut akan dihapus dengan menggunakan `.drop()` karena fitur tersebut tidak dibutuhkan dalam pemodelan nanti

### Data Preparation CBF
- Mengambil destinasi hanya pada daerah Yogyakarta
  `destination[destination['City'] == 'Yogyakarta']`
- Mengambil data rating pada daerah Yogyakarta
  Menggunanakn fungsi `.merge()` pada data rating dan destination untuk mengambil destinasi pada daerah Yogyakarta
- Mengambil data user pada userId yang memberi ulasan hanya pada daerah Yogyakarta
  Dengan fungsi `.merge()` kali ini data rating akan digabung dengan data user pada daerah UserId yang memberi rating pada daerah Yogyakarta

## Data Preparation Collaborative Filtering
- Melakukan encoding pada User_Id dan Place_Id agar Id memiliki nilai yang sama dimulai dari 0
- Membagi data menjadi data uji dan data latih


## Modeling

### Content Based Filtering
- Melakukan TF-IDF
  TF-IDF akan mengubah bentuk data menjadi matriks yang akan digunakan untuk perhitungan cosine similarity menggunanakan fungsi `TfidfVectorizer()`.
- Menghitung Cosine Similarity
  Cosine Similarity adalah pengukuran yang digunakan untuk mengukur dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. Metrik ini sering digunakan untuk mengukur kesamaan dokumen dalam analisis teks. Sebagai contoh, dalam studi kasus ini, cosine similarity digunakan untuk mengukur kesamaan nama tempat dan nama kaetgori.
- Mendapatkan Rekomendasi
  Selanjutnya membuat fungsi rekomendasi dengan parameter
  - place_name : nama tempat
  - similarity_data: dataframe mengenai similarity yang sudah didefinisikan sebelumnya
  - items: nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'Place_Name' dan 'Category'
  - k: banyaknya rekomendasi yang ingin diberikan

`destination_recommendation('Pantai Greweng')`
Place_Name - Category
Pantai Congot	- Bahari
Pantai Sundak	- Bahari
Pantai Depok Jogja	- Bahari
Hutan Mangrove Kulon Progo - Bahari
Pantai Sadranan	- Bahari

Rekomendasi menghasilkan kategori yang sama pada destinasi Pantai Greweng.


### Collaborative Filtering
- Membuat kelas RecommenderNet dengan keras Model class.
- Melakukan compile pada model dengan menggunakan Binary Crossentropy untuk menghitung loss function Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.
- Training: model dilakukan training sebanyak 100 epochs, 8 batch_size.
Berikut merupakan hasil rekoemendasi dari user 129:

**Showing recommendations for users: 129**

**Wisata Kraton Jogja : Budaya**

Top 10 destination recommendation
Situs Warungboto-Taman Hiburan
Sumur Gumuling-Taman Hiburan
Desa Wisata Sngai Code Jogja Kota-Taman Hiburan
Monumen Yogya Kembali-Budaya
Bukit Bintang Yogyakrta-Taman Hiburan
Monumen Sanapati-Budaya
The World Landmarks - Merapi Park Yogyakarta-Taman Hiburan
Watu Goyang-Budaya
Kampung Wisata Rejowinangun-Budaya
Alun-alun Utara Keraton Yogyakarta-Budaya

Hasil tersebut menunjukkan rekomendasi untuk user 235. Hasil rekomendasi destinasi adalah 6 kategori Taman hiburan dan 4 kategori budaya. 

Kelebihan
- CF : dapat memberikan rekomendasi yang lebih bervariasi
- CBF: memberi rekomendasi yang lebih personal dan relevan bagi pengguna

Kekurangan
- CF: membutuhkan user yang banyak
- CBF: tidak bisa memberikan rekomendasi yang bervariasi


## Evaluation
Evaluasi yang dilakukan untuk model collaborative filtering adalah dengan menggunakan metrik RMSE. RMSE adalah akar kuadrat dari MSE. Secara matematis, RMSE mengukur deviasi standar kesalahan. Mirip dengan MSE, RMSE banyak digunakan dalam regresi dan estimasi model yang memerlukan prediksi numerik.

Hasilnya, untuk data uji nilai RMSE naik dengan nilai akhir 0.36 sementara untuk data latih nilai RMSE cenderung turun di angka 0.3.

