# kamus — Kamus Standarisasi Skill IT

Folder ini menyimpan **file kamus (dictionary)** yang digunakan untuk standarisasi dan normalisasi nama skill dalam proses pembersihan data pada proyek **ITCareerMatch**.

---

## Isi Folder

| File | Ukuran | Digunakan Untuk | Jumlah Entri |
|------|--------|-----------------|--------------|
| `Kamus_IT_Bersih_Filtered.csv` | ~1.7 MB | Standarisasi skill pada **dataset Job** | Ribuan entri terminologi IT |
| `kamus_skill_cv.csv` | ~20 KB | Standarisasi skill pada **dataset CV** | Ratusan entri skill CV |

---

## Tujuan

Kamus ini digunakan untuk:

- **Menyeragamkan ejaan** skill yang berbeda-beda (contoh: `JavaScript` = `JS` = `Java Script`)
- **Menghilangkan sinonim** agar tidak ada duplikasi konsep yang sama
- **Mapping terminologi** dari teks bebas ke nama skill yang baku
- **Meningkatkan akurasi** pencocokan kandidat dengan lowongan (job matching)

---

## Perbedaan Kedua Kamus

| Aspek | `kamus_skill_cv.csv` | `Kamus_IT_Bersih_Filtered.csv` |
|-------|----------------------|-------------------------------|
| **Target Data** | Dataset CV kandidat | Dataset lowongan kerja (Job) |
| **Ukuran** | Lebih kecil (~20 KB) | Lebih besar (~1.7 MB) |
| **Fokus** | Skill umum yang sering muncul di CV | Terminologi IT komprehensif dari perspektif perusahaan |
| **Dipakai di** | `pipeline_cv_data_cleaning.ipynb` | `pipeline_job_data_cleaning.ipynb` |

---

## Format File

### `kamus_skill_cv.csv`
```
raw_skill, standar_skill
"js", "JavaScript"
"python3", "Python"
"ml", "Machine Learning"
...
```

### `Kamus_IT_Bersih_Filtered.csv`
File ini berisi daftar terminologi IT yang sudah difilter dan dibersihkan, digunakan sebagai referensi untuk normalisasi skill pada data lowongan.

---

## Alur Penggunaan dalam Pipeline

```
Teks Skill Mentah (dari CV / Job)
           ↓
  Lookup di Kamus (fuzzy / exact match)
           ↓
  Skill Terstandarisasi
           ↓
  Dataset Bersih (dataset_clean/)
```

---

## Keterkaitan dengan Modul Lain

| Kamus | Notebook | Output |
|-------|----------|--------|
| `kamus_skill_cv.csv` | `notebook/pipeline_cv_data_cleaning.ipynb` | `dataset_clean/dataset_cv.xlsx` |
| `Kamus_IT_Bersih_Filtered.csv` | `notebook/pipeline_job_data_cleaning.ipynb` | `dataset_clean/dataset_job.xlsx` |

---

## Cara Memperbarui Kamus

Jika menemukan skill yang belum terdaftar atau perlu penambahan:

1. Buka file kamus yang relevan (`.csv`) menggunakan Excel atau editor teks
2. Tambahkan baris baru dengan format: `raw_skill, standar_skill`
3. Simpan file dan jalankan ulang notebook pipeline yang sesuai
4. Verifikasi hasil standarisasi pada dataset output

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
