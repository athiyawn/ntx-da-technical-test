# Design Notes: Dashboard Kinerja Penjualan

**File:** `dashboard.html` (satu file mandiri, buka langsung di browser; tanpa instalasi, login, atau internet). Screenshot tiap halaman ada di `screenshots/` (PNG + satu PDF gabungan).

## Pengguna
- **Board of Directors:** perlu gambaran kesehatan perusahaan < 5 menit. Halaman 1 *Ringkasan*, tanpa filter.
- **Regional Sales Manager:** perlu membandingkan regionnya dengan region lain dan tahun lalu. Halaman 2 *Detail Region*, dengan filter Region, Channel, Kategori.

## KPI dan alasannya
| KPI | Alasan |
|---|---|
| **Net revenue** | Ukuran yang dipakai tim sales; tetap ada di kartu pertama |
| **Gross profit** dan **Gross margin** | Ukuran apakah pertumbuhan menguntungkan. Revenue +13,4% menutupi gross profit -9,4% |
| **Rata-rata diskon** | Penyebab utama penurunan margin, jadi manajemen bisa melihat sebab, bukan hanya akibat |

Semua KPI selalu ditampilkan **dibanding FY2025** (chip ▲/▼ dan angka tahun lalu). Manager mendapat tambahan tabel perbandingan antar region dan rincian kategori.

**Keputusan atas permintaan Head of Sales:** revenue tetap di posisi pertama, tetapi **sejajar dengan gross profit dan margin dengan ukuran yang sama**, bukan lebih besar sendirian. Alasannya, angka revenue saja akan menampilkan FY2026 sebagai tahun yang bagus padahal profitnya turun.

## Keputusan desain
- **Satu kalimat status** di atas halaman 1 menjawab "bagaimana kita?" sebelum membaca chart.
- Setiap chart punya konteks: garis FY2026 (biru, solid) vs FY2025 (abu, putus-putus). Perubahan memakai panah dan tanda +/- selain warna (merah = memburuk, hijau = membaik).
- Hanya garis, batang naik/turun, dan tabel. Tidak ada pie atau 3D. Maksimal 3 chart + 1 panel sorotan per halaman.
- Tabel perbandingan **tidak memfilter dimensi yang dibandingkan** (tabel region mengabaikan filter Region), sehingga region terpilih selalu terlihat di antara yang lain (baris biru).
- Tanda ⚠ otomatis bila margin turun ≥ 3 poin atau gross profit turun ≥ 15%.
- Semua halaman dihitung dari data tertanam yang sama, jadi total cocok antar halaman (Rp29,69 miliar revenue, Rp3,55 miliar gross profit).

## Persiapan data dan asumsi
- Sumber: hasil cleaning Soal 1 (duplikat, test order, satuan ribuan rupiah, label, tanggal sudah diperbaiki).
- FY = 1 Sep - 31 Agu. **1-15 Sep 2026 tidak dihitung** (bulan belum penuh). 8 order Retail dengan qty tidak wajar (Rp4,0 miliar) dikeluarkan.
- *Cancelled* = 0, *Returned* mengurangi revenue. Cost Networking (~60% baris) adalah estimasi. Region kosong ditampilkan "Tidak diketahui".
- Keterbatasan: file ini **snapshot statis**. Untuk update bulanan, data tertanam perlu dibuat ulang dari hasil cleaning terbaru.

## Lima sorotan (terlihat langsung di dashboard)
1. **Revenue naik, profit turun:** revenue +13,4%, gross profit -9,4%, margin 15,0% → 12,0%, lebih rendah di 12 dari 12 bulan.
2. **Diskon penyebabnya:** rata-rata diskon 4,3% → 7,1%. 575 order berdiskon ≥ 20% (tidak ada di FY2025) menghasilkan Rp3,70 miliar dengan gross profit **-Rp373 juta**.
3. **Masalah ada di Online:** revenue -0,2%, gross profit -55%. Offline: revenue +21,8%, gross profit +15,5%.
4. **Laptop & Smartphone:** 65% revenue tetapi hanya 24% gross profit; gross profit -31% dan -40%.
5. **Jawa Timur (halaman 2, filter Region):** revenue +27,2% tetapi gross profit -32,5%; margin 15,8% → 8,4% dengan diskon 11,1% (rata-rata perusahaan 7,1%). Margin Laptop di region ini 0,7% dan Smartphone 0,0%.
