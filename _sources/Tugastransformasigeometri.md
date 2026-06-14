# Tugas Transformasi Geometri: Translasi dan Refleksi terhadap Sumbu Y

## Pendahuluan

Pada tugas ini dilakukan transformasi geometri terhadap sebuah bangun persegi. Transformasi yang digunakan terdiri dari dua tahap, yaitu translasi (pergeseran) dan refleksi (pencerminan) terhadap sumbu Y.

Tujuan dari transformasi ini adalah untuk mengetahui perubahan posisi objek setelah dikenai beberapa operasi geometri secara berurutan.

---

## 1. Data Awal

Bangun yang digunakan adalah persegi dengan koordinat titik sebagai berikut:

| Titik | Koordinat |
|--------|-----------|
| A | (1,1) |
| B | (3,1) |
| C | (3,3) |
| D | (1,3) |

Representasi titik dalam koordinat homogen:

$$
P=
\begin{bmatrix}
x\\
y\\
1
\end{bmatrix}
$$

---

## 2. Operasi Translasi

Langkah pertama adalah menggeser seluruh titik sejauh 1 satuan ke arah kanan.

Persamaan translasi:

$$
(x,y)\rightarrow(x+1,y)
$$

Matriks translasi yang digunakan:

$$
T=
\begin{bmatrix}
1 & 0 & 1\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

Sehingga transformasi dapat dituliskan sebagai:

$$
P_1=T \cdot P
$$

### Hasil Translasi

| Titik Awal | Titik Baru |
|------------|------------|
| A(1,1) | (2,1) |
| B(3,1) | (4,1) |
| C(3,3) | (4,3) |
| D(1,3) | (2,3) |

---

## 3. Operasi Refleksi terhadap Sumbu Y

Setelah translasi dilakukan, objek dicerminkan terhadap sumbu Y.

Aturan refleksi:

$$
(x,y)\rightarrow(-x,y)
$$

Matriks refleksi:

$$
R=
\begin{bmatrix}
-1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

Transformasi refleksi:

$$
P_2=R \cdot P_1
$$

### Hasil Refleksi

| Titik Setelah Translasi | Titik Setelah Refleksi |
|------------------------|------------------------|
| (2,1) | (-2,1) |
| (4,1) | (-4,1) |
| (4,3) | (-4,3) |
| (2,3) | (-2,3) |

---

## 4. Komposisi Transformasi

Karena translasi dilakukan terlebih dahulu kemudian refleksi, maka transformasi gabungan dapat dituliskan sebagai:

$$
P' = R \cdot T \cdot P
$$

Dengan:

$$
T=
\begin{bmatrix}
1 & 0 & 1\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

dan

$$
R=
\begin{bmatrix}
-1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

Maka diperoleh:

$$
RT=
\begin{bmatrix}
-1 & 0 & -1\\
0 & 1 & 0\\
0 & 0 & 1
\end{bmatrix}
$$

---

## 5. Bentuk Transformasi Akhir

Dari matriks gabungan diperoleh fungsi transformasi:

$$
(x,y)\rightarrow(-(x+1),y)
$$

Artinya:

1. Titik digeser 1 satuan ke kanan.
2. Hasil pergeseran dicerminkan terhadap sumbu Y.

---

## 6. Simulasi Transformasi

Jika transformasi dilakukan berulang sebanyak n langkah, maka pola perpindahan titik menjadi:

$$
(x,y)\rightarrow(x+n,y)
$$

Kemudian direfleksikan menjadi:

$$
(x,y)\rightarrow(-(x+n),y)
$$

Sebagai contoh:

| Langkah | Koordinat |
|----------|------------|
| Awal | (1,1) |
| 1 | (-2,1) |
| 2 | (-3,1) |
| 3 | (-4,1) |
| ... | ... |

---

## 7. Analisis

Transformasi translasi tidak mengubah bentuk maupun ukuran bangun, hanya mengubah posisinya.

Refleksi terhadap sumbu Y menghasilkan bangun yang simetris terhadap sumbu tersebut. Akibatnya seluruh nilai koordinat x berubah tanda, sedangkan koordinat y tetap.

Karena kedua transformasi dilakukan secara berurutan, posisi akhir objek dipengaruhi oleh hasil translasi sebelumnya.

---

## 8. Kesimpulan

Berdasarkan hasil percobaan dapat disimpulkan bahwa:

- Bangun awal berupa persegi dengan empat titik sudut.
- Translasi menggeser seluruh titik ke arah kanan.
- Refleksi terhadap sumbu Y mengubah tanda koordinat x.
- Bentuk dan ukuran bangun tetap sama selama transformasi.
- Transformasi gabungan dinyatakan sebagai:

$$
P' = R \cdot T \cdot P
$$

dengan hasil akhir:

$$
\boxed{(x,y)\rightarrow(-(x+1),y)}
$$

Transformasi ini menunjukkan bagaimana dua operasi geometri dapat dikombinasikan untuk menghasilkan posisi baru suatu objek pada bidang koordinat.

## Link Google Colab

https://colab.research.google.com/drive/1bXaofTFXfyaRI2C47o_o5KNTYy2VXNFS?usp=sharing

---