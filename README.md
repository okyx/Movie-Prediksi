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
1. Mengetahui film yang akan disukai oleh pengguna

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

Selanjutnya dilakukan pembacaan terhadap 2 file lalu dilakukan pd.info() untuk melihat apakah terdapat data yang kosong, dan setelah dilakukan tahap tersebut ternyata tidak ada data yang kosong / null.

selanjutnya dilakukan describe untuk mengetahui nilai min dan max pada dataset rating untuk normalisasi dengan rumus sebagai berikut.<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/describe1.PNG)
setelah dilakukan terlihat bahwa nilai ada nilai yang valuenya 0 sebanyak 2 baris<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/height0.PNG)


Selanjutnya akan di drop kedua data tersebut

Pada sex terdapat 3 jenis kelamin yaitu M untuk male , F utk female dan I untuk indeterminate atau tidak tentu dan distribusi data untuk ke 3 jenis kelamin seimbang<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/distribusiSex.PNG) 

Pada data numerical terlihat bahwa umur paling banyak terdapat di umur 9 bulan, serta berdistribusi normal<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/distribusiNumerical.png) 

Pada pairplot dan heatmap juga terlihat jelas bahwa data cenderung berkorelasi antar 1 sama lain sehingga akan terjadi multicollinearity , dan tidak bisa hanya dihapus karna hampir semua data berkorelasi sehingga diperlukan teknik pereduksian seperti PCA, karna tidak ada teknik untuk memilih fitur mana yang akan di pertahankan dilihat dari masing masing fitur yang saling berkorelasi<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/pairplot.png)
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/heatmap.png) 

## Data Preparation
Tahap 1 One Hot Encoding: mengubah kolom kategori menjadi numerik. Prefix dan pada kasus ini adalah sex lalu juga menggunakan drop_first untuk menghindari multicollinearity sehingga kolom yang dihasilkan hanya 2 ,misal SEX_F pada kasus ini di drop karna jika SEX_I dan SEX_M sama 0 maka dapat dipastikan bahwa sex kepiting tersebut female<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/sexKepiting.PNG) 


Tahap 2 reduksi PCA, untuk mereduksi data tersebut serta menghilangkan kolom kolom yang berkorelasi sehingga tidak ada multicollinearity di data tersebut. Adapun sum of explained ratio yang saya pakai adalah minimal 90%.<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/pca.png)


Pada grafik diatas terlihat benar bahwa hanya 1 pca yang diperlukan karena memang pada dasarnya semua kolom saling berkorelasi kuat. yang artinya pada dasarnya semua fitur tersebut sama pentingnya untuk menentukan age dan saling berkorelasi sehingga hanya diambil 1 pca saja.

Tahap 3 train test split menjadi data train dan data uji dengan persentase 0.9 dan 0.1 

Tahap 4 standarisasi pada masing masing subset data agar data test tidak menangkap distribusi dari data train sehingga data test akan benar benar independent terhadap data train<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/scaler.PNG)



## Modeling
Dalam modelling disini digunakan 3 jenis model yakni linear regression, KNN dan SVR


Linear Regression digunakan sebagai model dasar dikarenakan kesederhanaaan model tersebut sehingga tidak diperlukan waktu lama untuk membuat model tersebut.

Algoritma kedua yakni KNN yang mudah diterapkan dan termasuk lazy learning sehingga tidak ada pelatihan tetapi pemilihan k harus sesuai sehingga tidak terjadi kesalahan dalam prediksi.

Algoritma ketiga yakni SVR yang merupakan salah satu algoritma kompleks yang baik dalam regression dan termasuk ke dalam keluarga SVM.

Pada percobaan ini digunakan semua parameter default dari library sklearn.

Berdasarkan dari pemakaian 3 algoritma ditemukan bahwa SVR menghasilkan nilai MAE terkecil yang artinya menjadi algortima terbaik pada percobaan ini, ditunjukan pada gambar dibawah<br>




![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/MAE.PNG)




## Evaluation
Metric evaluasi yang digunakan adalah MAE atau mean absolute error
adapun rumus MAE sebagai berikut<br>


![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/persamaan.PNG)<br>
dilihat dari rumus diatas jika nilai ypred mendekati ytrue maka nilai akan mendekati 0 (semakin kecil maka semakin baik)<br>

<br>
<br>



berdasarkan persamaan berikut contoh perhitungan MAE, jika ada 3 data dengan ytrue 10, 11, 12 dan ypred sebesar 10.2, 10.9, 12.6 maka nilai MAE dapat dituliskan sebagai berikut<br>


![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/penyelesaian.PNG)
<br>
dari contoh diatas jika nilai ypred dan ytrue sama persis maka nilai MAE akan 0, maka semakin kecil nilai MAE semakin baik algoritma tersebut dalam memprediksi
<br>
<br>


Berikut hasil MAE pada ketiga algoritma<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/MAE.PNG)


Berdasarkan gambar diatas dapat dilihat bahwa nilai error rata-rata terkecil berada pada algoritma SVR sehingga untuk problem statement ke 2 dapat dipenuhi dengan algoritma SVR yaitu membuat model ML seakurat mungkin 
<br><br>
berikut hasil prediksi 1 sample data test dengan ketiga algoritma<br>
![alt text](https://raw.githubusercontent.com/okyx/crabAge/main/prediksi.PNG)

