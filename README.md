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

---

## 📊 Hasil Utama

Beberapa hasil penting dari proyek ini:

- **Deteksi Anomali**  
  Ditemukan beberapa sekolah dengan citra satelit tidak wajar (misalnya area kosong, kabur, atau tidak sesuai label).  
  Contoh hasil visualisasi:
  - `hasil/anomaly_detection/...`
  - `hasil/features/visualisasi/anomali/...`

- **Clustering Citra Satelit**  
  Sekolah berhasil dikelompokkan berdasarkan kemiripan visual menggunakan PCA + K-Means.  
  Hasil pengelompokan disimpan pada:  
  - `hasil/clustering/data_clustering.csv`  
  - Visualisasi: `hasil/features/visualisasi/scatter/...`

- **Exploratory Data Analysis (EDA)**  
  Peta persebaran sekolah dan distribusi akreditasi per provinsi dapat dilihat di folder:  
  - `hasil/eda/diagram/`
  - `hasil/eda/peta-per-provinsi/html/`

> 📌 *Kesimpulan singkat:* kombinasi **PCA + K-Means** memberikan segmentasi visual yang baik untuk mengelompokkan sekolah,  
> sedangkan fitur **HOG dan LBP** efektif untuk mendeteksi anomali citra satelit.

---
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

## 📂 Struktur Folder  

```
├── data
│   ├── data_deteksi_anomali.csv       # Data untuk deteksi anomali citra
│   ├── data_preprocessing.csv         # Data hasil preprocessing
│   ├── data_scraping_maps.csv         # Data hasil scraping dari Google Maps
│   └── gambar                         # Folder kumpulan gambar sekolah
│       └── ...
│
├── hasil
│   ├── anomaly_detection              # Hasil deteksi anomali (HOG, LBP, dll.)
│   │   ├── HOG_anomali_list.csv
│   │   ├── HOG_pca_anomaly.html
│   │   ├── LBP_anomali_list.csv
│   │   └── LBP_pca_anomaly.html
│   │
│   ├── clustering
│   │   └── data_clustering.csv        # Hasil pengelompokan (PCA + K-Means)
│   │
│   ├── eda                            # Hasil eksplorasi data
│   │   ├── diagram                    # Grafik distribusi & heatmap
│   │   └── peta-per-provinsi          # Peta HTML dan PNG tiap provinsi
│   │
│   └── features                       # Fitur hasil ekstraksi citra
│       ├── features                   # File fitur numpy (.npy)
│       │   ├── hog_features.npy
│       │   ├── lbp_features.npy
│       │   ├── mobilenetv2_features.npy
│       │   ├── resnet50_features.npy
│       │   └── vgg16_features.npy
│       └── visualisasi                # Hasil visualisasi fitur & anomali
│           ├── anomali
│           ├── overlay
│           └── scatter
│
├── notebooks
│   ├── 1_preprocessing_data.ipynb           # Tahap 1: Preprocessing data
│   ├── 2_exploratory_data_analysis.ipynb    # Tahap 2: EDA
│   ├── 3_feature_extractions.ipynb          # Tahap 3: Ekstraksi fitur
│   ├── 4_anomaly_detection.ipynb            # Tahap 4: Deteksi anomali
│   └── 5_clustering_citra_satelit.ipynb     # Tahap 5: Clustering citra satelit
│
└── README.md                                # Dokumentasi utama proyek

```

---

## 📝 Keterangan  

1. **data/**  
   - Menyimpan seluruh data mentah, hasil preprocessing, serta hasil scraping dari Google Maps.  
   - File penting:  
     - `data_scraping_maps.csv` → hasil scraping awal.  
     - `data_preprocessing.csv` → data yang sudah dibersihkan dan distandarisasi.  
     - `data_deteksi_anomali.csv` → data untuk proses deteksi anomali citra.  
     - `evaluasi.csv` → hasil evaluasi performa model.  
   - Folder `gambar/` berisi kumpulan citra sekolah hasil scraping.  

2. **hasil/**  
   Folder ini berisi seluruh hasil analisis, visualisasi, dan ekstraksi fitur dari citra satelit, dibagi ke beberapa subfolder:  
   - **anomaly_detection/** → hasil deteksi anomali berdasarkan fitur (HOG, LBP, dsb).  
     - Contoh file: `HOG_anomali_list.csv`, `LBP_pca_anomaly.html`.  
   - **clustering/** → hasil pengelompokan citra sekolah menggunakan PCA + K-Means.  
     - Contoh file: `data_clustering.csv`.  
   - **eda/** → hasil *Exploratory Data Analysis* dalam bentuk grafik dan peta persebaran sekolah per provinsi.  
     - Subfolder `diagram/` berisi grafik distribusi dan heatmap.  
     - Subfolder `peta-per-provinsi/` berisi peta interaktif (`.html`) dan versi gambar (`.png`).  
   - **features/** → hasil ekstraksi fitur citra dari berbagai metode.  
     - Subfolder `features/` berisi file `.npy` untuk HOG, LBP, VGG16, ResNet50, MobileNetV2.  
     - Subfolder `visualisasi/` berisi hasil visualisasi anomali, overlay fitur, dan scatter PCA/t-SNE.

> ⚠️ **Catatan:** Folder `hasil/` di repository ini hanya berisi **contoh output**.  
> Untuk mendapatkan hasil lengkap, silakan jalankan seluruh notebook di folder `notebooks/` atau hubungi:  
> 📧 **saazizau@gmail.com** / **algaedesma2004@gmail.com**

3. **notebooks/**  
   - Berisi seluruh tahapan pemrosesan dan analisis dalam format Jupyter Notebook:  
     1. `1_preprocessing_data.ipynb`         → tahap preprocessing data.  
     2. `2_exploratory_data_analysis.ipynb`  → eksplorasi dan visualisasi data.  
     3. `3_feature_extractions.ipynb`        → ekstraksi fitur citra (HOG, LBP, CNN).  
     4. `4_anomaly_detection.ipynb`          → deteksi anomali citra berdasarkan fitur.  
     5. `5_clustering_citra_satelit.ipynb`   → pengelompokan citra dengan PCA + K-Means.  

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

