# ITCareerMatch — Data Science Repository

Repositori ini berisi seluruh pipeline data science untuk proyek **ITCareerMatch**, sebuah sistem pencocokan karier IT berdasarkan profil CV dan lowongan pekerjaan. Proses mencakup scraping, OCR, preprocessing, normalisasi, EDA, A/B Testing, hingga dashboard interaktif.

**Project:** Data Science Capstone — DBS Foundation Coding Camp 2026

**Live Demo Dashboard:** [dashboard-itcareermatch.streamlit.app](https://dashboard-data-science-itcareermatch.streamlit.app/)

---

## Struktur Direktori

```
Data-Science-ITCareerMatch/
│
├── AB Testing/                    # Eksperimen A/B Testing sistem job matching
│   ├── ITCareerMatch_AB_Testing.ipynb
│   └── README.md  ← lihat detail
│
├── Dashboard_Streamlit/           # Dashboard analitik interaktif berbasis Streamlit
│   ├── app.py                         # Entry point Streamlit
│   ├── data_loader.py                 # Pemuatan & preprocessing dataset
│   ├── visualizations.py             # Fungsi chart Plotly per Business Question
│   ├── requirements.txt
│   ├── data/                          # Dataset untuk dashboard
│   └── README.md  ← lihat detail
│
├── checkpoint_LLM/                # Checkpoint batch processing LLM
│   ├── detail_checkpoint_dataset_cv_ocr.xlsx
│   ├── detail_checkpoint_dataset_tambahan_cv.xlsx
│   ├── kualifikasi_checkpoint.csv
│   └── README.md  ← lihat detail
│
├── dataset_clean/                 # Dataset bersih siap pakai
│   ├── dataset_cv.xlsx                # Data CV yang sudah dibersihkan
│   ├── dataset_job.xlsx               # Data lowongan pekerjaan yang sudah dibersihkan
│   ├── glints_job.xlsx                # Data scraping Glints yang sudah dibersihkan
│   └── README.md  ← lihat detail
│
├── dataset_mentah/                # Data mentah sebelum diproses
│   ├── dataset_tambahan_cv.xlsx       # Dataset CV tambahan (Kaggle/Huggingface)
│   ├── hasil_cv_kaggle_it_ocr.xlsx    # Hasil OCR dari PDF CV bidang IT
│   └── README.md  ← lihat detail
│
├── kamus/                         # Kamus standarisasi skill IT
│   ├── Kamus_IT_Bersih_Filtered.csv   # Kamus skill untuk dataset Job
│   ├── kamus_skill_cv.csv             # Kamus skill untuk dataset CV
│   └── README.md  ← lihat detail
│
└── notebook/                      # Kode Python pipeline & analisis
    ├── pipeline_cv_data_cleaning.ipynb
    ├── pipeline_job_data_cleaning.ipynb
    ├── kode_scraping.ipynb
    ├── EDA_data_clean.ipynb
    └── README.md  ← lihat detail
```

---

## Alur Pipeline

```
Data Mentah (Kaggle / Huggingface / Web Scraping / PDF CV)
        ↓
  OCR (PDF CV → Teks)
  [pdfplumber / Tesseract / Poppler]
        ↓
  Web Scraping (Glints → Data Lowongan)
  [Selenium]
        ↓
  Preprocessing & Normalisasi (checkpoint_LLM/)
  - Normalisasi kolom detail CV      → Groq LLaMA-3.1-8b
  - Normalisasi kolom kualifikasi Job → Groq LLaMA-3.1-8b
  - Normalisasi teks hasil OCR
        ↓
  Standarisasi Skill (kamus/)
  - CV   → kamus_skill_cv.csv
  - Job  → Kamus_IT_Bersih_Filtered.csv
        ↓
  Dataset Bersih (dataset_clean/)
        ↓
  ┌─────────────────────────────────┐
  │  EDA & Analisis (notebook/)     │
  │  A/B Testing (AB Testing/)      │
  │  Dashboard (Dashboard_Streamlit/)│
  └─────────────────────────────────┘
```

---

## Dataset

### Dataset Bersih (`dataset_clean/`) — [README](./dataset_clean/README.md)

| Nama | Ukuran | Deskripsi |
|------|--------|-----------|
| `dataset_cv.xlsx` | ~1.5 MB | Data CV yang telah dibersihkan dan dinormalisasi |
| `dataset_job.xlsx` | ~2.1 MB | Data lowongan pekerjaan yang telah dibersihkan dan dinormalisasi |
| `glints_job.xlsx` | ~347 KB | Data lowongan hasil scraping dari Glints telah dibersihkan |

### Dataset Mentah (`dataset_mentah/`) — [README](./dataset_mentah/README.md)

| Nama | Sumber | Deskripsi |
|------|--------|-----------|
| `dataset_tambahan_cv.xlsx` | Kaggle & Huggingface | Dataset CV tambahan (open source) |
| `hasil_cv_kaggle_it_ocr.xlsx` | OCR | Hasil ekstraksi teks dari PDF CV bidang IT |
| `add_dataset_job` | Kaggle & Huggingface | Dataset job global — [Google Drive](https://drive.google.com/drive/folders/1TtqgWt3syTYXziRqSZ2gGf9MOF-J6tSZ?usp=sharing) |
| `cv_kaggle_it_pdf` | Kaggle | Folder PDF CV yang difilter posisi IT — [Google Drive](https://drive.google.com/file/d/15X7Q7Uk1b2EqkdP57zkxGiUy2XkrquE6/view?usp=drive_link) |
| `updated_dataset_scraping_xlsx` | Glints Web Scraping | Data mentah hasil scraping lowongan IT — [Google Drive](https://drive.google.com/drive/folders/1JAOwmHqFhRasohPOUWoGYwtbnvroPJ7n?usp=drive_link) |

---

## Notebook (`notebook/`) — [README](./notebook/README.md)

| Notebook | Fungsi |
|----------|--------|
| `pipeline_cv_data_cleaning.ipynb` | Pembersihan dan preprocessing dataset CV |
| `pipeline_job_data_cleaning.ipynb` | Pembersihan dan preprocessing dataset lowongan |
| `kode_scraping.ipynb` | Pengambilan data lowongan dari web (Glints) |
| `EDA_data_clean.ipynb` | Eksplorasi dan analisis data bersih |

---

## A/B Testing (`AB Testing/`) — [README](./AB%20Testing/README.md)

Eksperimen untuk membandingkan dan mengevaluasi dua varian pendekatan sistem pencocokan kandidat dengan lowongan IT secara statistik.

---

## Dashboard Streamlit (`Dashboard_Streamlit/`) — [README](./Dashboard_Streamlit/README.md)

Dashboard interaktif berbasis Streamlit yang menjawab **10 Business Questions** tentang rekrutmen IT di Indonesia, mencakup analisis supply (kandidat), demand (lowongan), dan gap analysis.

| BQ | Pertanyaan Bisnis | Dataset |
|----|------------------|---------| 
| BQ 1 | Distribusi tingkat pendidikan kandidat | Dataset_CV |
| BQ 2 | Proporsi lowongan entry / mid / senior | Dataset_Job |
| BQ 3 | Top 5 kota dengan lowongan terbanyak & komposisi WFO/WFH | Glints_Job |
| BQ 4 | Top 10 & Bottom 10 kategori peran berdasarkan median gaji | Glints_Job |
| BQ 5 | Gap distribusi pendidikan kandidat vs. syarat lowongan | CV + Job |
| BQ 6 | Top 15 skill paling sering dicari | Glints_Job |
| BQ 7 | Rata-rata jumlah skill per bucket pengalaman | Dataset_CV |
| BQ 8 | Dominasi Penuh Waktu per kategori peran | Glints_Job |
| BQ 9 | Lowongan dengan batasan gender/usia | Dataset_Job |
| BQ 10 | Perbandingan median gaji WFO vs. WFH vs. Hybrid | Glints_Job |

---

## Kamus Skill (`kamus/`) — [README](./kamus/README.md)

| File | Digunakan Untuk |
|------|-----------------|
| `kamus_skill_cv.csv` | Standarisasi nama skill pada data CV |
| `Kamus_IT_Bersih_Filtered.csv` | Standarisasi skill pada data Job (terminologi IT) |

---

## Checkpoint LLM (`checkpoint_LLM/`) — [README](./checkpoint_LLM/README.md)

File checkpoint untuk melanjutkan proses normalisasi LLM yang panjang tanpa mengulang dari awal.

---

## Teknologi

| Kategori | Tools |
|----------|-------|
| Bahasa | Python 3.8+ |
| Notebook | Jupyter Notebook |
| Ekstraksi PDF | pdfplumber |
| OCR | Tesseract |
| PDF Processing | Poppler |
| LLM | Groq API (LLaMA-3.1-8b-Instant) |
| Scraping | Selenium |
| Data Processing | Pandas, NumPy |
| Visualisasi | Plotly, Matplotlib, Seaborn |
| Dashboard | Streamlit |
| Statistik | SciPy |

---

## Cara Memulai

### 1. Clone repositori
```bash
git clone https://github.com/your-org/Data-Science-ITCareerMatch.git
cd Data-Science-ITCareerMatch
```

### 2. Buat virtual environment
```bash
python -m venv venv
venv\Scripts\activate   # Windows
```

### 3. Install dependensi notebook
```bash
pip install pandas numpy openpyxl jupyter selenium groq plotly matplotlib seaborn scipy
```

### 4. Jalankan pipeline (urutan yang direkomendasikan)
```bash
jupyter notebook notebook/kode_scraping.ipynb
jupyter notebook notebook/pipeline_cv_data_cleaning.ipynb
jupyter notebook notebook/pipeline_job_data_cleaning.ipynb
jupyter notebook notebook/EDA_data_clean.ipynb
```

### 5. Jalankan dashboard
```bash
cd Dashboard_Streamlit
pip install -r requirements.txt
streamlit run app.py
```

---

## Kontributor

Proyek ini dikembangkan oleh tim **ITCareerMatch** sebagai bagian dari program **DBS Foundation Coding Camp 2026**.
