# Laporan Proyek Machine Learning - Zicola Vladimir

## Domain Proyek
Untuk mempertahankan suatu layanan video streaming, maka diperlukan sistem rekomendasi film kepada pengguna sehingga mereka cenderung tetap di layanan video yang sama untuk menonton film tersebut, sehingga keuntungan suatu perusahaan dapat dipertahankan atau bahkan meningkat seiring dengan pertambahan jumlah pengguna baru.

## Business Understanding

Bayangkan suatu pengguna tertarik untuk menyewa suatu layanan dikarenakan ada film yang sedang viral di sosial media, tetapi ketika film tersebut telah selesai ditonton maka pengguna tersebut tidak melanjutkan untuk menyewa suatu layanan dikarenakan tidak ada film yang ingin ditonton, untuk itu diperlukan suatu rekomendasi film berdasarkan film yang diberi rating sehingga pengguna tersebut tetap memperpanjang layanan video streaming dan perusahaan akan tetap mendapatkan untung.

### Problem Statements
Berdasarkan permasalahan diatas, akan dikembangkan suatu sistem untuk merekomendasi film, adapun rumusan masalah sebagai berikut.
1. film apa yang kemungkinan bakalan disukai oleh pengguna?

### Goals
Untuk menjawab rumusan masalah diatas, maka perlu dibuatkan sistem rekomendasi dengan goals sebagai berikut.
1. Mengetahui film yang kemungkinan besar akan disukai oleh pengguna

### Solution Statement
Untuk menyelesaikan masalah tersebut demi mencapai hasil yang diinginkan maka digunakan algoritma Neural Network untuk mendapatkan embedding layer yang sesuai dengan pengguna dan rating filmnya.

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




## Data Preparation
Tahap 1 Normalisasi data : 
dataset rating dinormalisasi dengan rumus sebagai berikut untuk kolom rating.<br>
![alt text](https://github.com/okyx/Movie-Prediksi/blob/main/gambar/rumus%20standarisasi.PNG)

Tahap 2 One Hot Encoding untuk genres:
setelah dilakukan one hot encoding terdapat movie yang null dengan tulisan no genre maka data tersebut akan di hapus.<br>
![alt text](https://github.com/okyx/Movie-Prediksi/blob/main/gambar/onehotencoding.PNG)<br>
setelah dihapus berkurang data sebanyak 7 row dari 10329 menjadi 10322


Tahap 3 Penggabungan data:<br>
data dari movie dan rating digabung sehingga hasil akan menjadi seperti ini dan tidak ada null value lalu diambil kolom yang diperlukan untuk model yang akan dibuat. Lalu id untuk movie dan user dikurangi 1 sehingga index dimulai dari 0<br>
![alt text](https://github.com/okyx/Movie-Prediksi/blob/main/penggabungan.PNG)

Tahap 4 split data:
pada proyek ini hanya dilakukan split sebanyak 10% dikarenakan data yang ada cukup banyak yakni 10%.



## Modeling
Dalam modelling disini digunakan Model Neural Network dengan embedding layer

Neural Network digunakan untuk mengupdate bobot embedding layer sehingga hasil perkalian dot antara embedding layer user dan layer movie sesuai dengan target yang diingingkan , perlu diketahui bahwa perkalian dot pada matrix akan menghasilkan 1 jika vektor dari user dan vektor dari movie memiliki magnitude yang sama dan melalui pelatihan akan diupdate untuk mendapatkan loss terkecil mungkin.

Adapun plot loss pada pelatihan ini sebagai berikut
![alt text](https://github.com/okyx/Movie-Prediksi/blob/main/gambar/plot%20loss.png)<br>



pada contoh graph diatas dapat dilihat jika model konvergensi pada awal awal epoch untuk itu sebaiknya menggunakan callback


## Evaluation
Metric evaluasi yang digunakan adalah binary cross entropy dikarenakan fungsi ini baik untuk menghitung nilai dari 0 - 1
adapun rumus binary cross entropy sebagai berikut<br>
![alt text](https://github.com/okyx/Movie-Prediksi/blob/main/gambar/loss%20function.PNG)<br>

dilihat dari rumus diatas jika nilai pred mendekati target maka nilai akan mendekati 0 (semakin kecil maka semakin baik)<br>
dimisalkan target 1 dan predict 1 maka berdasarkan rumus diatas maka <br>
loss = -(1 * log(1) + (1-1) * log(1-1))<br>
loss = - (log(1))
loss = 0
<br>
<br>


