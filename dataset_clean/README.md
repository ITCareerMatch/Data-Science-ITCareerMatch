# dataset_clean — Dataset Bersih

Folder ini menyimpan **dataset yang sudah melalui proses pembersihan, normalisasi, dan standarisasi** dari pipeline data science proyek **ITCareerMatch**. Dataset di sini siap digunakan untuk analisis, EDA, dan pemodelan.

---

## Isi Folder

| File | Ukuran | Deskripsi |
|------|--------|-----------|
| `dataset_cv.xlsx` | ~1.5 MB | Data profil kandidat/CV yang sudah dibersihkan dan dinormalisasi |
| `dataset_job.xlsx` | ~2.1 MB | Data lowongan pekerjaan yang sudah dibersihkan dan dinormalisasi |
| `glints_job.xlsx` | ~347 KB | Data lowongan hasil scraping dari platform Glints yang sudah dibersihkan |

---

## Proses Pembersihan yang Sudah Dilakukan

### `dataset_cv.xlsx`
- Normalisasi kolom `detail` menggunakan LLM (Groq LLaMA-3.1-8b)
- Standarisasi nama skill menggunakan `kamus_skill_cv.csv`
- Penghapusan duplikasi dan nilai kosong
- Standardisasi format kolom (pendidikan, pengalaman, dll.)

### `dataset_job.xlsx`
- Normalisasi kolom `kualifikasi` menggunakan LLM (Groq LLaMA-3.1-8b)
- Standarisasi nama skill menggunakan `Kamus_IT_Bersih_Filtered.csv`
- Pembersihan teks dan format kolom
- Kategorisasi level pengalaman (entry/mid/senior)

### `glints_job.xlsx`
- Pembersihan data hasil scraping web
- Normalisasi kolom: lokasi, kategori peran, sistem kerja, gaji
- Standarisasi format gaji dan tipe waktu kerja

---

## Kolom Utama

### `dataset_cv.xlsx`
| Kolom | Deskripsi |
|-------|-----------|
| `pendidikan` | Jenjang pendidikan terakhir kandidat |
| `pengalaman` | Pengalaman kerja (dalam tahun atau kategori) |
| `skill` | Daftar skill kandidat (sudah terstandarisasi) |
| `detail` | Ringkasan profil kandidat (sudah ternormalisasi) |

### `dataset_job.xlsx`
| Kolom | Deskripsi |
|-------|-----------|
| `posisi` | Nama posisi/jabatan yang ditawarkan |
| `pengalaman` | Pengalaman yang disyaratkan |
| `pendidikan` | Pendidikan minimal yang disyaratkan |
| `kualifikasi` | Kualifikasi detail (sudah ternormalisasi) |
| `gender` | Syarat gender (jika ada) |
| `usia` | Syarat usia (jika ada) |

### `glints_job.xlsx`
| Kolom | Deskripsi |
|-------|-----------|
| `kategori_peran` | Kategori posisi IT (Backend, Frontend, ML, dll.) |
| `lokasi` | Kota lokasi pekerjaan |
| `sistem_kerja` | WFO / WFH / Hybrid |
| `tipe_waktu_kerja` | Penuh Waktu / Paruh Waktu / Freelance |
| `gaji` | Rentang gaji (sudah dinormalisasi) |
| `skill` | Skill yang dibutuhkan |

---

## Sumber Data

| Dataset | Pipeline Pembersihan | Sumber Asli |
|---------|---------------------|-------------|
| `dataset_cv.xlsx` | `notebook/pipeline_cv_data_cleaning.ipynb` | `dataset_mentah/dataset_tambahan_cv.xlsx` |
| `dataset_job.xlsx` | `notebook/pipeline_job_data_cleaning.ipynb` | `dataset_mentah/hasil_cv_kaggle_it_ocr.xlsx` |
| `glints_job.xlsx` | `notebook/kode_scraping.ipynb` | Web scraping Glints |

---

## Digunakan Oleh

- `notebook/EDA_data_clean.ipynb` — Eksplorasi dan analisis data
- `AB Testing/ITCareerMatch_AB_Testing.ipynb` — Eksperimen pencocokan
- `Dashboard_Streamlit/` — Visualisasi interaktif (via folder `data/`)

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
