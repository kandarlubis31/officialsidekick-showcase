# 🛍️ Sidekick Thrift — Toko Online Thrift dengan Scraper Instagram

<div align="center">

**Live di [sidekick.web.id](https://sidekick.web.id) — jual-beli pakaian bekas, dari post Instagram jadi katalog siap beli.**

[![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20)](https://laravel.com)
[![Live](https://img.shields.io/badge/🟢-sidekick.web.id-brightgreen)](https://sidekick.web.id)
[![PayPal](https://img.shields.io/badge/checkout-PayPal-003087)]()
[![WebP](https://img.shields.io/badge/gambar-otomatis%20WebP-4A827B)]()

</div>

<div align="center">
<img src="screenshots/desktop.png" alt="Sidekick Thrift — katalog produk" width="800" />
</div>

---

## ❌ Masalahnya

- Thrift seller jualan via **Instagram** — katalog nggak rapi, pembeli harus scroll, DM manual, borong-beres
- Upload foto produk satu-satu + resize manual itu **capek**
- Pembayaran online untuk barang second sering tidak ada — CMIIW, transfer manual & titip air mata kalau pembeli hilang

## ✅ Sidekick Thrift

Toko online thrift berbasis **Laravel 12**: katalog publik yang rapi, admin panel yang produktif, dan **checkout PayPal yang otomatis menandai barang terjual**.

### ✨ Fitur

- 🛒 **Katalog Livewire** — pencarian + filter (kategori, harga, kondisi, size) + sorting + pagination, tanpa reload
- 📄 **Detail produk** — ukuran (LD/PB/LB/LP + stok), produk terkait satu kategori
- 📸 **Instagram scraper** ⭐ — tempel link post/reel IG → gambar ter-scrape jadi foto produk (workflow admin paling disayang)
- 🖼️ **Optimasi gambar otomatis** — upload banyak sekaligus → resize 800px → **WebP kualitas 80%** (hemat bandwidth puluhan persen)
- 💳 **Checkout PayPal** — direct purchase, order dibuat → capture sukses → produk **otomatis `is_sold`**
- 🔐 **Auth Jetstream** — register/login, verifikasi email, 2FA
- 🛠️ **Admin panel** — CRUD produk & kategori, toggle terjual, hapus foto per produk, dashboard statistik

---

## 🏗️ Arsitektur

```mermaid
flowchart LR
    subgraph FE["🌐 Publik (Blade + Livewire + Tailwind)"]
        K["Katalog / detail / kategori"]
        CO["Checkout /buy/{slug}"]
    end
    subgraph ADM["🛠️ Admin Panel"]
        CRUD["CRUD produk + kategori"]
        IG["Instagram scraper"]
        UP["Bulk upload foto"]
    end
    subgraph BE["⚙️ Laravel 12"]
        LW["Livewire ProductCatalog"]
        PC["ProductController"]
        IM["Intervention Image → WebP"]
        PP["PaymentController<br/>PayPal REST"]
        AUTH["Jetstream · Fortify · Sanctum"]
    end
    DB[("🗄️ DB<br/>users · products · categories<br/>images · sizes")]
    PPAL["💳 PayPal API"]
    IGAPI["📸 Instagram"]
    ADM --> IG & UP & CRUD
    IG --> IGAPI
    UP & IG --> IM --> DB
    CRUD --> DB
    FE --> LW & PC & CO
    LW & PC --> DB
    CO --> PP <--> PPAL
    PP -->|"capture sukses → is_sold"| DB
    AUTH --- BE
```

- **Stack:** Laravel 12 (PHP 8.2+) · Livewire 3 · Tailwind + Vite · Jetstream 5 · Spatie Media Library 11 · Intervention Image v3 · PayPal REST API
- **Produksi:** live di [sidekick.web.id](https://sidekick.web.id) — versi produksi di-manage via server (commit `30a7b21`: order system + hardening)

---

## 🔒 Tentang Source Code

Repository ini adalah **showcase** — dokumentasi produk, bukan kode sumber.
Source code Sidekick Thrift tidak dipublikasikan dan semua hak dilindungi. Lihat [`LICENSE`](LICENSE).

> 💬 Demo, kolaborasi, atau lisensi? Hubungi [Kandar Lubis](https://github.com/kandarlubis31).

---

© 2026 Kandar Lubis — All Rights Reserved.
