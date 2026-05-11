code ini rapikan 
#  Transformasi Matriks 
---
##  Representasi Data

Titik objek disimpan dalam bentuk koordinat:

```
(x, y)
```

Contoh:

```
A(1,1), B(3,1), C(3,3), D(1,3)
```

Titik-titik tersebut membentuk sebuah persegi.

---

##  Translasi (Pergeseran)

Rumus yang digunakan:
```
(x, y) → (x + dx, y)
```
Pada program:
```
dx = 1
```
Maksudnya setiap langkah, objek bergeser 1 satuan ke kanan.
Maksudnya:
* x berubah → objek bergerak horizontal
* y tetap → tidak ada perubahan vertikal

---

##  Translasi dalam Matriks

Dalam bentuk matriks homogen:

[
T =
\begin{bmatrix}
1 & 0 & 1 \
0 & 1 & 0 \
0 & 0 & 1
\end{bmatrix}
]

Dengan:

[
P =
\begin{bmatrix}
x \
y \
1
\end{bmatrix}
]

Maka:

[
P' = T \cdot P
]

 Dan Ini Akan Menghasilkan:

```
(x, y) → (x+1, y)
```

Rumus di program dari bentuk matriks ini.

---

##  Refleksi terhadap Sumbu Y

Rumus refleksi:

```
(x, y) → (-x, y)
```

 Maksudnya itu:

* Posisi x dibalik (kanan ↔ kiri)
* y tetap

Contoh:

```
(4,2) → (-4,2)
```

---

## Refleksi dalam Matriks
[
R =
\begin{bmatrix}
-1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
]

Transformasi:

[
P' = R \cdot P
]

 Hasilnya Akan sama:

```
(x, y) → (-x, y)
```

---

##  Transformasi Gabungan

Urutan transformasi pada program:

1. Translasi
2. Refleksi

Sehingga:

[
P' = R \cdot T \cdot P
]

 Artinya:

* Titik digeser terlebih dahulu
* Kemudian dicerminkan

---

##  Proses Animasi (Loop)

Setiap langkah dalam program:

1. Objek ditranslasi (geser ke kanan)
2. Hasilnya langsung direfleksikan
3. Kedua hasil ditampilkan

 Proses diulang beberapa kali Agar Berbentuk animasi.

---

##  Kenapa Objek dan Bayangan Sejajar ?

Karena hubungan titiknya:

```
x_bayangan = -x_objek
y_bayangan = y_objek
```

Akibatnya:

* Jarak ke sumbu Y sama
* Posisi berlawanan arah


---

## Sistem Animasi

Program menggunakan:

```
matplotlib.animation.FuncAnimation
```

Fungsi ini akan:

* Menjalankan frame secara berulang
* Memperbarui tampilan setiap langkah

---

##  Visualisasi

Setiap frame menampilkan:

* Objek (biru)
* Bayangan (merah)
* Grid koordinat
* Sumbu X dan Y
* Label titik

---

##  Alur Program

```
Objek awal
   ↓
Translasi
   ↓
Refleksi
   ↓
Tampilkan
   ↓
Ulangi
```

---

##  Kesimpulannya ialah 
Program menggunakan dua transformasi: translasi dan refleksi.
Transformasi bisa ditulis dalam bentuk matriks.
Implementasi di kode menggunakan rumus langsung.
Hasil animasi menunjukkan hubungan objek dan bayangannya secara jelas

---

##  Ilustrasi Sederhana

Seperti berdiri di depan cermin:

* Kamu bergerak ke kanan
* Bayangan bergerak ke kiri
* Posisi tetap sejajar


tidak perlu di ubah cukup di rapikan saja 




---
## Link Google Collabnya
 https://colab.research.google.com/drive/1myENYF1s8OEZET6SuhJC9VYk1ycXmKEK?usp=sharing