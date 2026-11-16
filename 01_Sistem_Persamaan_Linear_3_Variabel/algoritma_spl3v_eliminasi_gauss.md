# ALGORITMA PENYELESAIAN SISTEM PERSAMAAN LINEAR TIGA VARIABEL (SPL 3V)
## METODE ELIMINASI GAUSS DENGAN PIVOTING PARSIAL DAN SUBSTITUSI MUNDUR

- **Mata Kuliah** : Komputasi Numerik
- **Topik**       : Sistem Persamaan Linear (SPL) Tiga Variabel
- **Metode**      : Eliminasi Gauss dengan Partial Pivoting & Back Substitution
- **Penyusun**    : Fahri Adis Al Hafni (NIM: 202511420105)
- **Program Studi**: Teknik Informatika - Fakultas Teknik
- **Institusi**   : Universitas Dr. Soetomo (Unitomo) Surabaya

---

## 1. Landasan Teori dan Formulasi Masalah

Sistem Persamaan Linear Tiga Variabel (SPL 3V) merupakan kumpulan tiga persamaan aljabar linear yang melibatkan tiga variabel yang belum diketahui ($x_1, x_2, x_3$ atau $x, y, z$). Bentuk umum SPL 3V dinyatakan sebagai berikut:

$$
\begin{aligned}
a_{11}x_1 + a_{12}x_2 + a_{13}x_3 &= b_1 \\
a_{21}x_1 + a_{22}x_2 + a_{23}x_3 &= b_2 \\
a_{31}x_1 + a_{32}x_2 + a_{33}x_3 &= b_3
\end{aligned}
$$

Dalam notasi aljabar matriks, sistem di atas dapat direpresentasikan secara ringkas dalam bentuk:

$$A \mathbf{x} = \mathbf{b}$$

di mana:
- $A \in \mathbb{R}^{3 \times 3}$ adalah matriks koefisien:
  $$A = \begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix}$$
- $\mathbf{x} \in \mathbb{R}^{3 \times 1}$ adalah vektor variabel solusi yang dicari:
  $$\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}$$
- $\mathbf{b} \in \mathbb{R}^{3 \times 1}$ adalah vektor konstanta ruas kanan:
  $$\mathbf{b} = \begin{bmatrix} b_1 \\ b_2 \\ b_3 \end{bmatrix}$$

---

## 2. Prinsip Kerja Metode Eliminasi Gauss

Metode Eliminasi Gauss bekerja dengan mentransformasikan matriks teraugmentasi $[A \mid \mathbf{b}]$ menjadi matriks segitiga atas (upper triangular matrix) melalui serangkaian **Operasi Baris Elementer (OBE)**. Setelah bentuk segitiga atas tercapai, nilai masing-masing variabel dihitung secara berurutan mulai dari variabel terakhir menggunakan **Substitusi Mundur (Back Substitution)**.

### 2.1 Mengapa Menggunakan Pivoting Parsial (*Partial Pivoting*)?
Dalam komputasi floating-point, pembagian dengan angka pivot yang nilainya nol ($a_{kk} = 0$) akan menyebabkan galat *ZeroDivisionError*. Lebih jauh lagi, pembagian dengan nilai pivot yang sangat kecil mendekati nol ($|a_{kk}| \ll 1$) akan memicu perambatan galat pembulatan (*round-off error propagation*) yang dapat merusak akurasi solusi numerik.

Oleh karena itu, algoritma ini mengimplementasikan **Pivoting Parsial**:
> Pada setiap tahap eliminasi kolom ke-$k$, cari baris $p$ (di mana $p \ge k$) yang memiliki nilai absolut elemen kolom terbesar $|a_{pk}| = \max_{i=k,\dots,n} |a_{ik}|$, kemudian tukar baris ke-$k$ dengan baris ke-$p$.

---

## 3. Langkah-Langkah Algoritma Terperinci

### Tahap 1: Pembentukan Matriks Teraugmentasi
Gabungkan matriks koefisien $A$ dan vektor konstanta $\mathbf{b}$ berukuran $3 \times 4$:
$$
\tilde{A} = [A \mid \mathbf{b}] = \begin{bmatrix} 
a_{11} & a_{12} & a_{13} & \bigm| & b_1 \\
a_{21} & a_{22} & a_{23} & \bigm| & b_2 \\
a_{31} & a_{32} & a_{33} & \bigm| & b_3 
\end{bmatrix}
$$

### Tahap 2: Eliminasi Maju (*Forward Elimination*) dengan Pivoting
Untuk setiap kolom pivot $k = 1$ sampai $2$:
1. **Pivoting**:
   - Tentukan indeks baris $p \in \{k, \dots, 3\}$ sedemikian hingga $|a_{pk}| = \max_{i=k,\dots,3} |a_{ik}|$.
   - Jika $|a_{pk}| < \epsilon$ (nilai batas mendekati nol, misal $10^{-12}$), maka matriks singular dan sistem tidak memiliki solusi unik (berhenti dengan pesan kesalahan).
   - Jika $p \neq k$, tukar baris ke-$k$ dengan baris ke-$p$.
2. **Eliminasi Baris di Bawah Pivot**:
   - Untuk setiap baris $i$ dari $k+1$ sampai $3$:
     - Hitung faktor pengali:
       $$m_{ik} = \frac{a_{ik}}{a_{kk}}$$
     - Lakukan operasi baris elementer:
       $$R_i \leftarrow R_i - m_{ik} \times R_k$$
       Secara komponen:
       $$a_{ij} \leftarrow a_{ij} - m_{ik} \cdot a_{kj}, \quad \text{untuk } j = k, \dots, 3$$
       $$b_i \leftarrow b_i - m_{ik} \cdot b_k$$

Setelah Tahap 2 selesai, matriks teraugmentasi berubah menjadi:
$$
\begin{bmatrix} 
a'_{11} & a'_{12} & a'_{13} & \bigm| & b'_1 \\
0 & a'_{22} & a'_{23} & \bigm| & b'_2 \\
0 & 0 & a'_{33} & \bigm| & b'_3 
\end{bmatrix}
$$

### Tahap 3: Substitusi Mundur (*Back Substitution*)
Setelah matriks segitiga atas terbentuk:
1. Hitung variabel terakhir ($x_3$):
   $$x_3 = \frac{b'_3}{a'_{33}}$$
2. Hitung variabel kedua ($x_2$):
   $$x_2 = \frac{b'_2 - a'_{23}x_3}{a'_{22}}$$
3. Hitung variabel pertama ($x_1$):
   $$x_1 = \frac{b'_1 - a'_{12}x_2 - a'_{13}x_3}{a'_{11}}$$

Rumus umum substitusi mundur untuk $i = n, n-1, \dots, 1$:
$$x_i = \frac{b'_i - \sum_{j=i+1}^n a'_{ij} x_j}{a'_{ii}}$$

---

## 4. Pseudocode Formal Algoritma

```text
ALGORITHM GaussianElimination_3V
INPUT: 
    A : matriks koefisien berukuran 3x3
    b : vektor konstanta berukuran 3x1
OUTPUT:
    x : vektor solusi berukuran 3x1 atau pesan kesalahan

BEGIN
    n ← 3
    // 1. Bentuk augmented matrix M = [A | b] berukuran 3 x 4
    FOR i FROM 1 TO n DO
        FOR j FROM 1 TO n DO
            M[i][j] ← A[i][j]
        END FOR
        M[i][n+1] ← b[i]
    END FOR

    // 2. Forward Elimination dengan Partial Pivoting
    FOR k FROM 1 TO n-1 DO
        // Cari baris pivot terbesar
        max_row ← k
        max_val ← ABS(M[k][k])
        FOR i FROM k+1 TO n DO
            IF ABS(M[i][k]) > max_val THEN
                max_val ← ABS(M[i][k])
                max_row ← i
            END IF
        END FOR

        // Validasi singularitas
        IF max_val < 10^(-12) THEN
            ERROR "Sistem Persamaan Linear Singular atau Tidak Memiliki Solusi Unik"
            EXIT
        END IF

        // Swap baris k dengan max_row
        IF max_row != k THEN
            SWAP M[k] WITH M[max_row]
        END IF

        // Eliminasi baris di bawah pivot
        FOR i FROM k+1 TO n DO
            factor ← M[i][k] / M[k][k]
            FOR j FROM k TO n+1 DO
                M[i][j] ← M[i][j] - factor * M[k][j]
            END FOR
        END FOR
    END FOR

    // Cek elemen diagonal terakhir
    IF ABS(M[n][n]) < 10^(-12) THEN
        ERROR "Matriks singular pada elemen pivot terakhir"
        EXIT
    END IF

    // 3. Back Substitution
    x[n] ← M[n][n+1] / M[n][n]
    FOR i FROM n-1 DOWNTO 1 DO
        sum_ax ← 0
        FOR j FROM i+1 TO n DO
            sum_ax ← sum_ax + M[i][j] * x[j]
        END FOR
        x[i] ← (M[i][n+1] - sum_ax) / M[i][i]
    END FOR

    RETURN x
END
```

---

## 5. Contoh Uji Kasus dan Perhitungan Manual

Diberikan Sistem Persamaan Linear 3 Variabel:
$$
\begin{aligned}
4x_1 + x_2 - 2x_3 &= 9 \\
2x_1 + 5x_2 + x_3 &= 19 \\
x_1 - 2x_2 + 6x_3 &= 5
\end{aligned}
$$

### Bentuk Matriks Teraugmentasi Awal:
$$
\left[
\begin{array}{ccc|c}
4 & 1 & -2 & 9 \\
2 & 5 & 1 & 19 \\
1 & -2 & 6 & 5
\end{array}
\right]
$$

### Iterasi Eliminasi 1 ($k = 1$):
- Pivot awal pada baris 1 adalah $4$. Karena $|4| > |2|$ dan $|4| > |1|$, tidak diperlukan penukaran baris.
- Eliminasi Baris 2 ($R_2 \leftarrow R_2 - \frac{2}{4} R_1$):
  $$R_2 = [2, 5, 1 \mid 19] - 0.5 \times [4, 1, -2 \mid 9] = [0, 4.5, 2 \mid 14.5]$$
- Eliminasi Baris 3 ($R_3 \leftarrow R_3 - \frac{1}{4} R_1$):
  $$R_3 = [1, -2, 6 \mid 5] - 0.25 \times [4, 1, -2 \mid 9] = [0, -2.25, 6.5 \mid 2.75]$$

Matriks setelah eliminasi kolom 1:
$$
\left[
\begin{array}{ccc|c}
4 & 1 & -2 & 9 \\
0 & 4.5 & 2 & 14.5 \\
0 & -2.25 & 6.5 & 2.75
\end{array}
\right]
$$

### Iterasi Eliminasi 2 ($k = 2$):
- Pivot pada baris 2 kolom 2 adalah $4.5$. Nilai $|4.5| > |-2.25|$, tidak perlu penukaran baris.
- Pengali: $m_{32} = \frac{-2.25}{4.5} = -0.5$.
- Operasi $R_3 \leftarrow R_3 - (-0.5) R_2 = R_3 + 0.5 R_2$:
  $$R_3 = [0, -2.25, 6.5 \mid 2.75] + 0.5 \times [0, 4.5, 2 \mid 14.5] = [0, 0, 7.5 \mid 10.0]$$

Matriks segitiga atas akhir:
$$
\left[
\begin{array}{ccc|c}
4 & 1 & -2 & 9 \\
0 & 4.5 & 2 & 14.5 \\
0 & 0 & 7.5 & 10.0
\end{array}
\right]
$$

### Substitusi Mundur (*Back Substitution*):
1. **Mencari $x_3$**:
   $$7.5 x_3 = 10.0 \implies x_3 = \frac{10.0}{7.5} = \frac{4}{3} \approx 1.333333$$
2. **Mencari $x_2$**:
   $$4.5 x_2 + 2\left(\frac{4}{3}\right) = 14.5 \implies 4.5 x_2 + 2.666667 = 14.5$$
   $$4.5 x_2 = 11.833333 \implies x_2 = \frac{11.833333}{4.5} = \frac{71}{27} \approx 2.629630$$
3. **Mencari $x_1$**:
   $$4x_1 + 1\left(\frac{71}{27}\right) - 2\left(\frac{4}{3}\right) = 9$$
   $$4x_1 + 2.629630 - 2.666667 = 9 \implies 4x_1 - 0.037037 = 9 \implies 4x_1 = 9.037037 \implies x_1 \approx 2.259259$$

---

## 6. Kompleksitas Komputasi & Stabilitas Numerik
- **Kompleksitas Waktu (Time Complexity)**:
  - Eliminasi Maju: $\sum_{k=1}^{n-1} (n-k)(n-k+1) \approx \frac{n^3}{3}$ operasi perkalian/pembagian.
  - Substitusi Mundur: $\sum_{i=1}^n (n-i) \approx \frac{n^2}{2}$ operasi.
  - Total kompleksitas asimtotik: $\mathcal{O}(n^3)$. Untuk sistem 3 variabel ($n = 3$), komputasi berlangsung instan.
- **Kompleksitas Ruang (Space Complexity)**: $\mathcal{O}(n^2)$ untuk menyimpan matriks augmented.
- **Stabilitas Numerik**: Pivoting parsial membatasi elemen faktor pengali $|m_{ik}| \le 1$, sehingga mencegah peledakan galat akibat pembulatan *floating-point arithmetic*.

