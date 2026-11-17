# Repositori Tugas 1: Komputasi Numerik

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue.svg" alt="Python Version" />
  <img src="https://img.shields.io/badge/Google-Colab-orange.svg" alt="Google Colab" />
  <img src="https://img.shields.io/badge/License-Academic%20Unitomo-green.svg" alt="License" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen.svg" alt="Status" />
</p>

Repositori ini memuat seluruh pemenuhan **Tugas 1 Mata Kuliah Komputasi Numerik**, Program Studi Teknik Informatika, Fakultas Teknik, **Universitas Dr. Soetomo (Unitomo) Surabaya**. 

Repositori ini dirancang mencakup landasan teori, analisis algoritma, implementasi kode *cell-by-cell* di Google Colaboratory, anotasi baris demi baris, dokumentasi prompt AI, naskah dan file video presentasi berdurasi maksimal 5 menit, serta integrasi portofolio profesional di LinkedIn.

---

## 📌 Identitas Mahasiswa
- **Nama Mahasiswa** : Fahri Adis Al Hafni
- **NIM**            : 202511420105
- **Program Studi**  : Teknik Informatika
- **Fakultas**       : Teknik
- **Perguruan Tinggi**: Universitas Dr. Soetomo (Unitomo) Surabaya
- **Mata Kuliah**    : Komputasi Numerik
- **Email Google**   : `fahriadisalhafni15@gmail.com`
- **Profil GitHub**  : [github.com/fhriads](https://github.com/fhriads)
- **Profil LinkedIn**: [linkedin.com/in/fahri-adis-al-hafni-29771a413](https://www.linkedin.com/in/fahri-adis-al-hafni-29771a413/)
- **Tautan Repositori**: [github.com/fhriads/Komputasi-Numerik](https://github.com/fhriads/Komputasi-Numerik)

---

## 📂 Struktur Repositori

```text
Komputasi-Numerik/
├── README.md                                          # Dokumentasi utama repositori
├── link_akun.txt                                      # Tautan akun GitHub, Google Colab, & LinkedIn (No. 4)
├── prompt_ai.txt                                      # Dokumentasi seluruh prompt AI yang digunakan (No. 9 & 12)
├── .gitignore                                         # Berkas pengecualian Git
│
├── 01_Sistem_Persamaan_Linear_3_Variabel/             # TUGAS SPL 3 VARIABEL (No. 5 - 7 & 10)
│   ├── SPL3V_Eliminasi_Gauss.ipynb                    # Notebook Google Colab resmi terhubung
│   └── algoritma_spl3v_eliminasi_gauss.md             # Dokumen teori, pseudocode, & hitungan manual SPL
│
├── 02_Persamaan_Non_Linear_Metode_Bisection/          # TUGAS PERSAMAAN NON-LINEAR BISECTION (No. 12)
│   ├── NonLinear_Metode_Bisection.ipynb               # Notebook Google Colab resmi terhubung
│   └── algoritma_metode_bisection.md                  # Dokumen teori Bolzano, analisis konvergensi, & pseudocode
│
├── 03_Video_Penjelasan/                               # VIDEO PRESENTASI (No. 10, 11, & 12)
│   └── link_video.txt                                 # Tautan video presentasi di Google Drive
```

---

## 🔬 Rincian Modul Pembahasan & Tautan Google Colab

### 1. Sistem Persamaan Linear 3 Variabel (SPL 3V)
- **Metode**: Eliminasi Gauss dengan *Partial Pivoting* dan *Back Substitution*.
- **Masalah**: Menyelesaikan sistem persamaan aljabar linear $A\mathbf{x} = \mathbf{b}$ berukuran $3 \times 3$.
- **Keunggulan**: Menggunakan *partial pivoting* untuk mencegah *division by zero* dan meminimalisasi perambatan galat pembulatan numerik (*round-off error*).
- **Verifikasi**: Divalidasi dengan penghitungan norma residu Euclidean $\|A\mathbf{x} - \mathbf{b}\|_2 \approx 0.00$ dan komparasi terhadap `numpy.linalg.solve`.
- **Akses Google Colab**: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1tNYyRAPvO1fHMB3GtR6rH5XOB-2ZWIvv?usp=sharing)
- **Berkas Notebook**: [`01_Sistem_Persamaan_Linear_3_Variabel/SPL3V_Eliminasi_Gauss.ipynb`](01_Sistem_Persamaan_Linear_3_Variabel/SPL3V_Eliminasi_Gauss.ipynb)

### 2. Persamaan Non-Linear Metode Bisection (Bagi Dua)
- **Metode**: Metode Tertutup (*Bracketing Method*) berbasis Teorema Nilai Antara Bolzano (*Intermediate Value Theorem*).
- **Kasus Uji**: Pencarian akar fungsi kontinu $f(x) = x^3 - 2x - 5 = 0$ pada interval $[2.0, 3.0]$.
- **Keunggulan**: Menjamin 100% konvergensi (*guaranteed global convergence*) dengan laju reduksi interval $\Delta x_n = \frac{b - a}{2^n}$.
- **Verifikasi**: Divalidasi terhadap tolok ukur resmi `scipy.optimize.bisect` dengan selisih deviasi $0.00$ pada toleransi $\epsilon = 10^{-6}$.
- **Akses Google Colab**: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1aIgakq1pwaLbOM9UY2R95FJgqSu4Z57Q?usp=sharing)
- **Berkas Notebook**: [`02_Persamaan_Non_Linear_Metode_Bisection/NonLinear_Metode_Bisection.ipynb`](02_Persamaan_Non_Linear_Metode_Bisection/NonLinear_Metode_Bisection.ipynb)

---

## 🎬 Video Presentasi Penjelasan (No. 10, 11, & 12)
- **Format**: Video rekaman beresolusi HD diunggah ke Google Drive agar dapat ditonton secara langsung (*streaming*) tanpa kendala ukuran file.
- **Struktur Video**: Menampilkan wajah dan suara presenter berbicara langsung di awal, dilanjutkan dengan rekaman layar penjalanan kode Google Colaboratory secara *cell-by-cell* disertai narasi penjelasan.
- **Tautan Video Streaming (Google Drive)**:
  - 🎥 **Video SPL 3 Variabel**: [Tonton Video SPL 3V di Google Drive](https://drive.google.com/file/d/1aypEoopemIXBigWtMUE4SG1xVCEvpWnT/view?usp=sharing)
  - 🎥 **Video Persamaan Non-Linear Bisection**: [Tonton Video Bisection di Google Drive](https://drive.google.com/file/d/1ML6Py-EUzC75qcPcRAUAZQ9X62L_CHTa/view?usp=sharing)
  - Berkas tautan lokal: [`03_Video_Penjelasan/link_video.txt`](03_Video_Penjelasan/link_video.txt)

---

## 🤖 Dokumentasi Prompt AI (No. 8 - 9 & 12)
Sesuai instruksi untuk menjaga orisinalitas dan menghindari plagiarisme (>80% kemiripan), seluruh riwayat perintah prompt AI disusun secara terstruktur dari perancangan teori, penulisan kode, anotasi baris demi baris, hingga pembuatan skenario video.
Seluruh prompt tercatat lengkap pada file [`prompt_ai.txt`](prompt_ai.txt).

---

## 💼 Portofolio LinkedIn (No. 13)
Hasil proyek komputasi numerik ini telah dipublikasikan pada akun LinkedIn sebagai portofolio keahlian komputasi sains dan *software engineering*.
- **Tautan Postingan Portofolio**: [Lihat Postingan di LinkedIn](https://lnkd.in/p/gcyfW3uw)
- **Profil Resmi LinkedIn**: [linkedin.com/in/fahri-adis-al-hafni-29771a413](https://www.linkedin.com/in/fahri-adis-al-hafni-29771a413/)

---

## 💻 Cara Menjalankan Kode di Google Colab:
1. Buka tautan Google Colab pada masing-masing modul di atas.
2. Jalankan masing-masing cell secara berurutan menggunakan pintasan keyboard `Shift + Enter`.

