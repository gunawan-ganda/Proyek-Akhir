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
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
