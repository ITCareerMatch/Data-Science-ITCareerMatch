# ITCareerMatch — Data Science Repository

Repositori ini berisi seluruh pipeline data science untuk proyek **ITCareerMatch**, sebuah sistem pencocokan karier IT berdasarkan profil CV dan lowongan pekerjaan. Proses mencakup scraping, OCR, preprocessing, normalisasi, hingga EDA.

---

## 🗂️ Struktur Direktori

```
Data-Science-ITCareerMatch/
│
├── checkpoint_LLM/               # Checkpoint batch processing preprocessing & normalisasi
│   ├── normalisasi kolom `detail` pada dataset CV
│   ├── normalisasi kolom `kualifikasi` pada dataset Job
│   └── normalisasi teks hasil OCR dari file PDF CV
│
├── dataset_clean/                # Dataset bersih siap pakai
│   ├── dataset_cv                    # Data CV yang sudah dibersihkan
│   ├── dataset_job                   # Data lowongan pekerjaan yang sudah dibersihkan
│   └── glints_job                    # Data hasil scraping dari Glints yang sudah dibersihkan
│
├── dataset_mentah/               # Data mentah sebelum diproses
│   ├── data_cv_kaggle                # Dataset CV dari Kaggle (open source)
│   ├── hasil_cv_kaggle_it_ocr        # Hasil OCR dari CV Kaggle bidang IT
│   ├── dataset_job_kaggle            # [link menyusul]
│   ├── pdf_cv/                       # Folder file PDF CV [link menyusul]
│   └── hasil_scraping/               # Data mentah hasil scraping [link menyusul]
│
├── notebook/                     # Kode Python pipeline & analisis
│   ├── pipeline pembersihan dataset CV
│   ├── pipeline pembersihan dataset Job
│   ├── kode scraping lowongan
│   └── EDA data bersih
│
├── Kamus_IT_Bersih_Filtered.csv  # Kamus standarisasi skill pada data Job
└── kamus_skill_cv.csv            # Kamus standarisasi skill pada data CV
```

---

## 🔄 Alur Pipeline

```
Data Mentah (Kaggle / Scraping / PDF CV)
        ↓
  OCR (PDF CV → Teks)
        ↓
  Preprocessing & Normalisasi (checkpoint_LLM)
  - Normalisasi kolom detail CV
  - Normalisasi kolom kualifikasi Job
  - Normalisasi teks hasil OCR
        ↓
  Standarisasi Skill
  - CV   → kamus_skill_cv.csv
  - Job  → Kamus_IT_Bersih_Filtered.csv
        ↓
  Dataset Bersih (dataset_clean/)
        ↓
  EDA & Analisis (notebook/)
```

---

## 📊 Dataset

### Dataset Bersih (`dataset_clean/`)

| Nama | Deskripsi |
|---|---|
| `dataset_cv` | Data CV yang telah dibersihkan dan dinormalisasi |
| `dataset_job` | Data lowongan pekerjaan yang telah dibersihkan dan dinormalisasi |
| `glints_job` | Data lowongan hasil scraping dari platform Glints telah dibersihkan dan dinormalisasi |

### Dataset Mentah (`dataset_mentah/`)

| Nama | Sumber | Deskripsi |
|---|---|---|
| `data_cv_kaggle` | Kaggle (open source) | Dataset CV tambahan |
| `hasil_cv_kaggle_it_ocr` | OCR | Hasil ekstraksi teks dari PDF CV bidang IT |
| `add_dataset_job` | Kaggle & Huggingface (open source) | Dataset job global https://drive.google.com/drive/folders/1TtqgWt3syTYXziRqSZ2gGf9MOF-J6tSZ?usp=sharing |
| `cv_kaggle_it_pdf` | Kaggle (open source)  | Folder berisi file PDF CV yang telah difilter khusus posisi IT https://drive.google.com/file/d/15X7Q7Uk1b2EqkdP57zkxGiUy2XkrquE6/view?usp=drive_link |
| `updated_dataset_scraping_xlsx` | Glints Web scraping | Data mentah hasil scraping lowongan IT https://drive.google.com/drive/folders/1JAOwmHqFhRasohPOUWoGYwtbnvroPJ7n?usp=drive_link |

---

## 📓 Notebook

| Notebook | Fungsi |
|---|---|
| Pipeline CV | Pembersihan dan preprocessing dataset CV |
| Pipeline Job | Pembersihan dan preprocessing dataset lowongan |
| Scraping | Pengambilan data lowongan dari web (Glints, dll.) |
| EDA | Eksplorasi dan analisis data bersih |

---

## 📁 File Kamus

| File | Digunakan Untuk |
|---|---|
| `kamus_skill_cv.csv` | Standarisasi nama skill pada data CV |
| `Kamus_IT_Bersih_Filtered.csv` | Standarisasi skill pada data Job (terminologi IT) |

---

## 🛠️ Teknologi

| Kategori | Tools |
|---|---|
| Bahasa | Python |
| Notebook | Jupyter Notebook |
| Ekstraksi PDF | pdfplumber untuk ekstraksi teks dari PDF berbasis teks |
| OCR | Tesseract untuk ekstraksi teks dari PDF hasil scan/gambar |
| PDF Processing | Poppler untuk  rendering dan konversi halaman PDF |
| LLM | Groq LLM API (LLaMA-3.1-8b-Instant) digunakan pada tahap normalisasi (batch processing) |
| Scraping | Selenium |
| Data Processing | Pandas, NumPy |

---

## 👥 Kontributor

Proyek ini dikembangkan oleh tim **ITCareerMatch**.
