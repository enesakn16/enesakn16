# Enes AKIN

E-ticaret operasyonları, finans, stok/depo süreçleri ve motosiklet sektörü için gerçek iş problemlerini çözen yazılımlar geliştiriyorum.

**Odak:** güvenilir iş kuralları · veri doğrulama · otomasyon · test/CI · operasyon yazılımları

[GitHub](https://github.com/enesakn16) · [TÜRKMOPET](https://turkmopet.com) · [Lastik Gezegeni](https://lastikgezegeni.com)

## Current focus

- **Moto Fitment Engine:** doğrulanmış marka/model/yıl → OEM lastik ölçüsü, güvenli alternatif eleme ve katalog sıralama
- **Supplier Price Watch:** tedarikçi fiyat değişimi, SKU kimliği ve marj riski; `v0.2.0` kod tabanı hazır, GitHub release/tag henüz yayınlanmadı
- **Portfolio reliability:** çalışan test/CI, sentetik public fixture'lar ve açık demo/production sınırları

[Kasım 2026 portföy yol haritası](ROADMAP-2026-11.md) · [Ekim arşivi](ROADMAP-2026-10.md)

## Featured projects

| Project | Purpose | Status |
| --- | --- | --- |
| [**cari-360**](https://github.com/enesakn16/cari-360) | Sentetik veriyle çalışan güvenli offline cari/finans demo uygulaması ve yaşlandırma raporu | Tested · CI |
| [**moto-fitment-engine**](https://github.com/enesakn16/moto-fitment-engine) | Marka/model/yıl → doğrulanmış OEM lastik ölçüsü; fail-closed alternatif eleme ve katalog sıralama | Working CLI/API · Tested · CI |
| [**supplier-price-watch**](https://github.com/enesakn16/supplier-price-watch) | CSV/XLSX tedarikçi listelerini karşılaştırır; fiyat değişimi, SKU kimliği ve marj riski üretir | v0.2.0 codebase · Tested · CI · Release pending |
| [**turkmopet-warehouse-ops**](https://github.com/enesakn16/turkmopet-warehouse-ops) | Stok mutabakatı, veri kalitesi, görev yaşam döngüsü, SLA ve eskalasyon | Tested · CI |
| [**turkmopet-marketplace-intelligence**](https://github.com/enesakn16/turkmopet-marketplace-intelligence) | Pazaryeri maliyetlerini ortak modele çevirip katkı kârı ve risk analizi üretir | Tested · CI |
| [**turkmopet-b2b-growth-suite**](https://github.com/enesakn16/turkmopet-b2b-growth-suite) | B2B müşteri puanlama, satış aksiyonları, görev ve audit akışı | Tested · CI |

## Building next

- [**bmi-hesaplama-mobile-app**](https://github.com/enesakn16/bmi-hesaplama-mobile-app) — Kotlin/Jetpack Compose Android uygulaması; açık PR doğrulanıp temiz biçimde merge edilmeden flagship kabul edilmiyor.
- [**turkmopet-seo-content-engine**](https://github.com/enesakn16/turkmopet-seo-content-engine) — katalog SEO denetimi ve Search Console önceliklendirmesi; ürünleşme ve dış kullanıcı değeri güçlendirilecek.

## Stack

**Python · SQLite · Git · GitHub Actions**  
Android tarafında: **Kotlin / Jetpack Compose**

## Engineering principles

- Finansal hesaplarda deterministik kurallar ve gerektiğinde `Decimal`
- Belirsiz eşleşmelerde tahmin yerine fail-closed davranış
- Gerçek ticari verileri public repolara koymama; sentetik fixture kullanma
- Değişiklikleri test + CI ile doğrulama
- Demo ile production sınırını README içinde açık tutma

> Gerçek problem → sade mimari → test → CI → kullanılabilir ürün