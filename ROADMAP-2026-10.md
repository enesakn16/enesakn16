# Ekim 2026 Portföy Yol Haritası

**Durum tarihi: 1 Ekim 2026**

Bu ayın amacı yeni repository sayısını artırmak değil; üç profesyonel projeyi doğrulanabilir ürün seviyesine taşımaktır. Çalışma ritmi 3–5 günlük odak bloklarıdır. Çoklu commit ancak gerçek uygulama, test, refactor, dokümantasyon veya release işi bunu gerektiriyorsa yapılır.

## Eylül değerlendirmesi

### Gerçekten teslim edilenler

- [`moto-fitment-engine`](https://github.com/enesakn16/moto-fitment-engine) install edilebilir CLI, sentetik katalog fixture'ı, MIT lisansı ve release öncesi CLI/quick-start kontrolleri kazandı. 30 Eylül'deki son `main` CI çalışması başarılıdır: [Actions #36681530552](https://github.com/enesakn16/moto-fitment-engine/actions/runs/36681530552).
- [`supplier-price-watch`](https://github.com/enesakn16/supplier-price-watch) kontrollü SKU kimlik eşlemesi, GTIN doğrulama, çözülemeyen kimliklerde fail-closed davranış ve satın alma odaklı XLSX çıktısı kazandı. 27 Eylül'deki son CI çalışması başarılıdır: [Actions #36329572864](https://github.com/enesakn16/supplier-price-watch/actions/runs/36329572864).
- Profil README'si kişisel/davetiye projelerini Featured Projects dışında tutuyor ve yalnız test/CI ile desteklenen iş projelerini öne çıkarıyor.

### Doğrulanamayan veya tamamlanmayanlar

- Moto Fitment için GitHub tag/release yok; `CHANGELOG.md` hâlâ `Unreleased - 0.1.0` durumunda. Hosted API veya public demo yok.
- Supplier Price Watch kodu `0.2.0`, ancak GitHub tag/release yok. Public demo veya Pages sitesi yok.
- [`bmi-hesaplama-mobile-app`](https://github.com/enesakn16/bmi-hesaplama-mobile-app) `main` dalında çalıştırılabilir Android kaynak kodu yok. [PR #1](https://github.com/enesakn16/bmi-hesaplama-mobile-app/pull/1) taslak, 32 commitlik, merge çatışmalı (`dirty`) ve son head commit için Actions çalışması görünmüyor. Release/APK yok.
- İncelenen amiral gemilerde repository description, topics ve homepage alanları boş; bunlar kod kalitesi değil ama ilk izlenim ve keşfedilebilirlik borcudur.
- İncelenen public repoların hiçbirinde doğrulanmış GitHub Pages canlı demosu yok. Bu nedenle bu yol haritası hiçbir projeyi bugün “live” olarak tanımlamaz.

### Devam / bakım / arşiv kararı

- **Aktif:** BMI Android, Moto Fitment Engine, Supplier Price Watch.
- **Bakım modu:** `cari-360`, Warehouse Ops, Marketplace Intelligence, B2B Growth Suite, SEO Content Engine ve `muhasebe-program`; yalnız kırık CI, güvenlik, veri bütünlüğü veya açıkça yanlış doküman düzeltmeleri.
- **Vitrin dışı:** `Enes-Nevra-Davetiye`, `hatice-enes`, `hatice-gelecekten-gelen-kargo` ve benzeri kişisel/davetiye projeleri Featured Projects ve önerilen pin setine alınmayacak.
- **Arşiv adayı:** Android kodu kanonik BMI reposuna güvenli biçimde taşınıp geçmiş/attribution korunduktan sonra yanlış isimli eski repo arşivlenebilir. Taşıma doğrulanmadan arşivleme yapılmayacak.

## Ekim hedefleri

1. Tek kanonik repoda, yeşil CI'lı ve indirilebilir APK artifact'lı Kotlin/Compose uygulaması.
2. Moto Fitment Engine `v0.1.0`: doğrulanmış release commit'i, wheel/sdist, CLI smoke testi ve ince bir HTTP adapter sınırı.
3. Supplier Price Watch `v0.2.0`: doğrulanmış release ve sentetik veriden otomatik üretilen, etkileşimli statik ürün demosu.
4. Ay sonunda profil iddialarının release, CI ve demo URL'leriyle birebir doğrulanması.

---

## 1–8 Ekim — Kotlin Android: kanonik BMI uygulaması

**Repository:** https://github.com/enesakn16/bmi-hesaplama-mobile-app

### Problem ve hedef kullanıcı

Kullanıcının boy/kilo girdisinden BMI ve sağlıklı kilo aralığı üreten, erişilebilir ve açıkça “bilgilendirme amaçlı” bir Android uygulaması. Hedef kullanıcı, hızlı ve çevrimdışı çalışan sade bir hesaplayıcı isteyen genel kullanıcıdır; uygulama tıbbi teşhis iddiası taşımamalıdır.

### Mimari hedef

- Kotlin + Jetpack Compose UI.
- Tek yönlü veri akışı; ekran seviyesinde `ViewModel` ve tek `UiState`.
- Saf Kotlin doğrulama/hesaplama domain katmanı.
- UI ile hesaplama kuralları arasında açık sınır; küçük uygulama için gereksiz katman/Hilt eklenmemesi.
- Düz metin parola, sahte authentication, gereksiz bildirim veya kişisel veri saklama olmaması.

### 1–4 Ekim: çatışmayı çöz ve kanonikleştir

- PR #1'in diff'ini ve kaynak geçmişini koruyarak `main` ile çatışmayı çöz; otomatik merge yapma.
- Eski yanlış isimli repodan gerekli kaynakları seçerek kanonik repoya taşı; kişisel içerik veya alakasız geçmiş taşınmasın.
- Gradle wrapper, AGP, Kotlin ve Compose sürümlerini yalnız mevcut build gerçekten gerektiriyorsa yükselt; aynı anda geniş framework migration yapma.
- Repository description/topics ve MIT lisansını gerçek ürün durumuyla uyumlu hâle getir.

### 5–8 Ekim: test, erişilebilirlik ve artifact

- BMI eşik değerleri, sağlıklı kilo aralığı ve invalid input için JVM unit testleri.
- `ViewModel` durum geçişleri için unit testleri; mümkünse fakes kullan.
- Compose semantics, klavye Next/Done akışı ve ana happy path için instrumentation testleri.
- PR ve `main` üzerinde unit test + lint + debug APK build + emulator test workflow'u.
- Release commit'inden üretilen APK'yı Actions artifact olarak sakla; artifact indirilebilirliği doğrulanmadan release iddiası yapma.
- README üst bölümüne problem, veri akışı, test komutları ve 3 güncel ekran görüntüsü ekle.

### Teslimat ve release kriteri

- PR mergeable ve review edilebilir; çatışma yok.
- `main` üzerinde unit, lint, build ve instrumentation işleri yeşil.
- Aynı SHA'dan üretilmiş APK artifact doğrulanmış.
- README ve release notes gerçek ekran görüntüleri içeriyor.
- İlk GitHub Release yalnız yukarıdaki kapılar geçilirse yayımlanır; aksi halde repo “in development” kalır.

### Mülakat anlatısı

- UDF/UiState yaklaşımının Compose ekranını domain kurallarından nasıl ayırdığı.
- JVM testi ile emulator/instrumentation testinin farklı riskleri nasıl yakaladığı.
- Erişilebilirlik semantics'inin hem kullanıcı hem otomasyon açısından neden davranış sözleşmesi olduğu.

---

## 9–16 Ekim — Python backend: Moto Fitment Engine `v0.1.0`

**Repository:** https://github.com/enesakn16/moto-fitment-engine

### Problem ve hedef kullanıcı

Motosiklet marka + model + yıl girdisini kaynak izi olan OEM lastik ölçüsüyle eşleştirmek; tedarikçi kataloğundaki adayları belirsizlikte tahmin yürütmeden elemek ve sıralamak. Hedef kullanıcılar parça e-ticaret ekipleri, katalog yöneticileri, servisler ve entegrasyon geliştiricileridir.

### Mimari hedef

- Mevcut dependency-light Python domain core tek doğruluk kaynağı olarak kalır.
- HTTP katmanı domain kurallarını kopyalamayan ince bir FastAPI adapter olur ve isteğe bağlı dependency extra olarak paketlenir.
- Endpoint'ler: `/health`, doğrulanmış fitment lookup ve katalog screening.
- Yanıtlar provenance, verification date, ret nedenleri ve güvenlik sınırını açıkça taşır.
- OpenAPI/Swagger yalnız etkileşimli API yüzeyidir; veri kapsamı eksikken “tam fitment kataloğu” pazarlaması yapılmaz.

### 9–12 Ekim: gerçek release kapısı

- `CHANGELOG.md` başlığını release tarihine dönüştür ve bilinen sınırlamaları koru.
- Wheel + sdist build, metadata kontrolü, temiz sanal ortam install ve gerçek `moto-fitment --help`/PCX sentetik akış smoke testi çalıştır.
- Git tag ile `pyproject.toml` sürümünün eşleşmesini CI'da zorunlu kıl.
- Sadece release commit'i yeşilse `v0.1.0` GitHub Release yayımla; wheel/sdist ve checksum ekle.
- Repository description/topics ayarla; homepage ancak gerçek URL varsa eklenir.

### 13–16 Ekim: testli HTTP adapter

- Domain fonksiyonlarına delegasyon yapan request/response modelleri ekle.
- Bulunamayan, belirsiz ve geçersiz inputları ayrı hata sözleşmeleriyle döndür.
- FastAPI `TestClient` ile başarılı lookup, 404/no-match, invalid payload ve safety/provenance alanlarını test et.
- CI'da API dependency extra kurulumu ve OpenAPI schema smoke testi çalıştır.
- README'ye `curl` örnekleri, mimari akış ve yerel çalıştırma komutu ekle.

### Teslimat ve release kriteri

- `v0.1.0` release URL'si ve artifact'ları doğrulanmış.
- CLI geriye dönük çalışıyor; API aynı domain core'u kullanıyor.
- Testler Python 3.11 ve 3.13'te yeşil.
- Bilinmeyen/çelişkili fitment “no match”; fuzzy tahmin yok.
- Hosted servis kurulmadıysa profil yalnız “tested local API” der, “live API” demez.

### Mülakat anlatısı

- Fail-closed matching'in satış hızından önce veri güvenliğini koruması.
- Provenance'ın neden yalnız URL alanı değil, veri sözleşmesi olduğu.
- Transport adapter ile domain core ayrımının CLI ve HTTP'yi aynı kurallarda tutması.

---

## 17–28 Ekim — Procurement + etkileşimli web: Supplier Price Watch `v0.2.0`

**Repository:** https://github.com/enesakn16/supplier-price-watch

### Problem ve hedef kullanıcı

Tedarikçi dosyalarını deterministik kimlikle karşılaştırmak, maliyet/katalog değişimini ve marj riskini satın alma ekibine karar verilebilir biçimde göstermek. Hedef kullanıcılar satın alma, fiyatlama, kategori yönetimi ve e-ticaret operasyon ekipleridir.

### Mimari hedef

- Mevcut strict CSV/XLSX ingestion + identity registry + `Decimal` domain katmanı korunur.
- Statik demo üreticisi, domain çıktısından JSON ve erişilebilir HTML oluşturur; finans kuralları JavaScript'te yeniden yazılmaz.
- Tarayıcı tarafı yalnız filtreleme, sıralama, özet kartları ve satır detayı sunar.
- Demo yalnız sentetik fixture içerir; gerçek tedarikçi fiyatı, SKU eşleme dosyası veya ticari veri yayınlanmaz.

### 17–20 Ekim: `v0.2.0` release

- `CHANGELOG.md` içindeki `Unreleased - 0.2.0` başlığını release tarihine çevir.
- Wheel/sdist, Twine metadata, temiz ortam install, iki CLI entry point ve sentetik tam akış smoke testlerini release workflow'da doğrula.
- Satın alma XLSX çıktısını açıp sheet adları, filtre, frozen header, risk sırası ve atomik yazma testlerini doğrula.
- Yeşil release commit'inden `v0.2.0` GitHub Release üret; artifact ve checksum ekle.

### 21–24 Ekim: etkileşimli statik demo

- Versioned sentetik önce/sonra fiyat listesi + sales catalog + identity map senaryosu oluştur.
- Mevcut domain sonucundan deterministic `demo/report.json` ve `demo/index.html` üret.
- UI: artan/azalan maliyet, added/removed SKU, `OK/WARNING/CRITICAL`, çözülemeyen kimlik ve currency filtresi.
- Klavye ile kullanılabilir tablo, görünür focus, anlamlı başlıklar ve renk dışında risk etiketi sağla.
- Snapshot/golden test ile demo çıktısının şemasını; unit test ile filtre/sıralama helper'larını doğrula.

### 25–28 Ekim: otomatik Pages teslimatı ve sunum

- CI önce test/build çalıştırır, sonra yalnız `main` için sentetik demo artifact'ını GitHub Pages'e deploy eder.
- GitHub'ın resmi akışındaki `upload-pages-artifact` + `deploy-pages` yaklaşımını kullan; elle “Run workflow” zorunluluğu oluşturma.
- README'ye gerçek ekran görüntüleri, 60 saniyelik quick-start ve demo veri sınırını ekle.
- URL dışarıdan 200 dönüp filtreler çalışmadan profile “Live demo” ekleme.

### Tek seferlik manuel işlem

Connector repository ayarlarında Pages kaynağını değiştiremiyorsa Enes'in bir kez **Settings → Pages → Build and deployment → Source: GitHub Actions** seçmesi gerekir. Bu yapılana kadar deployment “bekliyor” sayılır; canlı teslim edilmiş sayılmaz.

### Teslimat ve release kriteri

- `v0.2.0` release ve artifact URL'leri doğrulanmış.
- Sentetik uçtan uca senaryo CLI, CSV/XLSX ve web raporunda aynı risk sonucunu üretiyor.
- Demo build'i deterministic ve CI tarafından yeniden üretilebilir.
- Pages workflow push ile otomatik; manuel publish adımı yok.
- Public URL, erişilebilirlik temel kontrolleri ve hassas veri yokluğu doğrulanmış.

### Mülakat anlatısı

- Neden ürün kimliği `supplier + canonical SKU + currency` sözleşmesine bağlı ve fuzzy isim eşlemesi değil.
- Finansal hesaplarda `Decimal`, dosya tesliminde atomic replace ve kimlikte fail-closed tasarımın veri bütünlüğü etkisi.
- Domain sonucunu statik web artefactına dönüştürmenin aynı iş kurallarını iki yerde yazmayı nasıl önlediği.

---

## 29–31 Ekim — doğrulama ve portföy konsolidasyonu

- Üç projenin `main` CI, release, artifact ve varsa demo URL'lerini temiz tarayıcı oturumundan kontrol et.
- Profile yalnız doğrulanmış durumları yaz: “Release”, “APK”, “Live demo” ve “API” kelimeleri doğrudan kanıta bağlanmalı.
- README ekran görüntülerinin güncel UI/çıktıyla eşleştiğini kontrol et.
- Boş description/topics alanlarını gerçek teknoloji ve problem alanıyla doldur; rozet kalabalığı oluşturma.
- `cari-360` MIT lisans metninin GitHub tarafından tanınmama nedenini ayrı, küçük bir bakım işi olarak incele; lisans sahibinin hukuki tercihini varsayarak değiştirme.
- Açık kişisel repo PR'larını portföy faaliyeti olarak sayma; otomatik merge yapma.
- Başarısız release kapısını takvim uğruna atlama. Bitmeyen işi Kasım'a tek, açık blocker ile taşı.

## Otomatik CI ve dependency politikası

- Tüm amiral gemilerde push/PR testleri otomatik; release workflow'u tag veya release olayıyla deterministik çalışmalı.
- Dependency yükseltmeleri ayrı PR'da test edilmeli; alakasız major upgrade'ler tek pakette birleştirilmemeli.
- Android dependency yükseltmesi ürün işinden ayrı tutulmalı; Python paketlerinde build/install smoke testi zorunlu kalmalı.
- Secret gerektiren entegrasyon, secret sağlanmadan “teslim edildi” sayılmaz.

## Ay sonu ölçülebilir başarı kartı

- [ ] 1 kanonik Android repo; çatışmasız `main`, yeşil CI ve doğrulanmış APK artifact.
- [ ] Moto Fitment Engine `v0.1.0` GitHub Release; wheel/sdist + checksum + tested CLI.
- [ ] Moto Fitment için domain core'u kopyalamayan testli HTTP adapter.
- [ ] Supplier Price Watch `v0.2.0` GitHub Release; iki CLI entry point smoke-tested.
- [ ] Sentetik verili, otomatik üretilen Supplier Price Watch web demo; canlı URL yalnız doğrulandıysa profile eklenmiş.
- [ ] En az iki amiral gemide güncel ekran görüntüsü.
- [ ] Üç amiral gemide description/topics ve gerçeğe uygun README üst bölümü.
- [ ] Yeni boş repo, sahte commit, backdate, rozet sayısı odaklı değişiklik veya doğrulanmamış canlılık iddiası yok.

## Başvurulan güncel resmi rehberler

- Android architecture recommendations: https://developer.android.com/topic/architecture/recommendations
- Compose UI testing: https://developer.android.com/develop/ui/compose/testing
- FastAPI testing: https://fastapi.tiangolo.com/tutorial/testing/
- Python Packaging User Guide: https://packaging.python.org/en/latest/tutorials/packaging-projects/
- GitHub Pages publishing source and Actions deployment: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

Bu plan “çıktı kanıtı” prensibiyle yürütülür: bir özellik ancak test/CI ile; release ancak tag/artifact ile; demo ancak erişilebilir URL ile tamamlanmış sayılır.
