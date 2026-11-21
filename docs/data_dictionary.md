# Data Dictionary

## Tabel utama: `ecommerce_sales_customer_analytics_150k.csv` (46 kolom)

| Kelompok | Kolom |
|---|---|
| Order | `order_id`, `order_date`, `order_time`, `order_status` (Completed / Returned / Cancelled / Pending), `sales_channel` |
| Customer | `customer_id`, `customer_name`, `customer_age`, `gender`, `customer_segment`, `customer_type`, `is_repeat_customer`, `customer_order_count`, `customer_lifetime_value` |
| Lokasi | `customer_city`, `customer_state`, `customer_country`, `region`, `customer_postal_code` |
| Pembayaran | `payment_method`, `payment_status`, `currency` |
| Pengiriman | `shipping_method`, `warehouse`, `delivery_days`, `estimated_delivery_days`, `delivery_status` |
| Retur & ulasan | `return_status`, `return_reason`, `customer_rating`, `review_sentiment`, `customer_review` |
| Marketing | `marketing_channel`, `campaign_name` (kosong ±60% = tanpa campaign), `coupon_code` (kosong ±80% = tanpa kupon), `loyalty_points_earned`, `loyalty_points_redeemed` |
| Finansial | `quantity`, `gross_sales`, `discount_amount`, `tax_amount`, `shipping_cost`, `net_sales`, `product_cost`, `profit`, `profit_margin_percentage` |

Catatan: nilai kosong pada `campaign_name` dan `coupon_code` bukan data rusak, melainkan order tanpa campaign/kupon.

## Kolom turunan (dibuat di notebook)

| Kolom | Definisi |
|---|---|
| `month`, `month_num` | Bulan dari `order_date` (format `YYYY-MM` dan angka 1-12) |
| `season` | `Peak (Nov-Des)` bila bulan 11-12; `Mid-year (Jul)` bila bulan 7; selain itu `Normal` |
| `discount_pct_of_gross` | `discount_amount / gross_sales * 100` |
| `is_loss` | `True` bila `profit < 0` |
| `qty_bucket` | Kelompok quantity: 1-2, 3-4, 5-6, 7-8, 9+ |

## Definisi metrik

| Metrik | Definisi |
|---|---|
| Margin musiman (agregat) | `sum(profit) / sum(net_sales) * 100` |
| Diskon % | `sum(discount_amount) / sum(gross_sales) * 100` |
| Transaksi rugi | order dengan `profit < 0` |
| Scope analisis | `order_status` ∈ {Completed, Returned} |

## Tabel pendukung

- `order_items.csv`: item per order (`order_id`, `product_id`, serta kolom finansial tingkat item).
- `product_catalog.csv`: `product_id`, `product_name`, `product_category`, `product_subcategory`, `brand`, `supplier`, `unit_price`, `product_cost`, `product_rating`.
- `customer_master.csv`: master demografi customer (key: `customer_id`).
- `dataset_statistics.csv`: Total Transactions, Total Columns, Total Customers, Date Range, Total Revenue, Total Profit, Average Order Value, Average Rating, Return Rate, Cancellation Rate.
