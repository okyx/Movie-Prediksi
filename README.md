# Laporan Proyek Machine Learning - Zicola Vladimir

## Project Overview
Untuk mempertahankan suatu layanan video streaming, maka diperlukan sistem rekomendasi film kepada pengguna sehingga mereka cenderung tetap di layanan video yang sama untuk menonton film tersebut, sehingga keuntungan suatu perusahaan dapat dipertahankan atau bahkan meningkat seiring dengan pertambahan jumlah pengguna baru.

## Business Understanding

Bayangkan suatu pengguna tertarik untuk menyewa suatu layanan dikarenakan ada film yang sedang viral di sosial media, tetapi ketika film tersebut telah selesai ditonton maka pengguna tersebut tidak melanjutkan untuk menyewa suatu layanan dikarenakan tidak ada film yang ingin ditonton, untuk itu diperlukan suatu rekomendasi film berdasarkan film yang diberi rating sehingga pengguna tersebut tetap memperpanjang layanan video streaming dan perusahaan akan tetap mendapatkan untung.

### Problem Statements
Berdasarkan permasalahan diatas, akan dikembangkan suatu sistem untuk merekomendasi film, adapun rumusan masalah sebagai berikut.
1. Bagaimana sistem neural network dapat merekomendasikan sebuah film berdasarkan rating yang diberikan pengguna?

### Goals
Untuk menjawab rumusan masalah diatas, maka perlu dibuatkan sistem rekomendasi dengan goals sebagai berikut.
1. Mengetahui bagaimana sistem neural netowrk dapat merekomendasikan film yang kemungkinan besar akan disukai oleh pengguna

### Solution Statement
Untuk menyelesaikan masalah tersebut demi mencapai hasil yang diinginkan maka digunakan algoritma Neural Network untuk mendapatkan embedding layer yang sesuai dengan pengguna dan rating filmnya.
Algoritma ini mudah diterapkan dan tidak memerlukan hidden layer yang dalam, selain itu algoritma ini mudah diimplementasikan dikarenakan mudahnya pengaksesan library tensorflow.
Cara kerja algoritma ini adalah mengupdate bobot embedding layer pada neural network sehingga hasil perkalian dot antara embedding layer pengguna dan embedding layer movie mendekati target rating.

## Data Understanding
Data ini diambil dari kaggle dengan judul Movie Name and Review Data set yang dirilis 2 bulan yang lalu dengan link berikut [Dataset](https://www.kaggle.com/meetnagadia/movie-rating).
Data ini berisi 2 file csv, 1 file csv berisi data rating user terhadap film dengan total baris 105339 dan 4 kolom, lalu file ke-2 berisi data judul film dan genrenya dengan total baris 10329 dan 3 kolom

### Variabel-variabel pada crab age detection dataset adalah sebagai berikut:
File 1 rating.csv
1. userId          : id pengguna
2. movieId         : pid film
3. rating          : rating pengguna terhadap film tersebut
4. timestamp       : tanggal

File 2 movies.csv
1. moviesId        : id film
2. title           : judul film
3. genres          : genre film

Selanjutnya dilakukan pembacaan terhadap 2 file lalu dilakukan rating.info() dan movie.info() untuk melihat apakah terdapat data yang kosong, dan setelah dilakukan tahap tersebut ternyata tidak ada data yang kosong / null.

Pada bar di bawah terlihat bahwa judul film lebih banyak dibandingkan pengguna, tetapi hal ini tidak akan menyebabkan bias pada pelatihan dikarenakan antara pengguna dan film termasuk independent yang artinya tidak mempengaruhi satu sama lain.<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/barplot.PNG)<br>



## Data Preparation
Tahap 1 Normalisasi data : 
dataset rating dinormalisasi dengan rumus sebagai berikut untuk kolom rating.<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/rumus%20standarisasi.PNG)

Tahap 2 One Hot Encoding untuk genres:
setelah dilakukan one hot encoding terdapat movie yang null dengan tulisan no genre maka data tersebut akan di hapus.<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/onehotencoding.PNG)<br>
setelah dihapus berkurang data sebanyak 7 row dari 10329 menjadi 10322


Tahap 3 Penggabungan data:<br>
data dari movie dan rating digabung sehingga hasil akan menjadi seperti ini dan tidak ada null value lalu diambil kolom yang diperlukan untuk model yang akan dibuat. Lalu id untuk movie dan user dikurangi 1 sehingga index dimulai dari 0<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/penggabungan.PNG)

Tahap 4 split data:
pada proyek ini hanya dilakukan split sebanyak 10% dikarenakan data yang ada cukup banyak yakni 10%.



## Modeling
Dalam modelling disini digunakan Model Neural Network dengan embedding layer

Neural Network digunakan untuk mengupdate bobot embedding layer sehingga hasil perkalian dot antara embedding layer user dan layer movie sesuai dengan target yang diingingkan , perlu diketahui bahwa perkalian dot pada matrix akan menghasilkan 1 jika vektor dari user dan vektor dari movie memiliki magnitude yang sama dan melalui pelatihan akan diupdate untuk mendapatkan loss terkecil mungkin.

Adapun plot loss pada pelatihan ini sebagai berikut<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/plot%20loss.png)<br>



pada contoh graph diatas dapat dilihat jika model konvergensi pada awal awal epoch untuk itu sebaiknya menggunakan callback

Berikut top 10 judul film dengan rating tertinggi yang diberikan pengguna:<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/top%2010%20rating.PNG)<br>

Berikut top 10 judul yang direkomendasikan sistem yang telah dibangun:<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/top10%20recom.PNG)<br>






## Evaluation
Metric evaluasi yang digunakan adalah Root Mean Squared, untuk menghitung rata-rata akar perbedaan kuadrat antara target dan prediksi.
adapun rumus Root Mean Squared sebagai berikut<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/metric.PNG)<br>

dilihat dari rumus diatas jika nilai pred mendekati target maka nilai akan mendekati 0 (semakin kecil maka semakin baik)<br>

Dimisalkan ytrue berupa 1, 0.8, dan 0.5 sedangkan ypred yang diprediksi oleh sistem nerural network adalah 0.9, 0.8, 1. Maka perhitungan RSME seperti dibawah ini.<br>
![alt text](https://raw.githubusercontent.com/okyx/Movie-Prediksi/main/gambar/perhitungan%20metric.PNG)<br>



