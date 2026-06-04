# checkpoint_LLM — Checkpoint Batch Processing

Folder ini menyimpan **file checkpoint** dari proses preprocessing dan normalisasi berbasis **LLM (Large Language Model)** menggunakan Groq API. Checkpoint digunakan agar proses batch yang panjang dapat dilanjutkan tanpa mengulang dari awal jika terjadi gangguan.

---

## Isi Folder

| File | Deskripsi |
|------|-----------|
| `detail_checkpoint_dataset_cv_ocr.xlsx` | Checkpoint normalisasi kolom `detail` pada dataset CV hasil OCR — menyimpan progres baris yang sudah diproses |
| `detail_checkpoint_dataset_tambahan_cv.xlsx` | Checkpoint normalisasi kolom `detail` pada dataset CV tambahan — menyimpan progres baris yang sudah diproses |
| `kualifikasi_checkpoint.csv` | Checkpoint normalisasi kolom `kualifikasi` pada dataset Job — menyimpan progres baris yang sudah diproses |

---

## Tujuan

File-file checkpoint dibuat untuk:

- **Melanjutkan proses** normalisasi yang sempat terhenti (karena timeout, rate limit API, dll.)
- **Menghindari pemborosan token** LLM dengan tidak memproses ulang baris yang sudah selesai
- **Menjamin konsistensi** hasil normalisasi antara sesi yang berbeda

---

## Alur Penggunaan Checkpoint

```
Dataset Mentah
      ↓
Proses Normalisasi LLM (batch per N baris)
      ↓
  Baris selesai → Disimpan ke file checkpoint
      ↓
[Jika terjadi gangguan] → Lanjutkan dari baris terakhir di checkpoint
      ↓
Dataset Ternormalisasi → dataset_clean/
```

---

## Keterkaitan dengan Proses Pipeline

| Checkpoint File | Notebook yang Menggunakan | Output Akhir |
|-----------------|--------------------------|--------------|
| `detail_checkpoint_dataset_cv_ocr.xlsx` | `pipeline_cv_data_cleaning.ipynb` | `dataset_clean/dataset_cv.xlsx` |
| `detail_checkpoint_dataset_tambahan_cv.xlsx` | `pipeline_cv_data_cleaning.ipynb` | `dataset_clean/dataset_cv.xlsx` |
| `kualifikasi_checkpoint.csv` | `pipeline_job_data_cleaning.ipynb` | `dataset_clean/dataset_job.xlsx` |

---

## LLM yang Digunakan

| Detail | Keterangan |
|--------|------------|
| Provider | **Groq** |
| Model | **LLaMA-3.1-8b-Instant** |
| Tujuan | Normalisasi teks bebas (kolom `detail` CV & `kualifikasi` Job) menjadi format terstruktur |
| Mode | Batch processing dengan mekanisme checkpoint |

---

## Catatan Penting

> **Jangan hapus file checkpoint** selama proses normalisasi masih berlangsung. File ini adalah satu-satunya cara untuk melanjutkan proses dari titik yang sudah selesai.

> File checkpoint bersifat **sementara** dan dapat dihapus setelah seluruh normalisasi selesai dan dataset bersih sudah tersimpan di `dataset_clean/`.

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
