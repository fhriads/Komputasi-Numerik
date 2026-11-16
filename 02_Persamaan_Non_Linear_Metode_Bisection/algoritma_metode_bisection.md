# ALGORITMA PENYELESAIAN PERSAMAAN NON-LINEAR
## METODE BAGI DUA (BISECTION METHOD)

- **Mata Kuliah** : Komputasi Numerik
- **Topik**       : Pencarian Akar Persamaan Non-Linear $f(x) = 0$
- **Metode**      : Bisection Method (Metode Bagi Dua / Bolzano Interval Bisection)
- **Penyusun**    : Fahri Adis Al Hafni (NIM: 202511420105)
- **Program Studi**: Teknik Informatika - Fakultas Teknik
- **Institusi**   : Universitas Dr. Soetomo (Unitomo) Surabaya

---

## 1. Landasan Teori dan Teorema Bolzano

Pencarian akar persamaan non-linear bertujuan menemukan nilai $x = r$ sedemikian sehingga memenuhi:

$$f(r) = 0$$

Metode Bisection (Bagi Dua) merupakan salah satu metode numerik jenis **metode tertutup (bracketing method)**. Metode ini selalu menjamin konvergensi (*guaranteed convergence*) menuju akar asalkan fungsi kontinu dan kondisi batas awal dipenuhi.

### 1.1 Teorema Nilai Antara (*Intermediate Value Theorem / Teorema Bolzano*)
> Andaikan fungsi $f(x)$ kontinu pada interval tertutup $[a, b]$, dan nilai fungsi pada kedua titik ujung memiliki tanda yang berlawanan, yaitu:
> $$f(a) \cdot f(b) < 0$$
> Maka secara matematis pasti terdapat sekurang-kurangnya satu nilai riil $c \in (a, b)$ sedemikian rupa sehingga $f(c) = 0$.

---

## 2. Prinsip Kerja dan Mekanisme Reduksi Interval

Prinsip kerja metode ini adalah membagi interval pencarian $[a, b]$ menjadi dua sub-interval yang sama panjang secara berulang-ulang (*repetitive bisection*).
1. Pada setiap iterasi, titik tengah interval dihitung:
   $$c = \frac{a + b}{2}$$
2. Tanda dari $f(c)$ dievaluasi:
   - Jika $f(a) \cdot f(c) < 0$, maka akar terletak pada sub-interval kiri $[a, c]$. Oleh karenanya, batas kanan diperbaharui: $b \leftarrow c$.
   - Jika $f(a) \cdot f(c) > 0$, maka akar terletak pada sub-interval kanan $[c, b]$. Oleh karenanya, batas kiri diperbaharui: $a \leftarrow c$.
   - Jika $f(c) = 0$ atau $|f(c)| < \text{Toleransi}$, maka $c$ adalah akar yang dicari.
3. Panjang interval pada iterasi ke-$n$ berkurang secara eksponensial menjadi:
   $$\Delta x_n = \frac{b - a}{2^n}$$

### 2.2 Estimasi Jumlah Iterasi Minimum
Untuk mencapai toleransi galat absolut $\epsilon$ dari interval awal berlebar $[a, b]$, jumlah iterasi $n$ yang diperlukan dapat dihitung secara analitik:
$$\frac{b - a}{2^n} \le \epsilon \implies 2^n \ge \frac{b - a}{\epsilon} \implies n \ge \frac{\ln(b - a) - \ln(\epsilon)}{\ln(2)}$$

---

## 3. Langkah-Langkah Algoritma Terperinci

1. **Input / Inisialisasi**:
   - Definisikan fungsi non-linear kontinu $f(x)$.
   - Tentukan batas bawah interval $a$ dan batas atas interval $b$.
   - Tentukan toleransi galat $\epsilon$ (misal $10^{-6}$) dan batas maksimum iterasi $N_{\max}$ (misal 100).
2. **Pemeriksaan Syarat Awal (Teorema Bolzano)**:
   - Hitung $f(a)$ dan $f(b)$.
   - Jika $f(a) \cdot f(b) \ge 0$, maka metode Bisection **gagal/tidak dapat diaplikasikan** pada interval tersebut karena tidak menjamin adanya akar tunggal. Program harus berhenti dan meminta input interval baru.
3. **Proses Iterasi Bisection**:
   - Inisialisasi nomor iterasi $k = 1$.
   - Selama $k \le N_{\max}$:
     1. Hitung titik tengah: $c_k = \frac{a + b}{2}$.
     2. Evaluasi nilai fungsi di titik tengah: $f(c_k)$.
     3. Hitung estimasi galat aproksimasi:
        $$\text{Galat Relatif Hampiran} = \left| \frac{b - a}{2} \right| \quad \text{atau} \quad \left| \frac{c_k - c_{k-1}}{c_k} \right| \times 100\%$$
     4. **Kriteria Penghentian (Stopping Criteria)**:
        Jika $|f(c_k)| < \epsilon$ atau $\left| \frac{b - a}{2} \right| < \epsilon$:
        - Tetapkan $c_k$ sebagai hampiran akar solusi.
        - Tampilkan tabel iterasi dan keluar dari perulangan.
     5. **Pembaharuan Interval**:
        - Jika $f(a) \cdot f(c_k) < 0$: perbaharui $b = c_k$.
        - Sebaliknya: perbaharui $a = c_k$.
     6. Naikkan counter iterasi: $k \leftarrow k + 1$.
4. **Output Solusi**:
   - Cetak nilai akar hampiran $c_k$, nilai fungsi $f(c_k)$, jumlah iterasi konvergensi, dan tabel riwayat iterasi lengkap.

---

## 4. Pseudocode Formal Algoritma Bisection

```text
ALGORITHM BisectionMethod
INPUT:
    f       : fungsi matematika non-linear kontinu
    a, b    : batas awal interval pencarian real
    tol     : batas toleransi galat (epsilon)
    max_iter: jumlah iterasi maksimum

OUTPUT:
    akar    : hampiran akar f(x) = 0 atau pesan kesalahan

BEGIN
    // Evaluasi syarat Bolzano
    fa ← f(a)
    fb ← f(b)

    IF fa * fb >= 0 THEN
        ERROR "Nilai f(a) dan f(b) harus berlawanan tanda: f(a)*f(b) < 0"
        EXIT
    END IF

    PRINT "Iterasi |      a      |      b      |      c      |    f(c)     |    Galat    "
    c_lama ← a

    FOR iterasi FROM 1 TO max_iter DO
        // Hitung titik tengah
        c ← (a + b) / 2.0
        fc ← f(c)
        galat ← ABS(b - a) / 2.0

        PRINT iterasi, a, b, c, fc, galat

        // Evaluasi kriteria henti
        IF (ABS(fc) < tol) OR (galat < tol) THEN
            PRINT "Konvergensi tercapai pada iterasi ke-", iterasi
            RETURN c
        END IF

        // Pembaharuan interval
        IF fa * fc < 0 THEN
            b ← c
            fb ← fc
        ELSE
            a ← c
            fa ← fc
        END IF
    END FOR

    WARNING "Maksimum iterasi tercapai tanpa konvergensi sempurna."
    RETURN c
END
```

---

## 5. Contoh Uji Kasus dan Perhitungan Manual

Diberikan persamaan kubik non-linear:
$$f(x) = x^3 - 2x - 5 = 0$$

Target: Mencari akar pada interval $[2, 3]$ dengan toleransi galat $\epsilon = 0.01$.

### Evaluasi Titik Ujung:
- $f(a) = f(2) = 2^3 - 2(2) - 5 = 8 - 4 - 5 = -1$ (Negatif)
- $f(b) = f(3) = 3^3 - 2(3) - 5 = 27 - 6 - 5 = +16$ (Positif)
- Nilai perkalian: $f(2) \cdot f(3) = -1 \times 16 = -16 < 0$ $\implies$ **Syarat Bolzano Terpenuhi**.

### Runtutan Iterasi Manual:
1. **Iterasi 1**:
   - $c_1 = \frac{2 + 3}{2} = 2.5$
   - $f(c_1) = f(2.5) = (2.5)^3 - 2(2.5) - 5 = 15.625 - 5 - 5 = +5.625 > 0$
   - Galat: $\frac{3 - 2}{2} = 0.5 > 0.01$
   - Karena $f(2) \cdot f(2.5) = (-1)(+5.625) < 0$, perbaharui $b = 2.5$. Interval baru: $[2.0, 2.5]$.

2. **Iterasi 2**:
   - $c_2 = \frac{2.0 + 2.5}{2} = 2.25$
   - $f(c_2) = f(2.25) = (2.25)^3 - 2(2.25) - 5 = 11.390625 - 4.5 - 5 = +1.890625 > 0$
   - Galat: $\frac{2.5 - 2.0}{2} = 0.25 > 0.01$
   - Karena $f(2) \cdot f(2.25) < 0$, perbaharui $b = 2.25$. Interval baru: $[2.0, 2.25]$.

3. **Iterasi 3**:
   - $c_3 = \frac{2.0 + 2.25}{2} = 2.125$
   - $f(c_3) = f(2.125) = (2.125)^3 - 2(2.125) - 5 = 9.595703 - 4.25 - 5 = +0.345703 > 0$
   - Galat: $\frac{2.25 - 2.0}{2} = 0.125 > 0.01$
   - Karena $f(2) \cdot f(2.125) < 0$, perbaharui $b = 2.125$. Interval baru: $[2.0, 2.125]$.

4. **Iterasi 4**:
   - $c_4 = \frac{2.0 + 2.125}{2} = 2.0625$
   - $f(c_4) = f(2.0625) = (2.0625)^3 - 2(2.0625) - 5 = 8.774658 - 4.125 - 5 = -0.350342 < 0$
   - Galat: $\frac{2.125 - 2.0}{2} = 0.0625 > 0.01$
   - Karena $f(a) \cdot f(c_4) = (-1)(-0.350342) > 0$, maka perbaharui $a = 2.0625$. Interval baru: $[2.0625, 2.125]$.

Proses berlanjut hingga diperoleh hampiran akar berpresisi tinggi: $x \approx 2.094551$.

---

## 6. Analisis Kelebihan dan Keterbatasan Metode Bisection

### Kelebihan:
1. **Pasti Konvergen**: Selama fungsi kontinu dan nilai fungsi di titik batas berlawanan tanda, metode ini dijamin 100% menemukan akar (*globally convergent*).
2. **Sederhana dan Robust**: Tidak memerlukan perhitungan turunan pertama ($f'(x)$) seperti pada metode Newton-Raphson.
3. **Galat Terprediksi**: Jumlah iterasi untuk mencapai toleransi tertentu dapat ditentukan di muka secara pasti.

### Keterbatasan:
1. **Laju Konvergensi Lambat**: Bisection memiliki laju konvergensi linear ($r = 1$), di mana panjang interval hanya terbagi dua pada tiap langkah.
2. **Tidak Dapat Menemukan Akar Ganda**: Jika grafik kurva hanya menyinggung sumbu-$x$ tanpa memotong (misal $f(x) = (x-2)^2 = 0$), maka $f(a) \cdot f(b) > 0$ sehingga Bisection tidak dapat digunakan.

