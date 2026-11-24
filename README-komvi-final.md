# Final Project — Computer Vision

**Program Studi Mekatronika dan Kecerdasan Buatan (MKB)**  
**Semester:** 5  
**Tema:** *From Computer Vision Theory to Real-World Applications*  
**Bahasa pemrograman:** Python  
**Library utama:** OpenCV, NumPy, Matplotlib  
**Anggota kelompok:** 2–3 mahasiswa  
**Pelaksanaan:** Pertemuan 13–16

> **Tujuan:** Merancang, mengimplementasikan, dan mengevaluasi solusi *computer vision* untuk masalah nyata. Penilaian tidak hanya berdasarkan aplikasi yang berjalan, tetapi juga pemahaman algoritma, ketepatan eksperimen, dan analisis hasil.

## 1. Capaian pembelajaran

Setelah menyelesaikan proyek, mahasiswa mampu:

1. Merumuskan masalah yang relevan untuk *computer vision*.
2. Mendesain pipeline pemrosesan citra/video dengan sedikitnya tiga tahapan utama.
3. Mengimplementasikan algoritma menggunakan Python dan OpenCV.
4. Membandingkan sedikitnya dua metode atau konfigurasi.
5. Mengevaluasi performa dengan metrik kuantitatif yang sesuai.
6. Menjelaskan keberhasilan, keterbatasan, dan kondisi kegagalan sistem.

## 2. Pilih satu dari enam proyek

| Kode | Proyek | Target utama | Metode inti | Evaluasi utama |
|---|---|---|---|---|
| P01 | Automatic Image Stitching | Menggabungkan citra menjadi panorama | ORB/SIFT, matching, RANSAC, homography, warping | Inlier ratio, reprojection error, runtime |
| P02 | Automatic Document Scanner | Memindai foto dokumen dengan koreksi perspektif | Filtering, Canny, contours, perspective transform | Corner error, success rate, runtime |
| P03 | Motion Detection & Object Tracking | Mendeteksi dan melacak pergerakan objek | Frame differencing, MOG2, contours, optical flow/tracking | Precision/recall, position error, FPS |
| P04 | Stereo Vision & Depth Estimation | Memperkirakan disparity/kedalaman dari pasangan stereo | Rectification, StereoBM, StereoSGBM | Disparity/depth MAE jika ada ground truth, valid-pixel rate |
| P05 | Visual Inspection & Object Measurement | Mengukur dimensi dan/atau memeriksa cacat visual | Thresholding/segmentation, morphology, contours, calibration | Measurement MAE, precision/recall/F1 jika klasifikasi |
| P06 | Marker-Based Augmented Reality | Menempelkan overlay virtual pada marker planar | Feature matching, RANSAC, homography, warping | Detection rate, corner error, FPS, jitter |

### P01 — Automatic Image Stitching

**Masalah:** Menggabungkan beberapa foto dengan area yang bertumpang tindih menjadi panorama.

**Tahapan:** (1) Kumpulkan 10–15 pasangan foto dengan overlap sekitar 30–60%; (2) preprocessing; (3) deteksi keypoints dan descriptor dengan ORB atau SIFT; (4) pencocokan fitur dengan BFMatcher/FLANN sesuai descriptor; (5) penyaringan pasangan dan estimasi homography menggunakan RANSAC; (6) warping dan blending.

**Eksperimen wajib:** Bandingkan ORB vs SIFT atau dua konfigurasi matching; variasikan overlap/sudut pandang; analisis kondisi dengan terlalu sedikit inlier.

**Output:** Visualisasi keypoints dan matches, matriks homography, panorama, tabel metrik.

### P02 — Automatic Document Scanner

**Masalah:** Memperbaiki foto dokumen yang miring atau kurang jelas menjadi hasil pemindaian yang rapi.

**Tahapan:** (1) Ambil minimal 30 foto dengan variasi latar, sudut, dan cahaya; (2) filtering dan grayscale; (3) edge/contour detection; (4) temukan empat corner; (5) perspective transform; (6) thresholding/peningkatan keterbacaan.

**Eksperimen wajib:** Bandingkan Gaussian vs median filtering, serta global vs adaptive threshold; uji sudut miring dan cahaya rendah.

**Output:** Citra sebelum/sesudah, visualisasi corner, hasil scan, tabel deteksi dan error.

### P03 — Motion Detection & Object Tracking

**Masalah:** Menemukan objek bergerak dan melacak lintasannya dalam video.

**Tahapan:** (1) Rekam minimal 10 video dengan variasi gerakan; (2) ekstraksi frame; (3) frame differencing atau MOG2; (4) segmentasi dan bounding box; (5) tracking dengan centroid/optical flow; (6) lintasan dan estimasi kecepatan dalam pixel/detik.

**Eksperimen wajib:** Bandingkan frame differencing vs MOG2 dan dua konfigurasi tracking; uji perubahan cahaya, kecepatan, dan occlusion.

**Output:** Video dengan bounding box dan lintasan, data posisi per frame, grafik dan tabel metrik.

### P04 — Stereo Vision & Depth Estimation

**Masalah:** Mengestimasi jarak relatif atau kedalaman dari pasangan citra kiri-kanan.

**Tahapan:** (1) Siapkan stereo dataset atau sistem dua kamera; (2) kalibrasi dan rectification bila dibutuhkan; (3) grayscale; (4) hitung disparity dengan StereoBM dan StereoSGBM; (5) filtering/validasi disparity; (6) hitung depth **hanya bila** baseline dan focal length terkalibrasi tersedia.

**Eksperimen wajib:** Bandingkan StereoBM vs StereoSGBM, variasikan block size dan parameter; analisis area tanpa tekstur serta occlusion.

**Output:** Pasangan stereo, disparity map, visualisasi kedalaman (jika valid), tabel error dan runtime.

**Catatan:** Jangan mengklaim akurasi jarak dalam cm/mm tanpa kalibrasi metrik dan ground truth kedalaman.

### P05 — Visual Inspection & Object Measurement

**Masalah:** Mengukur dimensi komponen atau mendeteksi cacat/ketidaksesuaian produk dari citra.

**Tahapan:** (1) Pilih komponen fisik, misalnya baut atau hasil 3D printing; (2) ambil minimal 50 foto; (3) segmentasi; (4) operasi morfologi; (5) contour/feature measurement; (6) kalibrasi pixel-ke-mm; (7) bandingkan dengan ukuran aktual dan/atau aturan toleransi.

**Eksperimen wajib:** Bandingkan dua metode segmentasi; variasikan pencahayaan; ukur error terhadap penggaris/jangka sorong.

**Output:** Citra beranotasi, estimasi ukuran, grafik hasil vs referensi, metrik dan confusion matrix bila melakukan klasifikasi.

**Catatan:** Jaga kamera dan bidang ukur agar kalibrasi tetap valid.

### P06 — Marker-Based Augmented Reality

**Masalah:** Menambahkan overlay digital yang mengikuti lokasi dan orientasi marker planar saat kamera bergerak.

**Tahapan:** (1) Buat marker bergambar dengan tekstur cukup; (2) rekam pada berbagai sudut/jarak; (3) deteksi-deskripsi fitur; (4) matching; (5) homography RANSAC; (6) transformasi corner; (7) warp dan compositing overlay; (8) penanganan saat marker hilang.

**Eksperimen wajib:** Bandingkan ORB vs SIFT atau dua konfigurasi; variasikan jarak/rotasi; ukur kestabilan overlay.

**Output:** Video demonstrasi AR, gambar hasil deteksi, tabel success rate, FPS, dan jitter.

**Catatan:** Homography untuk overlay planar; pose dan objek 3D yang akurat memerlukan kalibrasi dan estimasi pose tambahan.

## 3. Persyaratan minimum (semua kelompok)

- [ ] Memiliki rumusan masalah, tujuan, dan diagram pipeline.
- [ ] Menggunakan **minimal 3 tahap** pemrosesan computer vision.
- [ ] Mengimplementasikan metode inti dengan Python/OpenCV dan mampu menjelaskan logikanya.
- [ ] Membandingkan **minimal 2 metode atau konfigurasi**.
- [ ] Menggunakan data pengujian yang memadai (lihat ketentuan tiap proyek), tidak hanya satu contoh.
- [ ] Menyertakan **metrik kuantitatif**, tabel/grafik, dan penjelasan cara perhitungan.
- [ ] Menguji dan membahas **minimal 2 kondisi kegagalan**.
- [ ] Mendokumentasikan parameter, versi library, sumber data, dan cara menjalankan kode.
- [ ] Menyertakan sitasi untuk kode, dataset, metode, atau aset eksternal.
- [ ] Tidak menjadikan API solusi otomatis sebagai satu-satunya implementasi inti (misalnya `cv2.Stitcher_create()` untuk keseluruhan P01).

## 4. Jadwal pengerjaan

| Pertemuan | Kegiatan | Luaran |
|---|---|---|
| 13 | Pemilihan proyek, rumusan masalah, desain, pengumpulan data | Proposal ringkas dan desain pipeline |
| 14 | Implementasi, eksperimen, perbaikan | Prototype dan hasil awal |
| 15 | Presentasi dan demo kelompok tahap 1 | Presentasi, demo, hasil akhir |
| 16 | Presentasi dan demo kelompok tahap 2 | Presentasi, demo, hasil akhir |

**Catatan:** Tenggat pengumpulan akhir berlaku sama untuk seluruh kelompok, termasuk yang presentasi pada pertemuan 16. Ikuti tanggal/jam yang diumumkan dosen.

## 5. Struktur folder pengumpulan

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

**Jika dataset/video besar:** Boleh menyertakan tautan akses yang bisa dibuka dosen dan petunjuk unduhnya. Jangan mengunggah data pribadi tanpa izin.

### Template isi `README.md` kelompok

Cantumkan: (1) judul dan kode proyek; (2) nama/NIM dan pembagian tugas; (3) deskripsi masalah; (4) desain pipeline; (5) spesifikasi perangkat dan versi perangkat lunak; (6) instruksi instalasi/eksekusi; (7) dataset dan cara mendapatkannya; (8) konfigurasi eksperimen; (9) ringkasan metrik dan tautan demo; (10) keterbatasan, referensi, dan lisensi/atribusi yang berlaku.

### Contoh instalasi dan eksekusi

```bash
python -m venv .venv
# Windows (PowerShell):
.venv\Scripts\Activate.ps1
# macOS/Linux:
# source .venv/bin/activate
pip install -r requirements.txt
python src/main.py --help
```

> Perintah `--help` adalah contoh antarmuka yang **disarankan**. Kelompok harus menuliskan perintah sebenarnya sesuai implementasi masing-masing. Jika menggunakan SIFT, pastikan versi OpenCV yang dipasang mendukungnya.

## 6. Format laporan (8–12 halaman, di luar lampiran)

1. **Pendahuluan** — latar belakang, rumusan masalah, tujuan, batasan.
2. **Metodologi** — dataset, diagram pipeline, algoritma dan persamaan penting, desain eksperimen dan metrik.
3. **Implementasi** — arsitektur kode, parameter, tahapan pemrosesan beserta contoh hasil.
4. **Hasil dan Pembahasan** — gambar/video contoh, tabel/grafik, perbandingan metode, kegagalan dan keterbatasan.
5. **Kesimpulan** — hasil utama dan pengembangan yang memungkinkan.
6. **Referensi** — gunakan format IEEE secara konsisten.

## 7. Presentasi dan demonstrasi

- Presentasi: **8 menit**.
- Demo aplikasi: **4 menit**.
- Tanya jawab: **5 menit**.
- Video demo yang dikumpulkan: **3–5 menit**.

Semua anggota kelompok harus memahami pipeline, kontribusi kode, parameter, dan hasil. Dosen dapat memberikan pertanyaan individual. Siapkan penjelasan untuk: mengapa metode dipilih, bagaimana metode bekerja, bagaimana evaluasi dihitung, apa perbedaan metode yang dibandingkan, dan kapan sistem gagal.

## 8. Rubrik penilaian

| Aspek | Bobot |
|---|---:|
| Rumusan masalah dan desain solusi | 15% |
| Implementasi algoritma computer vision | 30% |
| Eksperimen dan evaluasi kuantitatif | 25% |
| Analisis dan pembahasan hasil | 15% |
| Presentasi dan demonstrasi | 15% |
| **Total** | **100%** |

**Panduan level kualitas:**

- **85–100 (Sangat Baik):** Implementasi andal; eksperimen lengkap; metrik valid; analisis kritis dan mendalam.
- **70–84 (Baik):** Implementasi berfungsi; sebagian besar pengujian benar; analisis cukup jelas.
- **55–69 (Cukup):** Implementasi atau pengujian masih terbatas; analisis belum memadai.
- **0–54 (Kurang):** Pipeline tidak lengkap, hasil tidak dapat direproduksi, atau algoritma tidak dapat dijelaskan.

Dosen menilai tiap aspek berdasarkan kualitasnya lalu menerapkan bobot; penilaian individual dapat mempertimbangkan kontribusi dan pemahaman masing-masing anggota.

## 9. Checklist sebelum pengumpulan

- [ ] Program dapat dijalankan berdasarkan instruksi README kelompok.
- [ ] Dataset, parameter, dan dependensi terdokumentasi.
- [ ] Perbandingan algoritma/konfigurasi ditampilkan dalam tabel.
- [ ] Grafik, visualisasi hasil, dan analisis kegagalan tersedia.
- [ ] File `metrics.csv`, laporan PDF, slide PDF, dan video demo tersedia.
- [ ] Kontribusi anggota dan seluruh referensi dicantumkan.

---

**Prinsip utama:** Tunjukkan **bagaimana** algoritma bekerja, **seberapa baik** hasilnya, dan **mengapa** terjadi keberhasilan atau kegagalan — bukan hanya menampilkan aplikasi yang berjalan.
