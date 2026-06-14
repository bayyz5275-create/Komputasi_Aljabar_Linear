# Tugas Eigen Value dan Eigen Vektor dengan Dekomposisi QR (8)

## Link Google Colab

https://colab.research.google.com/drive/1Nb7MoC5RzdQFF833btc5nUpd7BSr5LY8?usp=sharing

Materi ini membahas proses mencari nilai eigen dan vektor eigen menggunakan metode **Dekomposisi QR** dengan proses **Gram-Schmidt** dan **Iterasi QR** sebanyak 10 kali.

Diberikan matriks:

$$
A=
\begin{bmatrix}
4 & 1\\
2 & 3
\end{bmatrix}
$$

---

## Tahap 1 — Menentukan Matriks Awal

Matriks awal:

$$
A=
\begin{bmatrix}
4 & 1\\
2 & 3
\end{bmatrix}
$$

Kolom-kolom matriks:

$$
a_1=
\begin{bmatrix}
4\\
2
\end{bmatrix}
$$

$$
a_2=
\begin{bmatrix}
1\\
3
\end{bmatrix}
$$

Metode QR akan memfaktorkan:

$$
A = QR
$$

dengan:

- $Q$ = matriks ortogonal
- $R$ = matriks segitiga atas

---

## Tahap 2 — Membentuk Vektor $q_1$

Norma kolom pertama:

$$
\|a_1\|
=
\sqrt{4^2+2^2}
$$

$$
=
\sqrt{20}
$$

$$
=
2\sqrt5
$$

Vektor ortonormal pertama:

$$
q_1
=
\frac{a_1}{\|a_1\|}
$$

$$
=
\begin{bmatrix}
\frac{4}{2\sqrt5}\\
\frac{2}{2\sqrt5}
\end{bmatrix}
$$

$$
=
\begin{bmatrix}
\frac{2}{\sqrt5}\\
\frac{1}{\sqrt5}
\end{bmatrix}
$$

---

## Tahap 3 — Menghitung Proyeksi $a_2$

Hitung hasil dot product:

$$
q_1 \cdot a_2
$$

$$
=
\frac{2}{\sqrt5}(1)
+
\frac{1}{\sqrt5}(3)
$$

$$
=
\frac5{\sqrt5}
$$

$$
=
\sqrt5
$$

Proyeksi:

$$
\text{proj}_{q_1}(a_2)
=
(q_1 \cdot a_2)q_1
$$

$$
=
\sqrt5
\begin{bmatrix}
\frac2{\sqrt5}\\
\frac1{\sqrt5}
\end{bmatrix}
$$

$$
=
\begin{bmatrix}
2\\
1
\end{bmatrix}
$$

---

## Tahap 4 — Membentuk Vektor Ortogonal $u_2$

Rumus:

$$
u_2
=
a_2-\text{proj}_{q_1}(a_2)
$$

$$
=
\begin{bmatrix}
1\\
3
\end{bmatrix}
-
\begin{bmatrix}
2\\
1
\end{bmatrix}
$$

$$
=
\begin{bmatrix}
-1\\
2
\end{bmatrix}
$$

---

## Tahap 5 — Membentuk Vektor $q_2$

Norma:

$$
\|u_2\|
=
\sqrt{(-1)^2+2^2}
$$

$$
=
\sqrt5
$$

Normalisasi:

$$
q_2
=
\frac{u_2}{\|u_2\|}
$$

$$
=
\begin{bmatrix}
-\frac1{\sqrt5}\\
\frac2{\sqrt5}
\end{bmatrix}
$$

---

## Tahap 6 — Membentuk Matriks $Q$

$$
Q=
\begin{bmatrix}
\frac2{\sqrt5} & -\frac1{\sqrt5}\\
\frac1{\sqrt5} & \frac2{\sqrt5}
\end{bmatrix}
$$

Dalam bentuk desimal:

$$
Q
\approx
\begin{bmatrix}
0.8944 & -0.4472\\
0.4472 & 0.8944
\end{bmatrix}
$$

---

## Tahap 7 — Membentuk Matriks $R$

Rumus:

$$
R=Q^TA
$$

Hasil:

$$
R=
\begin{bmatrix}
2\sqrt5 & \sqrt5\\
0 & \sqrt5
\end{bmatrix}
$$

Dalam bentuk desimal:

$$
R
\approx
\begin{bmatrix}
4.4721 & 2.2361\\
0 & 2.2361
\end{bmatrix}
$$

---

## Tahap 8 — Verifikasi Dekomposisi QR

Rumus:

$$
A = QR
$$

Perkalian:

$$
QR=
\begin{bmatrix}
4 & 1\\
2 & 3
\end{bmatrix}
$$

Hasil sama dengan matriks awal sehingga dekomposisi QR benar.

---

## Tahap 9 — Iterasi QR hingga 10 Kali

Proses QR dilakukan terus menerus:

$$
A_k = Q_kR_k
$$

kemudian:

$$
A_{k+1}=R_kQ_k
$$

### Iterasi 1

$$
A_1=
\begin{bmatrix}
4.8 & 0.4\\
0.4 & 2.2
\end{bmatrix}
$$

### Iterasi 2

$$
A_2=
\begin{bmatrix}
4.9756 & 0.1098\\
0.1098 & 2.0244
\end{bmatrix}
$$

### Iterasi 3

$$
A_3=
\begin{bmatrix}
4.9984 & 0.0280\\
0.0280 & 2.0016
\end{bmatrix}
$$

### Iterasi 4

$$
A_4=
\begin{bmatrix}
4.9999 & 0.0070\\
0.0070 & 2.0001
\end{bmatrix}
$$

### Iterasi 5

$$
A_5=
\begin{bmatrix}
5.0000 & 0.0018\\
0.0018 & 2.0000
\end{bmatrix}
$$

### Iterasi 6

$$
A_6=
\begin{bmatrix}
5.0000 & 0.0004\\
0.0004 & 2.0000
\end{bmatrix}
$$

### Iterasi 7

$$
A_7=
\begin{bmatrix}
5.0000 & 0.0001\\
0.0001 & 2.0000
\end{bmatrix}
$$

### Iterasi 8

$$
A_8=
\begin{bmatrix}
5.0000 & 0.0000\\
0.0000 & 2.0000
\end{bmatrix}
$$

### Iterasi 9

$$
A_9=
\begin{bmatrix}
5.0000 & 0.0000\\
0.0000 & 2.0000
\end{bmatrix}
$$

### Iterasi 10

$$
A_{10}=
\begin{bmatrix}
5.0000 & 0.0000\\
0.0000 & 2.0000
\end{bmatrix}
$$

Terlihat bahwa elemen di luar diagonal semakin mendekati nol.

---

## Tahap 10 — Menentukan Nilai Eigen

Setelah 10 iterasi:

$$
A_{10}
\approx
\begin{bmatrix}
5 & 0\\
0 & 2
\end{bmatrix}
$$

Maka nilai eigennya adalah:

$$
\lambda_1 = 5
$$

$$
\lambda_2 = 2
$$

---

## Tahap 11 — Menentukan Vektor Eigen

Persamaan karakteristik:

$$
\det(A-\lambda I)=0
$$

$$
\begin{vmatrix}
4-\lambda & 1\\
2 & 3-\lambda
\end{vmatrix}
=0
$$

$$
(4-\lambda)(3-\lambda)-2=0
$$

$$
\lambda^2-7\lambda+10=0
$$

$$
(\lambda-5)(\lambda-2)=0
$$

Untuk $\lambda = 5$ diperoleh:

$$
v_1=
\begin{bmatrix}
1\\
1
\end{bmatrix}
$$

Untuk $\lambda = 2$ diperoleh:

$$
v_2=
\begin{bmatrix}
-1\\
2
\end{bmatrix}
$$

---

## Kesimpulan

Metode Dekomposisi QR berhasil menemukan nilai eigen matriks:

$$
A=
\begin{bmatrix}
4 & 1\\
2 & 3
\end{bmatrix}
$$

melalui proses Gram-Schmidt dan Iterasi QR.

Hasil akhirnya adalah:

$$
\lambda_1 = 5
$$

$$
\lambda_2 = 2
$$

dengan vektor eigen:

$$
v_1=
\begin{bmatrix}
1\\
1
\end{bmatrix}
$$

$$
v_2=
\begin{bmatrix}
-1\\
2
\end{bmatrix}
$$

Semakin banyak iterasi dilakukan, matriks akan semakin mendekati bentuk diagonal sehingga nilai diagonalnya menjadi pendekatan nilai eigen matriks awal.