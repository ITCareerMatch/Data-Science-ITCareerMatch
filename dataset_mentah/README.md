# dataset_mentah — Dataset Mentah (Raw Data)

Folder ini menyimpan **data mentah sebelum diproses** yang menjadi bahan baku pipeline data science proyek **ITCareerMatch**. Data di sini belum melewati proses pembersihan atau normalisasi.

---

## Isi Folder

| File | Ukuran | Sumber | Deskripsi |
|------|--------|--------|-----------|
| `dataset_tambahan_cv.xlsx` | ~23.2 MB | Kaggle + Huggingface | Dataset tambahan profil CV kandidat (open source) sebelum diproses |
| `hasil_cv_kaggle_it_ocr.xlsx` | ~5.2 MB | OCR (Tesseract/pdfplumber) | Hasil ekstraksi teks dari file PDF CV bidang IT menggunakan OCR |

---

## Catatan Penting

> Data dalam folder ini adalah **data mentah** dan belum siap untuk analisis langsung. Gunakan dataset dari folder `../dataset_clean/` untuk keperluan analisis dan pemodelan.

---

## Dataset Eksternal (Tidak Disimpan di Repo)

Beberapa dataset berukuran besar disimpan di Google Drive karena keterbatasan ukuran repositori:

| Dataset | Deskripsi | Link |
|---------|-----------|------|
| `add_dataset_job` | Dataset lowongan kerja global dari Kaggle & Huggingface | [Google Drive](https://drive.google.com/drive/folders/1TtqgWt3syTYXziRqSZ2gGf9MOF-J6tSZ?usp=sharing) |
| `cv_kaggle_it_pdf` | File PDF CV dari Kaggle (sudah difilter posisi IT) | [Google Drive](https://drive.google.com/file/d/15X7Q7Uk1b2EqkdP57zkxGiUy2XkrquE6/view?usp=drive_link) |
| `updated_dataset_scraping_xlsx` | Data mentah hasil scraping lowongan IT dari Glints | [Google Drive](https://drive.google.com/drive/folders/1JAOwmHqFhRasohPOUWoGYwtbnvroPJ7n?usp=drive_link) |

---

## Alur Pengolahan Data

```
dataset_mentah/ (Sini)
      │
      ├── dataset_tambahan_cv.xlsx
      │         ↓
      │   pipeline_cv_data_cleaning.ipynb
      │         ↓
      │   dataset_clean/dataset_cv.xlsx
      │
      ├── hasil_cv_kaggle_it_ocr.xlsx
      │         ↓
      │   pipeline_cv_data_cleaning.ipynb
      │         ↓
      │   dataset_clean/dataset_cv.xlsx
      │
      └── [Dataset Job dari Drive]
                ↓
          pipeline_job_data_cleaning.ipynb
                ↓
          dataset_clean/dataset_job.xlsx
```

---

## Deskripsi Dataset

### `dataset_tambahan_cv.xlsx`
- **Sumber**: Kaggle (open source) dan Huggingface
- **Isi**: Data profil CV kandidat dalam format teks bebas
- **Status**: Belum dinormalisasi — kolom `detail` masih dalam format mentah
- **Diproses oleh**: `notebook/pipeline_cv_data_cleaning.ipynb`

### `hasil_cv_kaggle_it_ocr.xlsx`
- **Sumber**: Hasil OCR menggunakan Tesseract & pdfplumber dari file PDF CV bidang IT
- **Isi**: Teks hasil ekstraksi OCR dari halaman PDF CV
- **Status**: Teks mentah hasil OCR, belum dibersihkan
- **Diproses oleh**: `notebook/pipeline_cv_data_cleaning.ipynb`

---

## Tools yang Digunakan untuk Membuat Data Ini

| Tool | Fungsi |
|------|--------|
| **pdfplumber** | Ekstraksi teks dari PDF berbasis teks |
| **Tesseract OCR** | Ekstraksi teks dari PDF hasil scan/gambar |
| **Poppler** | Rendering & konversi halaman PDF ke gambar |
| **Selenium** | Web scraping lowongan dari platform Glints |

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
