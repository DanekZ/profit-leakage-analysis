# Data

Dataset: **E-Commerce Sales & Customer Analytics** (5 file CSV).
Sumber: _[isi tautan/sumber dataset dan lisensinya]_

## File

| File | Granularitas | Baris | Peran |
|---|---|---|---|
| `ecommerce_sales_customer_analytics_150k.csv` | 1 baris = 1 order | 138.116 | Tabel utama (agregat per order), **source of truth** |
| `order_items.csv` | 1 baris = 1 produk dalam 1 order | 397.569 | Detail item, dipakai untuk breakdown kategori |
| `product_catalog.csv` | 1 baris = 1 produk | 1.175 | Master kategori & brand |
| `customer_master.csv` | 1 baris = 1 customer | 25.000 | Master demografi customer |
| `dataset_statistics.csv` | ringkasan | 1 | Angka resmi untuk validasi |

## Relasi

```
order_items.order_id   → ecommerce_sales_customer_analytics_150k.order_id
order_items.product_id → product_catalog.product_id
ecommerce_sales_customer_analytics_150k.customer_id → customer_master.customer_id
```

## Struktur folder

- `raw/`: taruh 5 file asli di sini. **Tidak di-commit** (file terbesar ±49 MB) karena batas GitHub dan agar repo ringan.
- `sample/`: sampel acak 1.000 order (`random_state=42`) beserta item dan customer terkait, plus `product_catalog.csv` dan `dataset_statistics.csv` lengkap. Untuk demo/uji notebook; **angka hasilnya tidak sama** dengan laporan.
- `processed/`: output notebook (`orders_prepped.csv`, `items_prepped.csv`). Tidak di-commit.

Kamus kolom: [`../docs/data_dictionary.md`](../docs/data_dictionary.md)
