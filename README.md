
# Data-Manipulating-Language-DML-
```
NIM     : 312310576
NAMA    : TAUFIK HIDAYAT
KELAS   : TI.23.A6
MATKUL  : BASIS DATA
DOSEN   : Agung Nugroho, S.Kom., M.Kom.
```

## Praktikum 1

#### Data Model Mapping

Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)


### Tugas Praktikum

• Buat DDL Script berdasarkan skema ERD tersebut diatas.
• Jalankan script DDL tersebut pada DBMS MySQL.

langkah-langkahnya :

1. buat dulu script untuk table mahasiswa :

``CREATE TABLE Mahasiswa (nim VARCHAR(10) PRIMARY KEY, nama VARCHAR(255) NOT NULL, jenis_kelamin ENUM('Laki-Laki', 'Perempuan'), tgl_lahir DATE,jalan VARCHAR(255) NOT NULL, kota VARCHAR(255) NOT NULL, kodepos VARCHAR(5) NOT NULL, no_hp VARCHAR(15) NOT NULL, kd_ds VARCHAR(10) NOT NULL, FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds))``

![image](ss/ss11.png)

tampilkan hasil table :

``desc mahasiswa;``


![image](ss/ss6.png)

2. buat script untuk table dosen :

``CREATE TABLE Dosen (
    ->     kd_ds VARCHAR(10) PRIMARY KEY,
    ->     nama VARCHAR(255) NOT NULL
    -> );``


![image](ss/ss12.png)


tampiilkan tabel :

``desc dosen;``

![image](ss/ss7.png)

3. buat script untuk mata kuliah :

`` CREATE TABLE Matakuliah (
    ->     kd_mk VARCHAR(10) PRIMARY KEY,
    ->     nama VARCHAR(255) NOT NULL,
    ->     sks INT NOT NULL
    -> );``

![image](ss/ss13.png)


tampilkan table :

``desc Matakuliah;``

![image](ss/ss8.png)

4. buat script untuk jadwal mengajar :

``CREATE TABLE JadwalMengajar (
    ->     kd_ds VARCHAR(10) NOT NULL,
    ->     kd_mk VARCHAR(10) NOT NULL,
    ->     hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    ->     jam TIME NOT NULL,
    ->     ruang VARCHAR(255) NOT NULL,
    ->     PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    ->     FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    ->     FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    -> ); ``


![image](ss/ss14.png)


tampilkan table :

``desc JadwalMengajar;``


![image](ss/ss9.png)


5. buat script untuk KRSMahasiswa :

``CREATE TABLE KRSMahasiswa (
    ->     nim VARCHAR(10) NOT NULL,
    ->     kd_mk VARCHAR(10) NOT NULL,
    ->     kd_ds VARCHAR(10) NOT NULL,
    ->     semester VARCHAR(10) NOT NULL,
    ->     nilai FLOAT NOT NULL,
    ->     PRIMARY KEY (nim, kd_mk),
    ->     FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    ->     FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    ->     FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    -> );``

![image](ss/ss15.png)

tampilkan table :

``desc KRSMahasiswa;``


![image](ss/ss10.png)

berikut script secara keseluruhan :


![image](ss/ss16.png)

## Praktikum 2 Manipulasi Data (DML)
Berdasarkan table Mahasiswa pada praktikum sebelumnya:
(nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)


1. Isi data pada table tersebut sebanyak minimal 5 record data.
Tampilkan semua isi/record tabel!


• Ubah data tanggal lahir mahasiswa yang bernama Ari menjadi: 1979-08-31!


• Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!


• Hapus Mahasiswa yang bernama Dina!


• Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!


• Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!


• Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!


• Tampilkan data nama dan alamat mahasiswa saja dari tabel tersebut


• Tampilkan data mahasiswa terurut berdasarkan nama.


1. Mengisi tabel dengan minimal 5 record data :

``insert into mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values
    -> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""),
    -> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""),
    -> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""),
    -> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""),
    -> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""),
    -> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");``

![image](ss/ss17.png)

2. menampilkan semua isi/record pada tabel bisa menggunakan kode berikut : 


``select*from mahasiswa;``


![image](ss/ss18.png)

3. mengubah data tanggal lahir mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :

``update mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;``


![image](ss/ss19.png)

4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :

``select*from mahasiswa where nim=11223344;``


![image](ss/ss20.png)


5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:

``delete from mahasiswa where nim=11223346;``


![image](ss/ss21.png)


6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :

`` select*from mahasiswa where tgl_lahir<='1996-1-2';``


![image](ss/ss22.png)


7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :


``select * from mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';``


![image](ss/ss23.png)


8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :


`` select * from mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' or tgl_lahir<='1997-01-02' and jenis_kelamin='Perempuan';``


![image](ss/ss24.png)


9. Menampilkan data nama dan jalan mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :


``select nama, jalan from mahasiswa;``


![image](ss/ss25.png)


10. Menampilkan data mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :


`` select * from mahasiswa
    -> order by nama asc;``


![image](ss/ss26.png)



## Evaluasi 

* Tulis semua perintah-perintah SQL percobaan di atas beserta
outputnya!

1. menambah data :

``INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)``

contoh : 


``INSERT INTO biodata (nim, nama, alamat) VALUE ('1234','Rio','Bekasi');``


![image](ss/ss27.png)


2. menampilkan data :


``SELECT * FROM <table>``
``SELECT [field1, ..., fieldn] FROM <table>``

contoh :


``select * from biodata;``


![image](ss/ss28.png)


atau untuk memfilter data gunakan perintah :

``SELECT * FROM WHERE <kondisi>``


![image](ss/ss31.png)




3. mengubah data :

``UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>``

contoh : 

``UPDATE biodata SET nama='Rio', alamat='Bekasi' where nim='123344';``


![image](ss/ss29.png)


4. Menghapus data :

``DELETE FROM <table> WHERE <kondisi>``


contoh :


``DELETE FROM biodata WHERE nim=‘12334’``

![image](ss/ss30.png)



* Apa bedanya penggunaan BETWEEN dan penggunaan operator >=
dan <= ?

• (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')


• (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')


jawab : 

Operator between ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan yntuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>


* Berikan kesimpulan anda! 

jawab :


Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekan diatas.


* Buat laporan praktikum yang berisi, langkah-langkah praktikum
beserta screenshot yang sudah dilakukan dalam bentuk dokumen.

jawab :


laporan terlampir!
