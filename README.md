# Laporan Proyek Machine Learning - Gunawan

## Project Overview

Di era digital, jumlah buku yang tersedia di pasar, baik dalam format cetak maupun elektronik, terus meningkat. Menurut Statista (2023), pasar global e-book diproyeksikan mencapai pendapatan sebesar $15,8 miliar pada tahun 2025, dengan tingkat pertumbuhan tahunan sebesar 3,3% sejak 2020. Namun, banyaknya pilihan ini justru menghadirkan tantangan bagi pembaca untuk menemukan buku yang sesuai dengan preferensi mereka. Penelitian oleh Kardan dan Conati (2013) menunjukkan bahwa pemahaman pola perilaku pembaca digital sangat penting untuk mengembangkan rekomendasi yang relevan dan mendukung pembelajaran berbasis buku [Applying a Framework for Student Modeling in Exploratory Learning Environments: Comparing Data Representation Granularity to Handle Environment Complexity](https://link.springer.com/article/10.1007/s40593-016-0131-y).

Sementara itu, penelitian dari American Library Association (ALA) menunjukkan bahwa 70% pembaca mengandalkan rekomendasi dari teman, ulasan daring, atau algoritme untuk memilih buku. Kondisi ini menunjukkan adanya kebutuhan nyata akan teknologi yang dapat membantu pembaca memilih buku yang relevan dengan minat mereka.

Sistem rekomendasi berbasis machine learning dapat menjadi solusi untuk permasalahan ini. Dengan memanfaatkan algoritme seperti content-based filtering dan collaborative filtering, sistem rekomendasi mampu menganalisis data preferensi pengguna dan menyediakan saran buku yang lebih personal. Amazon menggunakan pendekatan kombinasi collaborative filtering, content-based filtering, dan deep learning untuk meningkatkan pengalaman pengguna dan penjualan . Sebuah studi menunjukkan bahwa sistem ini meningkatkan penjualan hingga 35% dari total pendapatan mereka [Amazon.com Recommendations: Item-to-Item Collaborative Filtering](https://ieeexplore.ieee.org/document/1167344).

Proyek ini memiliki beberapa tujuan strategis yang membuatnya penting untuk diselesaikan, antara lain:
- Meningkatkan Pengalaman Pengguna: Dengan menghadirkan rekomendasi personal, pengguna dapat menemukan buku yang sesuai dengan minat mereka tanpa perlu mencari secara manual dalam katalog yang besar.
- Mendukung Industri Penerbitan Buku: Sistem ini juga dapat membantu penerbit dan penjual buku untuk memasarkan produk mereka dengan lebih tepat sasaran kepada pembaca yang berpotensi tertarik.
- Efisiensi dan Personalisasi: Teknologi ini mengurangi waktu yang dibutuhkan pembaca untuk menemukan buku, sehingga meningkatkan efisiensi dan tingkat kepuasan.
- Pengembangan Teknologi AI: Implementasi sistem rekomendasi ini memberikan kontribusi nyata terhadap pengembangan teknologi berbasis AI, khususnya dalam ranah content-based filtering dan collaborative filtering.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan di atas, maka rumusan masalah yang akan diselesaikan pada proyek ini yaitu:
- Dibutuhkan model machine learning yang bisa memberikan rekomendasi buku kepada pengguna.
- Dari banyaknya buku yang tersedia, manakah yang akan direkomendasikan kepada pengguna?

### Goals

Berdasarkan rumusan masalah yang telah dipaparkan di atas, maka tujuan dari proyek ini yaitu:
- Membuat model machine learning rekomendasi buku.
- Dapat memberikan rekomendasi buku kepada pengguna tertentu.

### Solution Approach

Pendekatan solusi untuk mencapai goals sebelumnya dapat dijabarkan dalam langkah-langkah sebagai berikut.
- Menganalisis dataset yang ada dan menangani permasalahan pada dataset
- Mengembangkan model dengan menggunakan 2 pendekatan, yaitu content-based filtering recommendation dan collaborative filtering recommendation.
  - Content-based Filtering Recommendation (Sistem Rekomendasi Berbasis Penyaringan Konten)
    - Merupakan sistem rekomendasi yang memberikan rekomendasi item yang hampir sama dengan item yang disukai oleh pengguna di masa lalu. Content-based filtering akan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai oleh pengguna lain sebelumnya. Pendekatan content-based filtering menggunakan algoritme TF-IDF Vectorizer dan Cosine Similarity.
    - Algoritme ini bekerja dengan mencari kedekatan suatu buku yang akan direkomendasikan dengan buku yang telah diambil oleh pembaca berdasarkan kemiripan antar isinya.
    - Kelebihan:
      - Hasil rekomendasi didasarkan pada preferensi buku.
      - Sederhana dan transparan karena mudah dipahami bagaimana algoritme ini bekerja.
    - Kelemahan:
      - Pembaca buku tidak mendapatkan rekomendasi dari jenis buku yang berbeda.
  - Collaborative Filtering Recommendation (Sistem Rekomendasi Berbasis Penyaringan Kolaboratif)
    - Merupakan sistem rekomendasi yang memberikan rekomendasi item yang hampir sama dengan preferensi pengguna di masa lalu berdasarkan riwayat pengguna lain yang memiliki preferensi yang sama, misalnya berdasarkan penilaian atau rating yang telah diberikan pengguna di masa lalu.
    - Algoritme ini bekerja dengan mengumpulkan dan mengolah sejumlah besar informasi yang didasarkan pada aktifitas pembaca buku, seperti pemberian nilai, penulis buku, atau preferensi lainnya. Informasi yang telah dikumpulkan dan diolah tersebut akan digunakan sebagai preferensi dengan pembaca buku lain dengan mencari kesamaannya.
    - Kelebihan:
      - Informasi tentang preferensi dapat ditambahkan secara mudah.
      - Adanya rekam jejak preferensi memudahkan sistem rekomendasi bekerja lebih baik.
    - Kelemahan:
      - Kurang efektif terhadap pengguna yang belum memiliki data karena tidak terdapat informasi yang cukup.

## Data Understanding

Dataset yang digunakan pada proyek ini terdiri dari 3 file CSV, yaitu `Books.csv`, `Ratings.csv`, dan `Users.csv` ([Kaggle - Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)) dengan informasi detail dari masing-masing file sebagai berikut.

`Books.csv` berisi informasi mengenai buku. Terdapat 271.360 baris dan 8 kolom dengan keterangan variabel sebagai berikut.
| Variabel | Tipe Data | Deskripsi |
|----------|-----------|-----------|
| ISBN | Object | 13 digit angka sebagai identifikasi buku |
| Book-Title | Object | Judul buku |
| Book-Author | Object | Penulis buku |
| Year-Of-Publication | Object | Tahun terbit buku |
| Publisher | Object | Penerbit buku |
| Image-URL-S | Object | Tautan sampul buku ukuran kecil |
| Image-URL-M | Object | Tautan sampul buku ukuran menengah |
| Image-URL-L | Object | Tautan sampul buku ukuran besar |

`Ratings.csv` berisi informasi mengenai peringkat buku. Terdapat 1.149.780 baris dan 3 kolom dengan keterangan variabel sebagai berikut.
| Variabel | Tipe Data | Deskripsi |
|----------|-----------|-----------|
| User-ID | Integer | Identifikasi unik pengguna |
| ISBN | Object | 13 digit angka sebagai identifikasi buku |
| Book-Rating | Integer | Penilaian terhadap buku yang diberikan pengguna |

`Users.csv` berisi informasi mengenai pengguna. Terdapat 278.858 baris dan 3 kolom dengan keterangan variabel sebagai berikut.
| Variabel | Tipe Data | Deskripsi |
|----------|-----------|-----------|
| User-ID | Integer | Identifikasi unik pengguna |
| Location | Object | Lokasi tempat tinggal pengguna |
| Age | Float | Umur pengguna |

### Exploratory Data Analysis (EDA)

EDA adalah langkah kritis dalam analisis data yang memungkinkan untuk memahami informasi yang terkandung dalam dataset sebelum memulai proses analisis yang lebih mendalam. EDA membantu mengungkap pola, anomali, dan tren yang mungkin tersembunyi dalam data, sehingga memungkinkan pengambilan keputusan yang lebih baik. Dengan menjalankan EDA, variabel penting dapat diidentifikasi, merumuskan pertanyaan penelitian yang lebih tepat, dan membuat asumsi awal yang relevan untuk perancangan model yang lebih kompleks.

#### Dataset Books

![Gambar01](https://github.com/user-attachments/assets/998d1a54-32fd-4a88-9fa4-ec85046b383f)

DataFrame Books berisi 271.360 baris dengan 8 kolom data buku. Terdapat kesalahan tipe data pada kolom Year-Of-Publication yang seharusnya Integer, namun Object. Ada kemungkinan terdapat kesalahan nilai di dalamnya yang akan diperiksa di proses selanjutnya. Pada kolom Book-Author, Publisher, dan Image-URL-L terdapat nilai hilang, masing-masing sebanyak 2, 2, dan 3, sehingga perlu dilakukan pemrosesan lebih lanjut pada tahap persiapan data.

![Gambar02](https://github.com/user-attachments/assets/d96528d4-2fbe-4376-ae83-2acb832eb87a)

Kolom Year-Of-Publication memiliki kesalahan nilai. Kesalahan tulis pada nilai ini akan diperbaiki pada tahap persiapan data.

#### Dataset Ratings

![Gambar03](https://github.com/user-attachments/assets/daade7c7-736c-4152-b944-8e1e8ae9716c)

DataFrame Ratings berisi 1.149.780 baris dengan 3 kolom data rating. Tidak terdapat nilai hilang pada setiap kolomnya.

![Gambar04](https://github.com/user-attachments/assets/eeca8ca0-77bf-4ec9-83e4-f99229cfa2bd)

Berdasarkan visualisasi di atas, dapat disimpulkan bahwa rating terbanyak dari buku yang sudah pernah dibaca bernilai 0, dengan jumlah sekitar 700.000-an. Rating 0 tersebut dapat menyebabkan bias dan memengaruhi hasil analisis, sehingga data dengan rating 0 tersebut dapat dihapus pada tahap persiapan data.

#### Dataset Users

![Gambar05](https://github.com/user-attachments/assets/4f861680-dc61-464b-bb0e-4c0fed1924e6)

DataFrame Users berisi 278.858 baris dengan 3 kolom data user. Pada kolom Age terdapat nilai hilang sebanyak 110.762, sehingga perlu dilakukan pemrosesan lebih lanjut pada tahap persiapan data.

![Gambar06](https://github.com/user-attachments/assets/6fc6a76e-c985-4ce1-8eb2-a8044140994a)

Pada kolom Age terdapat nilai NaN dan nilai abnormal sehingga perlu dilakukan pemrosesan lebih lanjut pada tahap persiapan data.

![Gambar07](https://github.com/user-attachments/assets/64152860-d589-407a-b094-30634fc59ea1)

Berdasarkan visualisasi di atas, distribusi nilai Age memiliki skewness positif dan terdapat nilai abnormal yang akan diproses pada tahap persiapan data.

## Data Preparation

### Dataset Books

#### Memperbaiki Kesalahan Nilai

![Gambar08](https://github.com/user-attachments/assets/04a8ec5c-55da-4180-b6c0-ce9775413771)

Kolom Year-Of-Publication memiliki kesalahan nilai. Kesalahan tulis pada nilai ini akan diperbaiki secara manual.

![Gambar09](https://github.com/user-attachments/assets/a7415939-c92f-4f17-83cf-590d195f8dd7)

#### Mengganti Tipe Data Kolom

Setelah kesalahan nilai pada kolom Year-Of-Publication diperbaiki, maka kolom Year-Of-Publication sudah dapat diubah tipe datanya menjadi Integer.

![Gambar10](https://github.com/user-attachments/assets/5c06c036-6014-43f8-8a42-f6b74e9bd878)

#### Memperbaiki Kesalahan Nilai

![Gambar11](https://github.com/user-attachments/assets/0cde91d4-6651-4e04-ba8e-2a69b43b9260)

Nilai pada kolom Year-Of-Publication juga terdapat nilai abnormal 0 dan nilai di atas 2014 (dataset diambil di tahun 2014). Nilai abnormal tersebut diperbaiki dengan melakukan imputasi nilai yang sering muncul atau nilai modus karena imputasi dengan nilai mean tidak cocok untuk kolom ini yang memiliki skewness negatif yang apabila diberikan imputasi mean akan mengubah pola distribusinya.

![Gambar12](https://github.com/user-attachments/assets/1f46f0cc-3a0d-4ed9-8ec4-ae600391e6c1)

#### Menghapus Baris Nilai Kosong

Berdasarkan informasi yang diperoleh pada tahap pemahaman data, pada DataFrame Books terdapat kolom yang bernilai kosong atau null, yaitu kolom Book-Author sebanyak 2 data, Publisher sebanyak 2 data, dan Image-URL-L sebanyak 3 data. Jumlah tersebut tidak signifikan dibandingkan jumlah data yang tersedia, sehingga baris data dengan kolom yang bernilai kosong tersebut dapat dihapus dengan menggunakan fungsi .dropna(), dan jika dilakukan pengecekan kembali, maka tidak ditemukan lagi kolom yang bernilai kosong atau null.

![Gambar13](https://github.com/user-attachments/assets/560b9805-bd56-46b8-b4ce-5328e1690e76)

#### Menghapus Kolom yang Tidak Dibutuhkan

Dikarenakan kolom `Image-URL-S`, `Image-URL-M`, dan `Image-URL-L` tidak dibutuhkan pada saat pemodelan sistem, maka kolom-kolom tersebut bisa dihapus dari DataFrame Books.

![Gambar14](https://github.com/user-attachments/assets/36a616b5-fa48-4a53-a436-88edbab1c9ec)

#### Mengecek Data Duplikat

![Gambar15](https://github.com/user-attachments/assets/6b3524b5-173d-4266-947b-e8260e744ee7)

Berdasarkan informasi, diketahui bahwa tidak terdapat data duplikat pada DataFrame Books.

### Dataset Ratings

#### Menghapus Baris

Pada tahap pemahaman data, diketahui dari hasil visualisasi grafik "Distribusi Rating", sebagian besar data rating dari buku yang sudah pernah dibaca oleh user berada pada rating 0 (lebih dari 700.000-an). Kondisi tersebut dapat menyebabkan bias pada analisis data, sehingga data dengan rating 0 dapat dihapus. Data tersebut tidak akan diikutsertakan dalam DataFrame Ratings, dimana data yang diambil adalah data rating yang lebih besar dari 0, yaitu rating 1 hingga rating 10.

![Gambar16](https://github.com/user-attachments/assets/49ce97fa-84a1-47ac-a98a-51c7318aa13c)

#### Mengecek Data Duplikat

![Gambar17](https://github.com/user-attachments/assets/271a4baa-1535-45da-bf19-925591f4d268)

Berdasarkan informasi, diketahui bahwa tidak terdapat data duplikat pada DataFrame Ratings.

![Gambar18](https://github.com/user-attachments/assets/368250ab-447f-468d-93f0-3a62efda4302)

Berdasarkan hasil visualisasi grafik di atas setelah rating 0 dihapus, dapat dilihat bahwa distribusi data lebih jelas, terutama pada data rating 1 hingga rating 4.

### Dataset Users

#### Memperbaiki Kesalahan Nilai

![Gambar19](https://github.com/user-attachments/assets/c714b2c8-53fc-430c-baf3-5e7d08553087)

Nilai pada kolom Age terdapat nilai abnormal 0 dan nilai di atas 100. Nilai abnormal tersebut diperbaiki dengan melakukan imputasi nilai yang sering muncul atau nilai modus.

#### Menghapus Baris Nilai Kosong

Baris dengan kolom nilai kosong akan dihapus dari DataFrame Users.

![Gambar20](https://github.com/user-attachments/assets/3ef74839-d467-4905-b1e1-dc294f66dbfd)

Visualisasi distribusi nilai dari kolom Age setelah penghapusan nilai kosong.
 
![Gambar21](https://github.com/user-attachments/assets/f652690a-f9b8-4649-9ee4-1882333f1419)

#### Mengganti Tipe Data Kolom

Kolom Age yang bertipe float akan diubah menjadi tipe integer.

![Gambar22](https://github.com/user-attachments/assets/bc2c6db2-d180-4469-802a-02e91fd73ff2)

#### Menghapus Kolom yang Tidak Dibutuhkan

Dikarenakan kolom `Location` tidak dibutuhkan pada saat pemodelan sistem, maka kolom tersebut bisa dihapus dari DataFrame Users.

![Gambar23](https://github.com/user-attachments/assets/f5b55df0-14a0-4959-af50-c216340f9230)

#### Mengecek Data Duplikat

![Gambar24](https://github.com/user-attachments/assets/5874fb4c-c593-4efc-9b3c-c20f9b1d227e)

Berdasarkan informasi, diketahui bahwa tidak terdapat data duplikat pada DataFrame Users.

### Menggabungkan Dataset

Data User-ID terdapat pada DataFrame Ratings dan Users, sehingga dilakukan penggabungan data tersebut pada kolom User-ID. Data ISBN terdapat pada DataFrame Books dan Ratings, sehingga dilakukan penggabungan data tersebut pada kolom ISBN.

![Gambar25](https://github.com/user-attachments/assets/8f085a89-96ac-43cc-8ab5-290555b40aff)

Tabel berikut ini menampilkan 10 judul buku dengan total rating tertinggi.

![Gambar26](https://github.com/user-attachments/assets/f4e687dd-217e-442f-a2e3-75fa8d7e9f1b)

### Mengambil Sampel Data untuk Pemodelan

Pada tahapan sebelumnya, diketahui bahwa jumlah data setelah penggabungan DataFrame tergolong cukup banyak (mencapai 200.000-an data). Hal tersebut akan berdampak pada biaya yang diperlukan untuk melakukan proses pemodelan machine learning, seperti memakan waktu yang lama dan resource RAM ataupun GPU yang cukup besar. Oleh karena itu, pada proyek ini, jumlah data yang akan digunakan untuk proses pemodelan machine learning dibatasi hanya 10.000 baris.

![Gambar27](https://github.com/user-attachments/assets/e6edf763-4e1a-409c-9bed-7a4a4a697fdd)

### Encoding Fitur

Encoding atau penyandian fitur diperlukan agar fitur nonnumerik bisa dipetakan dalam bentuk numerik, karena model machine learning hanya bisa menerima nilai numerik.

![Gambar28](https://github.com/user-attachments/assets/17d6601b-24d9-4e06-9532-6033f86eb622)

### Pembagian Dataset untuk Training dan Validasi

Pembagian ditentukan dengan ukuran data latih 80% dan data uji 20%. Ini diperlukan agar model yang telah dilatih dapat diujikan seberapa akurat hasil prediksinya terhadap data baru. Hasilnya adalah sejumlah 8.000 baris data latih dan 2.000 baris data uji.

![Gambar29](https://github.com/user-attachments/assets/fd5844d4-a51f-4577-8444-3f1c89763e13)

## Modeling

Tahap berikutnya adalah proses modeling atau membuat model machine learning yang dapat digunakan sebagai sistem rekomendasi untuk menentukan rekomendasi buku yang terbaik kepada pengguna dengan algoritme sistem rekomendasi tertentu. Seperti yang telah dituliskan dalam Solution Approach, model machine learning yang digunakan untuk menyelesaikan permasalahan dalam proyek ini adalah algoritme Content-Based Filtering dan Collaborative Filtering.

### Content-Based Filtering

Algoritme ini menghasilkan rekomendasi berdasarkan kemiripan DataFrame dari matriks Cosine Similarity yang sebelumnya didapatkan dari matriks TF-IDF.

#### TF-IDF Vectorizer

TF-IDF Vectorizer akan mentransformasikan teks menjadi representasi angka yang memiliki makna tertentu dalam bentuk matriks.

![Gambar30](https://github.com/user-attachments/assets/6ad239da-8cac-48f7-8b6f-88904800294c)

#### Cosine Similarity

Cosine Similarity akan melakukan perhitungan derajat kesamaan (similarity degree) antar judul buku.

![Gambar31](https://github.com/user-attachments/assets/5b839224-df5f-415f-bc88-550555ff2092)

Selanjutnya fungsi rekomendasi_buku digunakan untuk melakukan komputasi perhitungan kesamaannya dengan nilai k atau jumlah rekomendasi, yaitu 10. 

![Gambar32](https://github.com/user-attachments/assets/9451f4aa-862e-4ef5-88f4-7fb2e3e7258f)

Berikut ini merupakan contoh dari hasil rekomendasi sistem dengan menggunakan algoritme Content-Based Filtering.

![Gambar32_1](https://github.com/user-attachments/assets/142e0803-6863-4598-9b9f-9caa2ed34f35)

Hasil dari algoritme Content-Based Filtering dari buku "Hercule Poirots Weihnachten." yang ditulis oleh "Agatha Christie" menghasilkan 10 buku lain dari penulis yang sama.

### Collaborative Filtering

Model ini menggunakan library Tensorflow Keras untuk mengimpor model RecommenderNet. Model ini perlu dilakukan inisialisasi fungsi sebelum akhirnya dilakukan proses training.

![Gambar33](https://github.com/user-attachments/assets/0c1a9df4-d61a-4577-bc4f-324d23d5156a)

Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan Root Mean Squared Error (RMSE) sebagai metrik evaluasi.

![Gambar34](https://github.com/user-attachments/assets/b4740d71-3ee1-4f16-866b-270081fcdb05)

Selanjutnya divisualisasikan hasil training dan validation error serta training dan validation loss menggunakan grafik plot dengan bantuan library matplotlib.

![Gambar35](https://github.com/user-attachments/assets/20c2f705-9252-4bc3-adbe-fa90701b4ac7)

Perhatikan bahwa proses training model cukup smooth dan model konvergen pada epochs sekitar "100". Dari proses ini diperoleh nilai error akhir sebesar "0.04" dan error pada data validasi sebesar "0.27". Nilai tersebut cukup bagus untuk sistem rekomendasi.

Untuk mendapatkan rekomendasi buku yang akan dihasilkan oleh sistem, diperlukan data atau sampel dari pengguna secara acak dan mendefinisikan variabel buku yang belum pernah dibaca oleh pengguna yang merupakan daftar buku yang nantinya akan direkomendasikan. Daftar tersebut dapat didapatkan dengan menggunakan operator logika bitwise (~) pada variabel buku yang telah dibaca oleh pengguna.



Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.
