# Final Project — Computer Vision
**Bahasa pemrograman:** Python  
**Library utama:** OpenCV, NumPy, Matplotlib  
**Anggota kelompok:** 2–3 mahasiswa  

> **Tujuan:** Merancang, mengimplementasikan, dan mengevaluasi solusi *computer vision* untuk masalah nyata.

## 1. Pilih satu dari enam proyek

| Kode | Proyek | Target utama | Metode inti | Evaluasi utama |
|---|---|---|---|---|
| P01 | Automatic Document Scanner | Memindai foto dokumen dengan koreksi perspektif | Filtering, Canny, contours, perspective transform | Corner error, success rate, runtime |
| P02 | Motion Detection & Object Tracking | Mendeteksi dan melacak pergerakan objek | Frame differencing, MOG2, contours, optical flow/tracking | Precision/recall, position error, FPS |
| P03 | Stereo Vision & Depth Estimation | Memperkirakan disparity/kedalaman dari pasangan stereo | Rectification, StereoBM, StereoSGBM | Disparity/depth MAE jika ada ground truth, valid-pixel rate |
| P04 | Visual Inspection & Object Measurement | Mengukur dimensi dan/atau memeriksa cacat visual | Thresholding/segmentation, morphology, contours, calibration | Measurement MAE, precision/recall/F1 jika klasifikasi |



### P01 — Automatic Document Scanner

**Masalah:** Memperbaiki foto dokumen yang miring atau kurang jelas menjadi hasil pemindaian yang rapi.

**Tahapan:** (1) Ambil minimal 30 foto dengan variasi latar, sudut, dan cahaya; (2) filtering dan grayscale; (3) edge/contour detection; (4) temukan empat corner; (5) perspective transform; (6) thresholding/peningkatan keterbacaan.

**Eksperimen wajib:** Bandingkan Gaussian vs median filtering, serta global vs adaptive threshold; uji sudut miring dan cahaya rendah.

**Output:** Citra sebelum/sesudah, visualisasi corner, hasil scan, tabel deteksi dan error.

### P02 — Motion Detection & Object Tracking

**Masalah:** Menemukan objek bergerak dan melacak lintasannya dalam video.

**Tahapan:** (1) Rekam minimal 10 video dengan variasi gerakan; (2) ekstraksi frame; (3) frame differencing atau MOG2; (4) segmentasi dan bounding box; (5) tracking dengan centroid/optical flow; (6) lintasan dan estimasi kecepatan dalam pixel/detik.

**Eksperimen wajib:** Bandingkan frame differencing vs MOG2 dan dua konfigurasi tracking; uji perubahan cahaya, kecepatan, dan occlusion.

**Output:** Video dengan bounding box dan lintasan, data posisi per frame, grafik dan tabel metrik.

### P03 — Stereo Vision & Depth Estimation

**Masalah:** Mengestimasi jarak relatif atau kedalaman dari pasangan citra kiri-kanan.

**Tahapan:** (1) Siapkan stereo dataset atau sistem dua kamera; (2) kalibrasi dan rectification bila dibutuhkan; (3) grayscale; (4) hitung disparity dengan StereoBM dan StereoSGBM; (5) filtering/validasi disparity; (6) hitung depth **hanya bila** baseline dan focal length terkalibrasi tersedia.

**Eksperimen wajib:** Bandingkan StereoBM vs StereoSGBM, variasikan block size dan parameter; analisis area tanpa tekstur serta occlusion.

**Output:** Pasangan stereo, disparity map, visualisasi kedalaman (jika valid), tabel error dan runtime.

**Catatan:** Jangan mengklaim akurasi jarak dalam cm/mm tanpa kalibrasi metrik dan ground truth kedalaman.

### P04 — Visual Inspection & Object Measurement

**Masalah:** Mengukur dimensi komponen atau mendeteksi cacat/ketidaksesuaian produk dari citra.

**Tahapan:** (1) Pilih komponen fisik, misalnya baut atau hasil 3D printing; (2) ambil minimal 50 foto; (3) segmentasi; (4) operasi morfologi; (5) contour/feature measurement; (6) kalibrasi pixel-ke-mm; (7) bandingkan dengan ukuran aktual dan/atau aturan toleransi.

**Eksperimen wajib:** Bandingkan dua metode segmentasi; variasikan pencahayaan; ukur error terhadap penggaris/jangka sorong.

**Output:** Citra beranotasi, estimasi ukuran, grafik hasil vs referensi, metrik dan confusion matrix bila melakukan klasifikasi.


## 2. Struktur folder pengumpulan program (.zip)

```text
FinalProject_KelompokXX/
├── README.md                 # Isi identitas, pilihan proyek, cara menjalankan, hasil
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

1. **Pendahuluan** — latar belakang, rumusan masalah, tujuan, batasan.
2. **Metodologi** — dataset, diagram pipeline, algoritma dan persamaan penting, desain eksperimen dan metrik.
3. **Implementasi** — arsitektur kode, parameter, tahapan pemrosesan beserta contoh hasil.
4. **Hasil dan Pembahasan** — gambar/video contoh, tabel/grafik, perbandingan metode, kegagalan dan keterbatasan.
5. **Kesimpulan** — hasil utama dan pengembangan yang memungkinkan.
6. **Referensi** 

## 4. Presentasi dan demonstrasi

- Presentasi: **8 menit**.
- Demo aplikasi: **4 menit**.
- Record fioe video dikumpulkan bersama  laporan.


**Prinsip utama:** Tunjukkan **bagaimana** algoritma bekerja, **seberapa baik** hasilnya, dan **mengapa** terjadi keberhasilan atau kegagalan — bukan hanya menampilkan aplikasi yang berjalan.
