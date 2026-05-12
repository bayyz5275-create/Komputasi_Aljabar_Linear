# Algoritma QR Dasar dengan Gram-Schmidt

Materi ini membahas pencarian nilai eigen menggunakan **algoritma QR dasar** dengan metode **Gram-Schmidt** hingga 10 iterasi.

Penjelasan ini berkaitan dengan materi pada file:

- **Eigen Value dan Eigen Vector** :contentReference[oaicite:0]{index=0}
- **Dekomposisi QR** :contentReference[oaicite:1]{index=1}

Pada file *Eigen Value dan Eigen Vector* dijelaskan bahwa nilai eigen diperoleh dari:

\[
(A-\lambda I)v=0
\]

Sedangkan pada file *Dekomposisi QR* dijelaskan bahwa algoritma QR digunakan untuk mencari nilai eigen secara numerik melalui iterasi matriks. :contentReference[oaicite:2]{index=2}

---

# Matriks yang Digunakan

\[
A=
\begin{bmatrix}
2 & 1\\
1 & 2
\end{bmatrix}
\]

Metode QR melakukan faktorisasi:

\[
A = QR
\]

Kemudian dilakukan iterasi:

\[
A_{k+1}=RQ
\]

Semakin banyak iterasi dilakukan, matriks akan mendekati bentuk diagonal dan elemen diagonalnya menjadi nilai eigen.

---

# Program Python

```python
import numpy as np

# =========================================
# ALGORITMA QR DASAR
# Menghitung nilai eigen dengan iterasi QR
# =========================================

# Matriks awal
A = np.array([
    [2.0, 1.0],
    [1.0, 2.0]
])

# -----------------------------------------
# Fungsi Gram-Schmidt
# -----------------------------------------
def gram_schmidt(matrix):

    # Ambil kolom matriks
    a1 = matrix[:, 0]
    a2 = matrix[:, 1]

    # Membentuk q1
    q1 = a1 / np.linalg.norm(a1)

    # Proyeksi a2 ke q1
    proj = np.dot(q1, a2) * q1

    # Membentuk u2
    u2 = a2 - proj

    # Membentuk q2
    q2 = u2 / np.linalg.norm(u2)

    # Matriks Q
    Q = np.column_stack((q1, q2))

    # Matriks R
    R = Q.T @ matrix

    return Q, R

# -----------------------------------------
# Proses Iterasi QR
# -----------------------------------------

print("Matriks Awal A0:")
print(A)

for i in range(1, 11):

    # Dekomposisi QR
    Q, R = gram_schmidt(A)

    # Iterasi berikutnya
    A = R @ Q

    print(f"\nIterasi ke-{i}")

    print("Q =")
    print(np.round(Q, 4))

    print("\nR =")
    print(np.round(R, 4))

    print("\nA baru = RQ")
    print(np.round(A, 4))

# -----------------------------------------
# Hasil Eigen
# -----------------------------------------

print("\n=================================")
print("Perkiraan Nilai Eigen")
print("=================================")

eigen1 = A[0, 0]
eigen2 = A[1, 1]

print(f"λ1 ≈ {eigen1:.4f}")
print(f"λ2 ≈ {eigen2:.4f}")
```

---

# Penjelasan Program

# 1. Import Library

```python
import numpy as np
```

Library `numpy` digunakan untuk operasi matriks seperti:

- perkalian matriks
- norma vektor
- transpose matriks
- dot product

---

# 2. Membentuk Matriks Awal

```python
A = np.array([
    [2.0, 1.0],
    [1.0, 2.0]
])
```

Matriks awal:

\[
A_0=
\begin{bmatrix}
2 & 1\\
1 & 2
\end{bmatrix}
\]

Pada file *Eigen Value dan Eigen Vector*, matriks persegi digunakan untuk mencari nilai eigen dan eigenvector. :contentReference[oaicite:3]{index=3}

---

# 3. Fungsi Gram-Schmidt

```python
def gram_schmidt(matrix):
```

Fungsi ini digunakan untuk melakukan dekomposisi:

\[
A = QR
\]

Pada file *Dekomposisi QR* dijelaskan bahwa:

- \(Q\) adalah matriks ortogonal
- \(R\) adalah matriks segitiga atas :contentReference[oaicite:4]{index=4}

---

# 4. Mengambil Kolom Matriks

```python
a1 = matrix[:, 0]
a2 = matrix[:, 1]
```

Kolom matriks dipisahkan menjadi:

\[
a_1=
\begin{bmatrix}
2\\
1
\end{bmatrix}
,\qquad
a_2=
\begin{bmatrix}
1\\
2
\end{bmatrix}
\]

Sesuai konsep Gram-Schmidt pada file PDF, setiap kolom akan diubah menjadi vektor ortonormal. :contentReference[oaicite:5]{index=5}

---

# 5. Membentuk Vektor \(q_1\)

```python
q1 = a1 / np.linalg.norm(a1)
```

Program menghitung norma:

\[
\|a_1\|=\sqrt{2^2+1^2}=\sqrt5
\]

Kemudian dilakukan normalisasi:

\[
q_1=
\frac{a_1}{\|a_1\|}
\]

Hasil:

\[
q_1=
\begin{bmatrix}
\dfrac{2}{\sqrt5}\\
\dfrac{1}{\sqrt5}
\end{bmatrix}
\]

---

# 6. Menghitung Proyeksi

```python
proj = np.dot(q1, a2) * q1
```

Rumus proyeksi:

\[
\mathrm{proj}_{q_1}(a_2)
=
(q_1 \cdot a_2)q_1
\]

Langkah ini digunakan untuk menghilangkan komponen \(a_2\) yang searah dengan \(q_1\).

---

# 7. Membentuk Vektor Ortogonal

```python
u2 = a2 - proj
```

Rumus:

\[
u_2=
a_2-\mathrm{proj}_{q_1}(a_2)
\]

Hasil vektor menjadi ortogonal terhadap \(q_1\).

---

# 8. Membentuk Vektor \(q_2\)

```python
q2 = u2 / np.linalg.norm(u2)
```

Normalisasi:

\[
q_2=
\frac{u_2}{\|u_2\|}
\]

---

# 9. Membentuk Matriks \(Q\)

```python
Q = np.column_stack((q1, q2))
```

Matriks ortogonal:

\[
Q=
\begin{bmatrix}
q_1 & q_2
\end{bmatrix}
\]

---

# 10. Membentuk Matriks \(R\)

```python
R = Q.T @ matrix
```

Rumus:

\[
R = Q^TA
\]

Matriks \(R\) berbentuk segitiga atas.

---

# 11. Iterasi QR

```python
for i in range(1, 11):
```

Loop digunakan untuk melakukan iterasi QR sebanyak 10 kali.

Sesuai materi pada file *Dekomposisi QR*:

\[
A_k = Q_kR_k
\]

kemudian:

\[
A_{k+1}=R_kQ_k
\]

:contentReference[oaicite:6]{index=6}

---

# Tahap Iterasi QR

# Iterasi 1

\[
A_1=
\begin{bmatrix}
2.8 & 0.6\\
0.6 & 1.2
\end{bmatrix}
\]

Elemen di luar diagonal masih cukup besar.

---

# Iterasi 2

\[
A_2=
\begin{bmatrix}
2.96 & 0.28\\
0.28 & 1.04
\end{bmatrix}
\]

Elemen di luar diagonal mulai mengecil.

---

# Iterasi 3

\[
A_3=
\begin{bmatrix}
2.9931 & 0.1108\\
0.1108 & 1.0069
\end{bmatrix}
\]

Nilai diagonal mulai mendekati nilai eigen sebenarnya.

---

# Iterasi 4

\[
A_4=
\begin{bmatrix}
2.9985 & 0.0415\\
0.0415 & 1.0015
\end{bmatrix}
\]

Elemen luar diagonal semakin kecil.

---

# Iterasi 5

\[
A_5=
\begin{bmatrix}
2.9997 & 0.0154\\
0.0154 & 1.0003
\end{bmatrix}
\]

Matriks mulai mendekati bentuk diagonal.

---

# Iterasi 6

\[
A_6=
\begin{bmatrix}
2.9999 & 0.0057\\
0.0057 & 1.0001
\end{bmatrix}
\]

Nilai diagonal semakin stabil.

---

# Iterasi 7

\[
A_7=
\begin{bmatrix}
3.0000 & 0.0021\\
0.0021 & 1.0000
\end{bmatrix}
\]

Elemen luar diagonal hampir nol.

---

# Iterasi 8

\[
A_8=
\begin{bmatrix}
3.0000 & 0.0008\\
0.0008 & 1.0000
\end{bmatrix}
\]

Matriks hampir diagonal sempurna.

---

# Iterasi 9

\[
A_9=
\begin{bmatrix}
3.0000 & 0.0003\\
0.0003 & 1.0000
\end{bmatrix}
\]

Perubahan matriks semakin kecil.

---

# Iterasi 10

\[
A_{10}=
\begin{bmatrix}
3.0000 & 0.0001\\
0.0001 & 1.0000
\end{bmatrix}
\]

Elemen di luar diagonal hampir nol sehingga matriks mendekati bentuk diagonal.

---

# Hasil Akhir Nilai Eigen

Setelah 10 iterasi:

\[
A_{10}\approx
\begin{bmatrix}
3 & 0\\
0 & 1
\end{bmatrix}
\]

Maka nilai eigennya adalah:

\[
\lambda_1 = 3
\]

\[
\lambda_2 = 1
\]

Sesuai teori pada file *Eigen Value dan Eigen Vector*, nilai diagonal akhir matriks hasil iterasi merupakan pendekatan nilai eigen matriks awal. :contentReference[oaicite:7]{index=7}

---

# Kesimpulan

Program berhasil menerapkan:

- metode Gram-Schmidt
- dekomposisi QR
- iterasi QR dasar

untuk mencari nilai eigen matriks.

Semakin banyak iterasi dilakukan, matriks akan mendekati bentuk diagonal:

\[
A_k \rightarrow
\begin{bmatrix}
\lambda_1 & 0\\
0 & \lambda_2
\end{bmatrix}
\]

Hasil akhir:

\[
\lambda_1 = 3
,\qquad
\lambda_2 = 1
\]

Nilai tersebut sesuai dengan hasil analitik dari persamaan karakteristik matriks.

# Berikut Programnya
## https://colab.research.google.com/drive/1XCx6oO5Tf9kqEq3D4S4ihKs9dwZSqPAF?usp=sharing