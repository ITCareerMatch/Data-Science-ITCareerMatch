# notebook — Pipeline & Analisis Data

Folder ini berisi **Jupyter Notebook** yang mencakup seluruh pipeline pembersihan data, scraping, dan eksplorasi data (EDA) untuk proyek **ITCareerMatch**.

---

## Isi Folder

| Notebook | Fungsi Utama |
|----------|-------------|
| `pipeline_cv_data_cleaning.ipynb` | Pipeline pembersihan dan normalisasi dataset CV |
| `pipeline_job_data_cleaning.ipynb` | Pipeline pembersihan dan normalisasi dataset lowongan kerja |
| `kode_scraping.ipynb` | Pengambilan data lowongan IT dari web (Glints) |
| `EDA_data_clean.ipynb` | Eksplorasi dan analisis data bersih (EDA) |

---

## Urutan Eksekusi yang Direkomendasikan

```
1. kode_scraping.ipynb
          ↓ (menghasilkan data mentah scraping)
2. pipeline_cv_data_cleaning.ipynb
          ↓ (menghasilkan dataset_clean/dataset_cv.xlsx)
3. pipeline_job_data_cleaning.ipynb
          ↓ (menghasilkan dataset_clean/dataset_job.xlsx)
4. EDA_data_clean.ipynb
          ↓ (menghasilkan insight & visualisasi)
```

---

## Detail Setiap Notebook

### 1. `kode_scraping.ipynb`
- **Tujuan**: Scraping data lowongan IT dari platform **Glints**
- **Output**: Data mentah lowongan (disimpan di `dataset_mentah/`)
- **Tools**: Selenium, pandas
- **Catatan**: Memerlukan ChromeDriver dan koneksi internet

### 2. `pipeline_cv_data_cleaning.ipynb`
- **Tujuan**: Membersihkan dan menormalisasi dataset CV kandidat
- **Input**: 
  - `dataset_mentah/dataset_tambahan_cv.xlsx`
  - `dataset_mentah/hasil_cv_kaggle_it_ocr.xlsx`
- **Output**: `dataset_clean/dataset_cv.xlsx`
- **Proses**:
  - Pembersihan teks OCR
  - Normalisasi kolom `detail` menggunakan Groq LLM (batch processing + checkpoint)
  - Standarisasi skill dengan `kamus/kamus_skill_cv.csv`
  - Penghapusan duplikasi & nilai kosong

### 3. `pipeline_job_data_cleaning.ipynb`
- **Tujuan**: Membersihkan dan menormalisasi dataset lowongan pekerjaan
- **Input**: Dataset job dari `dataset_mentah/` & Google Drive
- **Output**: `dataset_clean/dataset_job.xlsx`
- **Proses**:
  - Normalisasi kolom `kualifikasi` menggunakan Groq LLM (batch processing + checkpoint)
  - Standarisasi skill dengan `kamus/Kamus_IT_Bersih_Filtered.csv`
  - Kategorisasi level pengalaman (entry/mid/senior)
  - Pembersihan format kolom

### 4. `EDA_data_clean.ipynb`
- **Tujuan**: Eksplorasi mendalam data bersih untuk menghasilkan insight bisnis
- **Input**: Semua dataset dari `dataset_clean/`
- **Output**: Visualisasi, grafik, dan temuan statistik
- **Analisis**:
  - Distribusi pendidikan dan pengalaman kandidat
  - Distribusi level pengalaman yang dicari perusahaan
  - Analisis skill paling dibutuhkan
  - Gap antara profil kandidat vs. kebutuhan lowongan
  - Analisis gaji berdasarkan lokasi dan kategori peran

---

## Cara Menjalankan

### Prasyarat
```bash
pip install pandas numpy jupyter openpyxl selenium groq plotly matplotlib seaborn
```

### Menjalankan Notebook
```bash
jupyter notebook
```
Kemudian buka notebook yang diinginkan dari browser.

### Konfigurasi LLM (untuk pipeline_cv dan pipeline_job)
Siapkan API Key Groq sebelum menjalankan notebook pipeline:
```python
# Di dalam notebook, set API key:
GROQ_API_KEY = "your-api-key-here"
```

Daftar akun dan dapatkan API key gratis di: [console.groq.com](https://console.groq.com)

---

## Dependensi Utama

| Library | Versi | Digunakan Oleh |
|---------|-------|----------------|
| pandas | >=2.0.0 | Semua notebook |
| numpy | >=1.26.0 | Semua notebook |
| openpyxl | >=3.1.0 | Membaca/menulis .xlsx |
| groq | latest | pipeline_cv, pipeline_job |
| selenium | latest | kode_scraping |
| plotly | >=5.18.0 | EDA_data_clean |
| matplotlib | latest | EDA_data_clean |
| seaborn | latest | EDA_data_clean |

---

## File Output

| Notebook | Menghasilkan |
|----------|-------------|
| `kode_scraping.ipynb` | `dataset_mentah/` (data scraping mentah) |
| `pipeline_cv_data_cleaning.ipynb` | `dataset_clean/dataset_cv.xlsx` + checkpoint di `checkpoint_LLM/` |
| `pipeline_job_data_cleaning.ipynb` | `dataset_clean/dataset_job.xlsx` + checkpoint di `checkpoint_LLM/` |
| `EDA_data_clean.ipynb` | Visualisasi & insight (disimpan langsung dari notebook) |

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
