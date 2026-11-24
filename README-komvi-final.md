# Final Project — Computer Vision

**Bahasa pemrograman:** Python  
**Library utama:** OpenCV, NumPy, Matplotlib  
**Anggota kelompok:** 2–3 mahasiswa

> **Tujuan:** Merancang, mengimplementasikan, dan mengevaluasi solusi *computer vision* untuk menyelesaikan permasalahan nyata.

## 1. Pilih satu dari empat proyek

| Kode | Proyek | Target utama | Metode inti | Evaluasi utama |
|---|---|---|---|---|
| **P01** | Automatic Document Scanner | Memindai foto dokumen dengan koreksi perspektif | Filtering, Canny, contours, perspective transform | Corner error, success rate, runtime |
| **P02** | Motion Detection & Object Tracking | Mendeteksi dan melacak pergerakan objek | Frame differencing, MOG2, contours, optical flow/tracking | Precision/recall, position error, FPS |
| **P03** | Stereo Vision & Depth Estimation | Memperkirakan disparity/kedalaman dari pasangan stereo | Rectification, StereoBM, StereoSGBM | Disparity/depth MAE jika ada ground truth, valid-pixel rate |
| **P04** | Visual Inspection & Object Measurement | Mengukur dimensi dan/atau memeriksa cacat visual | Thresholding/segmentation, morphology, contours, calibration | Measurement MAE, precision/recall/F1 jika klasifikasi |

### P01 — Automatic Document Scanner

**Masalah:** Memperbaiki foto dokumen yang miring atau kurang jelas menjadi hasil pemindaian yang rapi.

**Tahapan:**

1. Ambil minimal **30 foto** dengan variasi latar, sudut, dan pencahayaan.
2. Lakukan preprocessing menggunakan filtering dan konversi grayscale.
3. Terapkan edge detection dan contour detection untuk mendeteksi batas dokumen.
4. Temukan empat titik sudut (*corner*) dokumen.
5. Lakukan perspective transform untuk mengoreksi perspektif dokumen.
6. Terapkan thresholding atau teknik peningkatan kualitas citra untuk meningkatkan keterbacaan dokumen.

**Eksperimen wajib:** Bandingkan Gaussian vs median filtering serta global vs adaptive thresholding; uji sudut miring dan pencahayaan rendah.

**Output:** Citra sebelum/sesudah, visualisasi corner, hasil scan, dan tabel deteksi serta error.

### P02 — Motion Detection & Object Tracking

**Masalah:** Menemukan objek bergerak dan melacak lintasannya dalam video.

**Tahapan:**

1. Rekam minimal **10 video** dengan variasi gerakan.
2. Ekstraksi frame dari video menggunakan OpenCV.
3. Deteksi gerakan menggunakan frame differencing atau MOG2.
4. Lakukan segmentasi objek bergerak dan tentukan bounding box.
5. Lacak posisi objek menggunakan centroid tracking atau optical flow.
6. Visualisasikan lintasan dan estimasi kecepatan dalam **pixel/detik**.

**Eksperimen wajib:** Bandingkan frame differencing vs MOG2 dan dua konfigurasi tracking; uji perubahan pencahayaan, kecepatan, dan *occlusion*.

**Output:** Video dengan bounding box dan lintasan, data posisi per frame, grafik, dan tabel metrik.

### P03 — Stereo Vision & Depth Estimation

**Masalah:** Mengestimasi jarak relatif atau kedalaman dari pasangan citra kiri–kanan.

**Tahapan:**

1. Siapkan stereo dataset atau sistem dua kamera.
2. Lakukan kalibrasi dan *rectification* bila diperlukan.
3. Konversi pasangan citra menjadi grayscale.
4. Hitung disparity menggunakan StereoBM dan StereoSGBM.
5. Lakukan filtering dan validasi disparity.
6. Hitung depth **hanya jika** baseline dan focal length terkalibrasi tersedia.

**Eksperimen wajib:** Bandingkan StereoBM vs StereoSGBM, variasikan *block size* dan parameter algoritma; analisis area tanpa tekstur serta *occlusion*.

**Output:** Pasangan citra stereo, disparity map, visualisasi kedalaman (jika valid), serta tabel error dan runtime.

> **Catatan:** Jangan mengklaim akurasi jarak dalam cm/mm tanpa kalibrasi metrik dan *ground truth* kedalaman.

### P04 — Visual Inspection & Object Measurement

**Masalah:** Mengukur dimensi komponen atau mendeteksi cacat/ketidaksesuaian produk dari citra.

**Tahapan:**

1. Pilih komponen fisik, misalnya baut atau hasil 3D printing.
2. Ambil minimal **20 foto** komponen dengan variasi kondisi pengambilan.
3. Lakukan segmentasi untuk memisahkan objek dari latar belakang.
4. Terapkan operasi morfologi untuk membersihkan hasil segmentasi.
5. Lakukan contour detection dan pengukuran fitur geometris objek.
6. Kalibrasi skala **pixel-ke-mm** menggunakan referensi ukuran yang diketahui.
7. Bandingkan estimasi dengan ukuran aktual dan/atau aturan toleransi yang ditetapkan.

**Eksperimen wajib:** Bandingkan dua metode segmentasi, variasikan pencahayaan, dan ukur error terhadap penggaris atau jangka sorong.

**Output:** Citra beranotasi, estimasi ukuran, grafik hasil vs referensi, metrik evaluasi, dan confusion matrix bila melakukan klasifikasi.

## 2. Struktur folder pengumpulan program (.zip)

```text
FinalProject_KelompokXX/
├── README.md                 # Identitas, pilihan proyek, cara menjalankan, hasil
├── requirements.txt          # Dependensi Python
├── src/
│   └── main.py               # Entry point program
├── dataset/
│   ├── raw/                  # Data mentah (atau tautan jika terlalu besar)
│   └── annotations/          # Ground truth / anotasi jika ada
├── results/
│   ├── images/
│   ├── videos/
│   └── metrics.csv           # Hasil evaluasi kuantitatif
├── report/
│   └── laporan.pdf
├── presentation/
│   └── presentasi.pdf
└── demo/
    └── demo.mp4
```

## 3. Format laporan (8–12 halaman, di luar lampiran)

1. **Pendahuluan** — latar belakang, rumusan masalah, tujuan, dan batasan.
2. **Metodologi** — dataset, diagram pipeline, algoritma dan persamaan penting, desain eksperimen, serta metrik.
3. **Implementasi** — arsitektur kode, parameter, dan tahapan pemrosesan beserta contoh hasil.
4. **Hasil dan Pembahasan** — gambar/video contoh, tabel/grafik, perbandingan metode, kegagalan, dan keterbatasan.
5. **Kesimpulan** — hasil utama dan kemungkinan pengembangan.
6. **Referensi** — sumber metode, pustaka, dan dataset yang digunakan.

## 4. Presentasi dan demonstrasi

- **Presentasi:** 8 menit.
- **Demonstrasi aplikasi:** 4 menit.
- **Rekaman video demonstrasi** dikumpulkan bersama laporan dan berkas program dalam folder `demo/`.

---

**Prinsip utama:** Tunjukkan **bagaimana** algoritma bekerja, **seberapa baik** hasilnya, dan **mengapa** terjadi keberhasilan atau kegagalan — bukan hanya menampilkan aplikasi yang berjalan.
