# 📌 Proyek CLUSTERING-CITRA-SATELIT

Proyek ini merupakan **bagian ketiga** dari lima tahap utama inisiatif **SKYLEARN**:  

1. **SCRAPING-DATA-SEKOLAH**  
2. **SCRAPING-CITRA-SATELIT**  
3. **CLUSTERING-SEKOLAH**  
4. **KLASIFIKASI-SEKOLAH**  
5. **DEPLOYMENT**  

---

## 🎯 Tujuan  

Tujuan dari **CLUSTERING-CITRA-SATELIT** adalah melakukan **analisis clustering** pada citra satelit bangunan sekolah untuk **14.927 SMA di Indonesia**.

📂 **`../data/data_scraping_maps.csv`** — gabungan dari:  
1. **Data sekolah** (nama sekolah, kabupaten/kota, provinsi) hasil tahap **SCRAPING-DATA-SEKOLAH**  
2. **Citra satelit sekolah** hasil tahap **SCRAPING-CITRA-SATELIT**  

## 🗂️ Struktur Dataset  

Kolom dalam dataset:  

- `nomor` → nomor urut data  
- `kode_sekolah` → kode unik sekolah  
- `nama_sekolah` → nama resmi sekolah  
- `alamat` → alamat lengkap sekolah  
- `kabupaten` → kabupaten sekolah berada  
- `kota` → kota (jika ada)  
- `provinsi` → provinsi sekolah  
- `akreditasi` → akreditasi sekolah (A, B, C, dll)  
- `nama_sekolah_di_maps` → nama sekolah versi Google Maps  
- `long` → longitude sekolah  
- `lat` → latitude sekolah  
- `dir_gambar_ori` → path citra satelit asli  
- `dir_gambar_titik` → path citra satelit dengan titik lokasi  
- `dir_gambar_kotak_dan_yolo` → path citra satelit dengan bounding box + YOLO  
- `keterangan` → status scraping (misal: sukses/gagal)  

---

## 📊 Contoh Data  

| nomor | kode_sekolah | nama_sekolah                | kabupaten   | provinsi | akreditasi | nama_sekolah_di_maps      | long      | lat      | dir_gambar_ori                                                                 | dir_gambar_titik                                                               | dir_gambar_kotak_dan_yolo                                                                 | keterangan |
|-------|--------------|-----------------------------|-------------|----------|------------|---------------------------|-----------|----------|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|------------|
| 1     | 10100139     | SMA NEGERI 1 LEMBAH SEULAWAH | Aceh Besar  | Aceh     | A          | SMA NEGERI 1 LEMBAH SEULAWAH | 95.682881 | 5.370129 | `../hasil/gambar_ori/ACEH/KAB ACEH BESAR/sma_negeri_1_lembah_seulawah.jpg`     | `../hasil/gambar_titik/ACEH/KAB ACEH BESAR/sma_negeri_1_lembah_seulawah.jpg`     | `../hasil/gambar_kotak_dan_yolo/ACEH/KAB ACEH BESAR/img/sma_negeri_1_lembah_seulawah.jpg`     | sukses     |
| 2     | 10100170     | SMA NEGERI MODAL BANGSA     | Aceh Besar  | Aceh     | A          | SMA Negeri Modal Bangsa   | 95.395695 | 5.508437 | `../hasil/gambar_ori/ACEH/KAB ACEH BESAR/sma_negeri_modal_bangsa.jpg`          | `../hasil/gambar_titik/ACEH/KAB ACEH BESAR/sma_negeri_modal_bangsa.jpg`          | `../hasil/gambar_kotak_dan_yolo/ACEH/KAB ACEH BESAR/img/sma_negeri_modal_bangsa.jpg`          | sukses     |
| 3     | 10100176     | SMAS MALEM PUTRA 1          | Aceh Besar  | Aceh     | C          | SMP Malem Putra 1         | 95.330857 | 5.493038 | `../hasil/gambar_ori/ACEH/KAB ACEH BESAR/smp_malem_putra_1.jpg`                | `../hasil/gambar_titik/ACEH/KAB ACEH BESAR/smp_malem_putra_1.jpg`                | `../hasil/gambar_kotak_dan_yolo/ACEH/KAB ACEH BESAR/img/smp_malem_putra_1.jpg`                | sukses     |

---



---

## 📂 Struktur Folder  

```
CLUSTREING-CITRA-SATELIT/
├── data                               # Berisi data mentah dan hasil scraping citra satelit
│   ├── data_preprocessing.csv         # Data sekolah yang sudah dibersihkan dan siap digunakan
│   ├── data_scraping_maps.csv         # Data sekolah hasil scraping dari Google Maps atau sumber lain
│   └── gambar                         # Folder yang menyimpan semua citra satelit sekolah
├── hasil                  # Berisi semua output analisis dan ekstraksi fitur
│   ├── eda                # Hasil Exploratory Data Analysis
│   │   ├── diagram        # Diagram visualisasi statistik
│   │   │   ├── distribusi_akreditasi.png                         # Distribusi akreditasi sekolah secara umum
│   │   │   ├── distribusi_akreditasi_per_provinsi_stacked.png    # Distribusi akreditasi per provinsi (stacked)
│   │   │   ├── heatmap_akreditasi_per_provinsi.png               # Heatmap akreditasi per provinsi
│   │   │   ├── jumlah_sekolah_per_provinsi.png                   # Jumlah sekolah per provinsi
│   │   │   ├── persentase_akreditasi_per_provinsi.png            # Persentase akreditasi per provinsi
│   │   │   └── sebaran_sekolah_per_akreditasi.png                # Sebaran sekolah berdasarkan akreditasi
│   │   └── peta-per-provinsi
│   │       ├── html           # File HTML interaktif peta per provinsi
│   │       └── img            # Screenshot/hasil rendering peta per provinsi
│   └── features               # Hasil ekstraksi fitur citra
│       ├── overlay            # Visualisasi overlay fitur pada citra
│       └── scater             # Scatter plot hasil reduksi dimensi (PCA, t-SNE)
│       ├── hog_features.npy       # Fitur HOG (Histogram of Oriented Gradients)
│       ├── lbp_features.npy       # Fitur LBP (Local Binary Pattern)
│       ├── vgg16_features.npy     # Fitur dari model VGG16
│       ├── resnet50_features.npy  # Fitur dari model ResNet50
│       └── mobilenetv2_features.npy # Fitur dari model MobileNetV2
├── notebooks                                # Notebook Jupyter untuk alur proyek
│   ├── 1_preprocessing_data.ipynb           # Notebook untuk pembersihan dan persiapan data
│   ├── 2_exploratory_data_analysis.ipynb    # Notebook untuk EDA
│   └── 3_feature_extractions.ipynb          # Notebook untuk ekstraksi fitur citra
└── README.md                # Dokumentasi utama proyek

```

---

## 📝 Keterangan  

1. **data/**  
   - Menyimpan data mentah atau referensi tambahan.  
   - `README.md` di dalam folder ini berisi catatan sumber data.

2. **hasil/**  
   Folder ini berisi semua hasil scraping citra satelit yang telah diproses, dibagi menjadi beberapa subfolder:  
   - **gambar_kotak_dan_yolo/**: berisi gambar sekolah dengan bounding box dan label YOLO untuk deteksi objek.  
   - **gambar_ori/**: gambar asli dari citra satelit.  
   - **gambar_titik/**: gambar citra satelit dengan titik lokasi sekolah yang ditandai.  
   - **tile/**: menyimpan potongan-potongan tile sebelum digabung menjadi citra utuh.

>⚠️ **Catatan:** Folder `hasil/` yang ada di repository hanyalah **sampel**. Apabila ingin mendapatkan hasil penuh, bisa menjalankan program sendiri atau menghubungi email: **saazizau@gmail.com** / **algaedesma2004@gmail.com**.

3. **notebooks/**  
   - **scraping_citra_satelit.ipynb**: notebook utama untuk scraping citra satelit.  
   - **gambar/**: dokumentasi gambar yang digunakan atau dihasilkan selama pengembangan notebook.  

---

## 🤝 Kolaborasi  

Proyek ini dikerjakan secara kolaboratif dalam rangka inisiatif **SKYLEARN**.  

### 👥 Kontributor  
- 🌟 **Algae Desma Fridasary** — *Ketua Tim & Visioner Utama*  
  Pemilik ide dan penggerak utama proyek. Berfokus pada penulisan artikel ilmiah serta deployment sistem.  

- 🎓 **Sabrina Aziz Aulia** — *Mentor & Spesialis Komputasi*  
  Memberikan arahan strategis dan pendampingan teknis, terutama dalam aspek komputasi dan pemodelan data.  

---

## 📢 Kontribusi  

Kami sangat terbuka untuk kontribusi dari komunitas!  
- Buat **issue** untuk melaporkan bug atau memberikan ide.  
- Ajukan **pull request** jika ingin menambahkan fitur atau perbaikan.  

> Mari bersama-sama membangun ekosistem data sekolah Indonesia yang lebih terbuka, rapi, dan bermanfaat 🚀  

