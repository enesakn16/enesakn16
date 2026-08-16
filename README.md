# Enes AKIN

E-ticaret operasyonları, finans, stok/depo süreçleri ve motosiklet sektörü için gerçek iş problemlerini çözen yazılımlar geliştiriyorum.

**Odak:** güvenilir iş kuralları · veri doğrulama · otomasyon · test/CI · operasyon yazılımları

[GitHub](https://github.com/enesakn16) · [TÜRKMOPET](https://turkmopet.com) · [Lastik Gezegeni](https://lastikgezegeni.com)

## Featured projects

| Project | Purpose | Status |
| --- | --- | --- |
| [**cari-360**](https://github.com/enesakn16/cari-360) | Sentetik veriyle çalışan, güvenli offline cari/finans demo uygulaması ve yaşlandırma raporu | Tested · CI |
| [**turkmopet-warehouse-ops**](https://github.com/enesakn16/turkmopet-warehouse-ops) | Stok mutabakatı, veri kalitesi, görev yaşam döngüsü, SLA ve eskalasyon | Tested · CI |
| [**turkmopet-marketplace-intelligence**](https://github.com/enesakn16/turkmopet-marketplace-intelligence) | Pazaryeri maliyetlerini ortak modele çevirip katkı kârı ve risk analizi üretir | Tested · CI |
| [**turkmopet-b2b-growth-suite**](https://github.com/enesakn16/turkmopet-b2b-growth-suite) | B2B müşteri puanlama, satış aksiyonları, görev ve audit akışı | Tested · CI |
| [**turkmopet-seo-content-engine**](https://github.com/enesakn16/turkmopet-seo-content-engine) | Katalog SEO denetimi, Search Console önceliklendirmesi ve içerik çakışması analizi | Tested · CI |
| [**muhasebe-program**](https://github.com/enesakn16/muhasebe-program) | Muhasebe/finans iş akışları için doğrulama ve güvenli demo katmanları | Active |

## Building next

- [**supplier-price-watch**](https://github.com/enesakn16/supplier-price-watch) — CSV/XLSX tedarikçi listelerini karşılaştıran, fiyat değişimi ve marj riskini çıkaran testli Python aracı. Çalışan CLI ve CI mevcut; ilk public release öncesi ürün kimliği eşleştirme ve dokümantasyon tamamlanıyor.
- [**moto-fitment-engine**](https://github.com/enesakn16/moto-fitment-engine) — marka/model/yıl → OEM/alternatif lastik-parça eşleştirme motoru. Test ve CI mevcut; doğrulanabilir üretici kaynaklı fitment veri katmanı tamamlanmadan production-ready kabul edilmiyor.

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
