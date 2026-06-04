# AB Testing — ITCareerMatch

Folder ini berisi notebook eksperimen **A/B Testing** yang digunakan untuk mengevaluasi performa sistem rekomendasi karier IT pada proyek **ITCareerMatch**.

---

## Isi Folder

| File | Deskripsi |
|------|-----------| 
| `ITCareerMatch_AB_Testing (2).ipynb` | Notebook utama A/B Testing untuk membandingkan performa dua varian sistem pencocokan kandidat dengan lowongan pekerjaan |

---

## Tujuan A/B Testing

A/B Testing dilakukan untuk:

- **Membandingkan dua pendekatan** sistem *job matching* (Varian A vs Varian B)
- **Mengukur performa** berdasarkan metrik relevansi rekomendasi
- **Memvalidasi secara statistik** pendekatan mana yang menghasilkan pencocokan lebih baik antara profil CV kandidat dengan lowongan pekerjaan IT

---

## Metodologi

```
Kandidat & Lowongan
       ↓
  Varian A ──────────────────┐
  (Metode Pencocokan A)      ├── Evaluasi & Perbandingan Statistik
  Varian B ──────────────────┘
  (Metode Pencocokan B)
       ↓
  Kesimpulan & Rekomendasi
```

### Metrik Evaluasi
- **Precision / Recall** — Relevansi hasil pencocokan
- **Uji Statistik** — Signifikansi perbedaan antar varian
- **Distribusi Skor** — Analisis skor kecocokan kandidat–lowongan

---

## Cara Menjalankan

1. Pastikan dependensi sudah terinstal:

   ```bash
   pip install pandas numpy scipy matplotlib seaborn jupyter
   ```

2. Buka notebook:

   ```bash
   jupyter notebook "ITCareerMatch_AB_Testing (2).ipynb"
   ```

3. Jalankan seluruh sel secara berurutan (`Run All`)

---

## Prasyarat

| Kebutuhan | Detail |
|-----------|--------|
| Python | 3.8+ |
| Dataset | `dataset_clean/` harus tersedia di root proyek |
| Library | pandas, numpy, scipy, matplotlib, seaborn |

---

## Keterkaitan dengan Modul Lain

- **Input**: Dataset bersih dari `../dataset_clean/`
- **Output**: Insight statistik untuk pengambilan keputusan arsitektur sistem matching
- **Relevan dengan**: `../notebook/EDA_data_clean.ipynb` untuk konteks eksplorasi data

---

*Bagian dari pipeline proyek **ITCareerMatch** — DBS Foundation Coding Camp 2026*
