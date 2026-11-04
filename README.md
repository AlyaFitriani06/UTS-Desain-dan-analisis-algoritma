# UTS-Desain-dan-analisis-algoritma
Analisis data dan prediksi kelulusan mahasiswa menggunakan machine learning

Nama: Alya Fitriani 

NIM: TI22250004

 => Tujuan dari analisis ini adalah:
1. Memahami karakteristik dan struktur dataset mahasiswa.
2. Mengidentifikasi data kosong, data duplikat, dan nilai yang tidak sesuai.
3. Mengetahui distribusi setiap variabel dalam dataset.
4. Menganalisis hubungan antarvariabel.
5. Menyiapkan dataset agar dapat digunakan untuk analisis selanjutnya.

Dataset yang digunakan dalam proyek ini adalah `original.csv`, yang terdiri dari 87 baris dan 22 kolom sebelum proses pembersihan data.
=> Dataset memiliki beberapa kelompok variabel, yaitu:
1. Demografi: Gender dan Age.
2. Latar Belakang Wilayah: POLAR4 Quintile, POLAR3 Quintile, Adult HE 2001 Quintile, Adult HE 2011 Quintile, TUNDRA MSOA Quintile, TUNDRA LSOA Quintile, Gaps GCSE Quintile, Gaps GCSE Ethnicity Quintile, dan Uni Connect Target Ward.
3. Keterlibatan Belajar: Attending from Home, Distance to University, Count of Module Area Logins, Total Hours in Module Area, % of Average Hours in Module Area, # of Presence, # of Absence, dan Percent Attended.

=> Variabel target yang digunakan adalah `label`, dengan keterangan:
a. `0` = Lulus (Pass).
b. `1` = Gagal (Fail).
Berdasarkan distribusi label, terdapat 68 mahasiswa lulus (85%) dan 12 mahasiswa gagal (15%).

=> Tahap Data Understanding dilakukan untuk memahami struktur dan karakteristik dataset menggunakan Python, terutama library Pandas dan NumPy.
# Beberapa proses yang dilakukan meliputi:
1. Memuat dataset menggunakan `pd.read_csv()`.
2. Menampilkan beberapa baris awal menggunakan `df.head()`.
3. Mengetahui jumlah baris dan kolom menggunakan `df.shape`.
4. Memeriksa tipe data dan informasi setiap kolom menggunakan `df.info()`.
5. Melihat ringkasan statistik menggunakan `df.describe()`.
6. Mengidentifikasi variabel fitur dan variabel target.
7. Memeriksa jumlah data berdasarkan kategori kelulusan menggunakan `value_counts()`.
Dari tahap ini diketahui bahwa dataset memiliki 87 baris dan 22 kolom dengan variabel yang menggambarkan karakteristik serta keterlibatan belajar mahasiswa.

=> Tahap EDA dilakukan untuk memahami pola, distribusi, dan hubungan antarvariabel serta mengidentifikasi permasalahan dalam dataset.
a. Pemeriksaan Data Kosong
Ditemukan 7 baris yang seluruh nilainya kosong dan 2 kolom yang seluruh datanya kosong. Setelah baris dan kolom tersebut dihapus, jumlah data menjadi 80 baris.
Selain itu, ditemukan 2 nilai kosong pada kolom `# of Absence`. Nilai tersebut ditangani menggunakan median.

b. Pemeriksaan Data Duplikat
Ditemukan 6 baris data duplikat dalam dataset. Data tersebut diidentifikasi sebagai bagian dari pemeriksaan kualitas data.

c. Pemeriksaan Nilai Nol
Ditemukan 14 nilai nol pada beberapa kolom quintile, yaitu:
1. Adult HE 2011 Quintile: 2 nilai.
2. TUNDRA MSOA Quintile: 2 nilai.
3. TUNDRA LSOA Quintile: 2 nilai.
4. Gaps GCSE Quintile: 4 nilai.
5. Gaps GCSE Ethnicity Quintile: 4 nilai.
Nilai tersebut diperiksa berdasarkan label dan tidak langsung dihapus karena masih dipertahankan sebagai bagian dari informasi dataset.

d. Analisis Distribusi Data
Berdasarkan histogram pada kolom `Percent Attended`, sebagian besar mahasiswa memiliki persentase kehadiran yang tinggi, yaitu sekitar 90–100%.
Hasil boxplot menunjukkan bahwa persentase kehadiran berada pada rentang sekitar 0–100%, dengan median sekitar 84%. Tidak terlihat titik pencilan yang terpisah pada variabel tersebut.

e. Perbandingan Keterlibatan Belajar
Perbandingan dilakukan terhadap variabel `Percent Attended`, `Count of Module Area Logins`, dan `Total Hours in Module Area`.
Hasil analisis menunjukkan bahwa mahasiswa yang lulus cenderung memiliki median persentase kehadiran lebih tinggi. Sementara itu, distribusi jumlah login dan total jam belajar antara mahasiswa lulus dan gagal terlihat relatif berdekatan.

f. Analisis Korelasi
=> Beberapa hubungan korelasi yang ditemukan dalam dataset adalah:
1. TUNDRA MSOA Quintile dan TUNDRA LSOA Quintile memiliki korelasi 1,00.
2. Gaps GCSE Quintile dan Gaps GCSE Ethnicity Quintile memiliki korelasi 0,93.
3. POLAR3 Quintile dan Adult HE 2001 Quintile memiliki korelasi 0,90.
4. Uni Connect Target Ward dan POLAR4 Quintile memiliki korelasi -0,57.
Hasil ini menunjukkan adanya hubungan yang kuat pada beberapa variabel.

g. Identifikasi Outlier
Pemeriksaan outlier menggunakan metode IQR menemukan beberapa nilai pencilan pada variabel numerik, yaitu Age sebanyak 6, Distance to University sebanyak 7, Count of Module Area Logins sebanyak 2, Total Hours in Module Area sebanyak 3, % of Average Hours in Module Area sebanyak 4, # of Presence sebanyak 2, dan # of Absence sebanyak 2.
Sementara itu, variabel Percent Attended tidak menunjukkan adanya outlier berdasarkan metode tersebut. Nilai pencilan yang ditemukan tidak langsung dihapus karena perlu mempertimbangkan karakteristik dan informasi pada dataset.

h. Pemeriksaan Nilai Negatif
Pemeriksaan dilakukan terhadap variabel numerik untuk mengetahui apakah terdapat nilai negatif. Hasilnya tidak ditemukan nilai negatif pada variabel yang diperiksa.

=> Tahap Data Preparation dilakukan untuk mempersiapkan dataset sebelum digunakan pada proses analisis selanjutnya.
# Beberapa proses yang dilakukan adalah:
1. Menghapus 7 baris yang seluruh nilainya kosong.
2. Menghapus 2 kolom yang seluruh datanya kosong.
3. Menangani 2 nilai kosong pada kolom `# of Absence` menggunakan median.
Menghapus kolom `TUNDRA LSOA Quintile` karena memiliki korelasi sempurna sebesar 1,00 dengan `TUNDRA MSOA Quintile`, sehingga kedua variabel memiliki informasi yang sama. Memisahkan variabel fitur (X) dan variabel target (y).Setelah proses tersebut, dataset memiliki 80 baris dengan 18 variabel fitur dan 1 variabel target.

=> Kesimpulan
Berdasarkan hasil analisis, dataset awal memiliki 87 baris dan 22 kolom. Setelah dilakukan pemeriksaan dan pembersihan, jumlah data menjadi 80 baris karena terdapat 7 baris kosong dan 2 kolom kosong yang dihapus.
Hasil EDA menunjukkan bahwa sebagian besar mahasiswa memiliki persentase kehadiran yang tinggi. Analisis juga menemukan beberapa hubungan korelasi yang kuat antarvariabel, nilai kosong, data duplikat, serta beberapa nilai pencilan.
Nilai kosong pada kolom `# of Absence` ditangani menggunakan median. Sementara itu, nilai nol dan outlier diperiksa tanpa langsung dihapus agar informasi dalam dataset tetap dipertahankan.
Pada tahap Data Preparation, kolom `TUNDRA LSOA Quintile` dihapus karena memiliki informasi yang sama dengan `TUNDRA MSOA Quintile`. Dataset kemudian dipisahkan menjadi 18 variabel fitur dan 1 variabel target.
