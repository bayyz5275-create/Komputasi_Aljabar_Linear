# Animasi Transformasi Geometri: Translasi & Refleksi

## 📌 Deskripsi Program

Program ini dibuat menggunakan Python untuk menampilkan animasi transformasi geometri berupa:

* **Translasi (pergeseran)**
* **Refleksi terhadap sumbu Y (pencerminan)**

Objek utama berupa **persegi** yang bergerak ke kanan, dan bayangannya selalu muncul secara **simetris di sisi kiri**, seperti efek cermin.

---

## 🔢 Representasi Data

Titik-titik objek disimpan dalam bentuk pasangan koordinat:

```
( x, y )
```

Contoh:

```
A(1,1), B(3,1), C(3,3), D(1,3)
```

Semua titik ini membentuk sebuah persegi.

---

## ➡️ Translasi (Pergeseran)

Fungsi translasi pada program:

```
(x, y) → (x + dx, y)
```

Penjelasan:

* Nilai **x bertambah** → objek bergerak ke kanan
* Nilai **y tetap** → tidak naik atau turun

Pada program:

```
dx = 1
```

Artinya setiap langkah, objek bergeser 1 satuan ke kanan.

---

## 🪞 Refleksi terhadap Sumbu Y

Fungsi refleksi:

```
(x, y) → (-x, y)
```

Penjelasan:

* Posisi x dibalik (kanan ↔ kiri)
* Jarak terhadap sumbu Y tetap sama

Contoh:

```
(4,2) → (-4,2)
```

Ini membuat objek terlihat seperti bayangan di cermin.

---

## 🔁 Proses Perulangan (Animasi)

Program menggunakan perulangan untuk membuat animasi:

### Setiap langkah:

1. Objek digeser ke kanan (translasi)
2. Bayangan dibuat dari posisi terbaru (refleksi)

Urutan ini sangat penting karena:

* Bayangan harus selalu mengikuti objek
* Agar terlihat seperti cermin nyata

---

## 🧠 Kenapa Objek & Bayangan Selalu Sejajar?

Karena setiap titik memenuhi hubungan:

```
x_bayangan = -x_objek
y_bayangan = y_objek
```

Artinya:

* Jarak ke sumbu Y sama
* Posisi saling berlawanan

Hasilnya:

* Objek dan bayangan selalu **simetris**
* Terlihat **sejajar kiri-kanan**

---

## 🎬 Sistem Animasi

Animasi dibuat menggunakan:

```
matplotlib.animation.FuncAnimation
```

Fungsi ini:

* Menjalankan frame secara berulang
* Memanggil fungsi `update()` setiap langkah
* Menampilkan perubahan posisi objek

---

## 🎨 Proses Visualisasi

Setiap frame akan menampilkan:

* 🔵 Objek asli (warna biru)
* 🔴 Bayangan/cermin (warna merah)
* Grid koordinat
* Sumbu X dan Y
* Label titik (A, B, C, D)

---

## ⚙️ Alur Logika Program

Secara sederhana:

```
Objek awal
   ↓
Translasi (geser kanan)
   ↓
Refleksi (buat bayangan)
   ↓
Tampilkan hasil
   ↓
Ulangi
```

---

## 🎯 Kesimpulan

* Translasi mengubah posisi objek
* Refleksi membuat bayangan simetris
* Urutan transformasi menentukan hasil
* Animasi menunjukkan proses secara bertahap

---

## 💡 Ilustrasi Sederhana

Bayangkan kamu berdiri di depan cermin:

* Kamu bergerak ke kanan
* Bayangan kamu bergerak ke kiri
* Posisi tetap sejajar

Program ini bekerja dengan cara yang sama 😊

---

## 🛠️ Teknologi

* Python
* Matplotlib
* Numpy

---
### Berikut ialah Link Google Colaab nya
https://colab.research.google.com/drive/1myENYF1s8OEZET6SuhJC9VYk1ycXmKEK?usp=sharing