# Kompresi Citra Digital dengan Metode DCT (JPEG Baseline)

**kompresi citra *lossy* berbasis DCT** (seperti pada standar JPEG baseline) dari nol menggunakan `numpy` dan `scipy`, lalu menganalisis pengaruh parameter *quality* terhadap ukuran file dan kualitas citra.

## Isi Program

1. Konversi ruang warna RGB ke YCbCr dan *chroma subsampling* 4:2:0
2. Pembagian blok 8x8, DCT 2D, dan kuantisasi (tabel standar JPEG, dapat diatur lewat parameter *quality*)
3. Zig-zag scan, *run-length*, dan Huffman untuk menghitung ukuran bitstream sebenarnya
4. Dekompresi (de-kuantisasi, IDCT, rekonstruksi) dan evaluasi dengan **CR, bpp, MSE, PSNR, SSIM**
5. Visualisasi: blok DCT, fungsi basis, perbandingan visual, zoom, peta galat, dan grafik *trade-off*
6. Perbandingan dengan encoder JPEG Pillow dan PNG (*lossless*)

## Struktur Repository

```
kompresi-citra-dct/
├── kompresi_citra.ipynb     # notebook utama (sudah berisi output)
├── images/
│   └── sample.png           # citra contoh (ganti dengan citra sendiri)
├── output/                  # hasil rekonstruksi, file JPEG, dan tabel CSV
├── requirements.txt
├── .gitignore
└── README.md
```

```python
IMAGE_PATH = "images/nama_citra_kamu.jpg"
```

## Ringkasan Hasil

| Quality | Ukuran (KB) | CR | bpp | PSNR (dB) | SSIM |
|---:|---:|---:|---:|---:|---:|
| 5 | 4.1 | 106.6x | 0.23 | 20.45 | 0.639 |
| 10 | 7.6 | 56.7x | 0.42 | 22.55 | 0.749 |
| 25 | 15.5 | 27.9x | 0.86 | 24.76 | 0.846 |
| 50 | 24.8 | 17.4x | 1.38 | 26.62 | 0.896 |
| 75 | 37.6 | 11.5x | 2.09 | 28.71 | 0.932 |
| 90 | 60.5 | 7.1x | 3.36 | 31.64 | 0.963 |

PNG (*lossless*) pada citra yang sama: sekitar 432.0 KB (CR 1,86x). Pembahasan lengkap ada di bagian **Kesimpulan** pada notebook.

## Referensi

- Gonzalez & Woods, *Digital Image Processing*, 4th ed., Pearson, 2018.
- Wallace, G. K., "The JPEG Still Picture Compression Standard", *IEEE Trans. Consumer Electronics*, 1992.
- Ahmed, Natarajan & Rao, "Discrete Cosine Transform", *IEEE Trans. Computers*, 1974.
