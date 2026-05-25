---
tittle: Sistem Pengenalan Wajah Menggunakan Eigenface dan SVD

---

# Sistem Pengenalan Wajah Menggunakan Eigenface dan SVD

Eigenface merupakan metode pengenalan wajah yang memanfaatkan teknik reduksi dimensi untuk menemukan pola utama dari kumpulan citra wajah. Metode ini dibangun berdasarkan konsep **Principal Component Analysis (PCA)** dan pada implementasinya dihitung menggunakan **Singular Value Decomposition (SVD)**.

Tujuan utama metode ini adalah:
- mengurangi ukuran data citra,
- mengambil fitur penting wajah,
- dan mengenali identitas wajah berdasarkan kemiripan fitur.

---

## Dasar Teori Eigenface

Pada komputer, gambar direpresentasikan sebagai kumpulan angka piksel.

Jika sebuah citra memiliki ukuran:

$$
H \times W
$$

maka jumlah total piksel adalah:

$$
N = H \times W
$$

Setiap gambar kemudian diubah menjadi sebuah vektor berdimensi:

$$
1 \times N
$$

Jika terdapat:
- $M$ gambar wajah,
- masing-masing memiliki $N$ piksel,

maka seluruh dataset dapat dibentuk menjadi matriks:

$$
X \in \mathbb{R}^{M \times N}
$$

Setiap baris matriks mewakili satu wajah.

---

## Tahapan Metode Eigenface

### 1. Konversi Gambar Menjadi Vektor

Semua gambar wajah diubah menjadi bentuk vektor agar dapat diproses secara matematis.

Contoh:
- gambar `120 × 120`
- menjadi vektor `1 × 14400`

Implementasi (`main.cpp`):

```cpp
Mat vectorImage = face.reshape(1, 1);

vectorImage.convertTo(vectorImage, CV_32F);

trainingData.push_back(vectorImage);
```

Penjelasan:
- `reshape(1,1)` mengubah matriks gambar menjadi satu dimensi.
- `CV_32F` digunakan agar operasi numerik lebih stabil.
- data disimpan ke matriks pelatihan.

---

### 2. Menghitung Wajah Rata-rata (Average Face)

Sistem menghitung rata-rata seluruh wajah pada dataset.

Persamaan:

$$
\mu = \frac{1}{M}\sum_{i=1}^{M} x_i
$$

Keterangan:
- $\mu$ = mean face
- $M$ = jumlah citra
- $x_i$ = citra ke-$i$

Implementasi (`eigenface.cpp`):

```cpp
reduce(trainingData, meanFace, 0, REDUCE_AVG);
```

Penjelasan:
- sistem mencari nilai rata-rata pada setiap kolom piksel.
- hasilnya adalah pola wajah umum dari dataset.

---

### 3. Centering Data

Setelah mean face diperoleh, setiap gambar dikurangi dengan rata-rata wajah.

Rumus:

$$
A_i = x_i - \mu
$$

Tujuan:
- menghilangkan informasi umum,
- memperjelas ciri khas masing-masing wajah.

Implementasi:

```cpp
Mat normalized;

for (int i = 0; i < trainingData.rows; i++) {

    normalized.push_back(
        trainingData.row(i) - meanFace
    );
}
```

Penjelasan:
- data hasil pengurangan disebut *centered data*.
- matriks ini digunakan pada proses PCA/SVD.

---

### 4. Dekomposisi Menggunakan SVD

Matriks hasil normalisasi kemudian diproses menggunakan Singular Value Decomposition.

Persamaan SVD:

$$
A = U \Sigma V^T
$$

Keterangan:
- $U$ = basis hubungan antar data
- $\Sigma$ = nilai singular
- $V^T$ = eigenvector utama

Baris-baris pada matriks:

$$
V^T
$$

disebut sebagai **Eigenfaces**.

Implementasi (`eigenface.cpp`):

```cpp
SVD svd(
    normalized,
    SVD::FULL_UV
);

eigenfaces = svd.vt.rowRange(
    0,
    totalComponents
);
```

Penjelasan:
- hanya beberapa eigenvector utama yang digunakan.
- semakin besar nilai singular, semakin penting fitur tersebut.

---

## Konsep Eigenface

Eigenface bukan gambar wajah manusia secara langsung, melainkan representasi statistik dari pola wajah.

Ciri yang biasanya muncul:
- bentuk mata,
- struktur hidung,
- kontur wajah,
- pencahayaan,
- dan tekstur wajah.

Eigenface menjadi dasar pembentukan ruang fitur wajah (*face space*).

---

### 5. Proyeksi ke Face Space

Semua gambar dipetakan ke ruang fitur berdimensi rendah.

Persamaan:

$$
y = A \times V^T
$$

Keterangan:
- $y$ = representasi fitur wajah
- $A$ = data hasil normalisasi
- $V^T$ = eigenface

Implementasi:

```cpp
Mat centered = sample - meanFace;

Mat feature = centered * eigenfaces.t();
```

Penjelasan:
- gambar wajah berubah menjadi data fitur kecil.
- proses ini mempercepat pencarian dan pengenalan wajah.

---

### 6. Identifikasi Wajah

Untuk mengenali wajah baru:
1. gambar diproyeksikan ke face space,
2. hitung jarak ke seluruh data latih,
3. ambil jarak terkecil.

Metode jarak yang digunakan adalah Euclidean Distance.

Rumus:

$$
Distance = \sqrt{\sum_{i=1}^{n}(p_i-q_i)^2}
$$

Implementasi:

```cpp
double distance = norm(
    inputFeature,
    savedFeature,
    NORM_L2
);

if (distance < bestDistance) {

    bestDistance = distance;

    bestLabel = labels[i];
}
```

Penjelasan:
- semakin kecil jarak,
- semakin mirip kedua wajah tersebut.

---

## Implementasi Sistem

Program dibangun menggunakan:
- C++
- OpenCV
- Webcam
- Haar Cascade
- Eigenface + SVD

Tahapan kerja sistem:
1. membaca dataset wajah,
2. preprocessing gambar,
3. training Eigenface,
4. mendeteksi wajah dari kamera,
5. melakukan prediksi identitas secara real-time.


---

## Tahapan Preprocessing

Sebelum diproses, gambar wajah melalui beberapa tahap:

### Grayscale

Mengubah gambar berwarna menjadi abu-abu.

```cpp
cvtColor(frame, gray, COLOR_BGR2GRAY);
```

---

### Resize

Menyamakan ukuran seluruh gambar.

```cpp
resize(face, face, Size(100,100));
```

---

### Histogram Equalization

Meningkatkan kualitas kontras gambar.

```cpp
equalizeHist(face, face);
```

---

## Struktur Fungsi Utama

### `train()`

Berfungsi untuk:
- menghitung mean face,
- normalisasi data,
- menjalankan SVD,
- menyimpan eigenface.

---

### `project()`

Berfungsi untuk:
- memproyeksikan wajah ke ruang fitur.

---

### `predict()`

Berfungsi untuk:
- menghitung kemiripan,
- mencari jarak minimum,
- menentukan identitas wajah.

---

## Diagram Alur Sistem

```text
Dataset Wajah
      ↓
Preprocessing
      ↓
Konversi ke Vektor
      ↓
Mean Face
      ↓
Normalisasi Data
      ↓
SVD
      ↓
Eigenface
      ↓
Face Space
      ↓
Perhitungan Jarak
      ↓
Prediksi Identitas
```

---

## Kesimpulan

Metode Eigenface menggunakan PCA dan SVD untuk mengekstraksi fitur penting dari wajah manusia.

Keunggulan:
- proses cepat,
- penggunaan memori ringan,
- mudah dipahami untuk pembelajaran computer vision.

Kekurangan:
- sensitif terhadap cahaya,
- kurang baik pada perubahan pose,
- kurang stabil untuk ekspresi berbeda.

Walaupun termasuk metode lama, Eigenface tetap menjadi fondasi penting dalam perkembangan sistem pengenalan wajah modern.


 Copy Link Tersebut Untuk Melihat contoh programnya [Demo HTML Eigenface](file:///C:/Users/Pongo/Downloads/kal.html)