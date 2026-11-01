# Kasım 2026 — Public GitHub Portfolio Roadmap

**Plan tarihi:** 1 Kasım 2026 · **Dönem:** 1–30 Kasım 2026 · **Durum:** hedefler; tamamlanmış release veya canlı demo iddiası değildir.

## Ekim retrospektifi / 1 Kasım kanıt kontrolü

GitHub bağlantısı üzerinden **13 public repository** listelendi. Profil README hâlâ Ekim yol haritasına bağlanıyor. Kanonik [BMI deposunun](https://github.com/enesakn16/bmi-hesaplama-mobile-app) `main` README'si çalıştırılabilir Android kaynak kodu/APK bulunmadığını söylüyor. [Eski BMI kaynak deposu](https://github.com/enesakn16/Enes-Nevra-Davetiye) ayrı kaldı; açık [güvenlik issue #2](https://github.com/enesakn16/Enes-Nevra-Davetiye/issues/2) ve [bildirim issue #10](https://github.com/enesakn16/Enes-Nevra-Davetiye/issues/10) mevcut. [Moto Fitment](https://github.com/enesakn16/moto-fitment-engine) README'si installable CLI, doğrulanmış OEM kaynakları, fail-closed katalog kuralları ve Python 3.11/3.13 CI tasarımını açıklıyor. [Supplier Price Watch](https://github.com/enesakn16/supplier-price-watch) README'si v0.2.0 kod tabanı olduğunu, GitHub tag/release'in beklediğini belirtiyor. [Warehouse Ops](https://github.com/enesakn16/turkmopet-warehouse-ops) CSV/SQLite stok mutabakatı ve görev akışını belgeler.

**Bu kontrolde:** README'ler, repo görünürlüğü ve son commit SHA'ları okundu; güncel tüm GitHub Actions sonuçları, GitHub Releases varlığı, bağımlılık güvenlik uyarıları ve canlı HTTP demo uçları uçtan uca doğrulanmadı. Dolayısıyla **hiçbir Ekim release'i veya demo yeni doğrulanmış olarak sayılmıyor**. Ekim'den taşınan işler başarısız/eksik doğrulama olarak ele alınır; daha önceki başarılı CI kayıtları yeni SHA'ları kanıtlamaz.

**Devam:** BMI, Moto Fitment, Supplier Price Watch. **Bakım:** Warehouse Ops, Marketplace Intelligence, B2B Growth Suite, SEO Content Engine, Cari 360. **Vitrin dışı / konsolidasyon adayı:** kişisel davetiye depoları ve yanlış isimli eski BMI deposu; kaynak taşıma ve attribution doğrulanmadan arşivleme yok. **Yeni repo açılmayacak.**

## Aylık teslimat kuralları

Her proje 3–5 günlük odak bloklarıyla yürütülür. Commit sayısı hedef değildir; feature, test, CI, refactor, docs/release gibi bağımsız değişiklikler doğal olarak ayrılırsa bir günde birkaç anlamlı commit olabilir. PR ve `main` push'larında otomatik test/lint/build; deploy gerekiyorsa test job'una bağlı otomatik yayın. Release yalnız aynı SHA üzerinde başarılı CI, gerçek artifact ve indirme/smoke kontrolünden sonra. Public veriler sentetik; müşteri, tedarikçi fiyatı ve kimlik bilgisi yayınlanmaz. README: problem, hedef kullanıcı, mimari, local setup, test, demo/screenshot, lisans, changelog, güvenlik sınırı ve **AI-assisted development** notu.

## 1–5 Kasım — Kotlin Android: BMI stabilizasyonu

**Kod:** https://github.com/enesakn16/bmi-hesaplama-mobile-app · **Kaynak geçmişi:** https://github.com/enesakn16/Enes-Nevra-Davetiye · **Hedef artifact:** https://github.com/enesakn16/bmi-hesaplama-mobile-app/releases

**Problem / kullanıcı:** internetsiz, erişilebilir, bilgilendirme amaçlı BMI hesabı isteyen Android kullanıcıları. **Mimari:** Compose → screen ViewModel/UiState → saf Kotlin input evaluator ve calculator; gereksiz DI/Room eklenmeyecek. **İş:** açık PR diff/çatışmasını incele; yalnız Android kaynaklarını kanonik repoya taşı; plaintext credential ve loglamayı kaldır; bildirim gerekmiyorsa özelliği çıkar, gerekiyorsa Android sistem izniyle düzelt; ekran hatalarını ve sonuç metnini birleştir. **Test:** sınır ve lokal sayı formatı JVM testleri, ViewModel durum testleri, Compose UI/instrumentation, Android lint, debug build, emulator smoke. **CI:** PR + `main` push; JDK/AGP/Gradle uyumluluğu mevcut sürümler üzerinden resmi dokümana göre kontrol edilecek. **Çıktı:** 3 gerçek cihaz/emülatör ekran görüntüsü, README kurulum ve güvenlik notu, otomatik APK artifact; tag/release yalnız artifact doğrulanırsa. **Bitti sayılması:** tek kanonik repo; merge conflict yok; main unit+lint+build+UI checks yeşil; APK indirilebilir ve yüklenebilir; açık güvenlik issue'ları giderilmiş veya kapsamı gerekçeli kapatılmış. **Risk:** Actions izin/runner veya emulator eksikse release bloke; manuel Run workflow beklenmez.

## 6–10 Kasım — Python: Moto Fitment Engine API ve paketleme

**Kod:** https://github.com/enesakn16/moto-fitment-engine · **Hedef release:** https://github.com/enesakn16/moto-fitment-engine/releases

**Problem / kullanıcı:** motosiklet yedek parça satıcısı ve servislerin model/yıl bazında OEM lastik ölçüsünü güvenilir bulması. **Mimari:** mevcut saf Python fitment/domain kuralları → küçük FastAPI HTTP adapter; aynı validation tek kaynak, API yalnız transport; verified OEM provenance ve fail-closed korunur. **İş:** `/health`, `/fitments` gibi minimal read-only uçlar, stabil JSON hata şeması, açık kaynak doğrulama notları; Python wheel/sdist ve CLI smoke. **Test:** mevcut domain regression, pytest/TestClient adapter testleri, malformed input/unknown model, packaging/install smoke; ruff/static checks yalnız repo durumuyla uyumlu kontrollü ekleme. **CI:** push/PR test matrisi, package build, artifact; tag sonrası otomatik release yalnız yeşil build ve doğrulanmış dist. **Teslim:** `python -m pip install -e .`, API local `uvicorn` çalıştırma, OpenAPI `/docs` ekran görüntüsü, curl örnekleri; ücretsiz host zorunlu değil, hosted API ancak doğrulanırsa linklenir. **Bitti sayılması:** CLI ile API aynı örnekte tutarlı, negatif senaryolar testli, dağıtım wheel'i kurulabilir, release indirilebilir. **Trade-off:** gerçek onaylı alternatif lastik iddiası yok; geometri elemesi üretici homologasyonu değildir.

## 11–15 Kasım — Web: Supplier Price Watch sentetik interactive demo

**Kod:** https://github.com/enesakn16/supplier-price-watch · **Hedef demo (doğrulanana kadar aday):** https://enesakn16.github.io/supplier-price-watch/ · **Hedef release:** https://github.com/enesakn16/supplier-price-watch/releases

**Problem / kullanıcı:** satın alma ekiplerinin tedarikçi fiyat artışı, SKU alias ve marj riskini hızlı görmesi. **Mimari:** mevcut Python CLI/Decimal motoru → sentetik fixture'lardan deterministik, versiyonlanmış JSON export → erişilebilir statik TypeScript/React veya minimal vanilla UI (mevcut repo yapısı ve resmi docs kontrol edilerek seçilecek). Browser tarafında gizli gerçek veriye veya backend'e ihtiyaç yok. **İş:** fiyat değişim tablosu, filtre/arama, risk grupları, responsive grafik, açıklayıcı empty/error states; gerçekçi ama sentetik örnek veriler. **Test:** Python export snapshot/regression, web unit/component tests, build, Playwright smoke (uygunsa), mobil viewport ve keyboard/a11y kontrolü. **CI/deploy:** `main` push → Python export + frontend build/test → GitHub Pages artifact/deploy; testler geçmeden yayın yok. GitHub Pages Source = GitHub Actions tek seferlik repo ayarı gerekebilir; ayar mevcut değilse deployment **blocked** olarak raporlanır, başka doğrulanmış hosting yolu araştırılır. **Bitti sayılması:** JSON tekrar üretilebilir; fiyat/marj tutarlı; demo URL HTTP 200 ve UI smoke; mobil ekran görüntüleri; v0.2.0 release artifact'ları doğrulanmış.

## 16–20 Kasım — Warehouse Ops kalite ve operasyon ürünü

**Kod:** https://github.com/enesakn16/turkmopet-warehouse-ops · **Çıktı:** CLI release/örnek rapor, hosted demo zorunlu değil.

**Problem / kullanıcı:** depo sayım farklarını, bozuk hareket kayıtlarını ve geciken görevleri yönetmek. **Mimari:** CSV ingestion → strict validation/quarantine → deterministic reconciliation → SQLite task lifecycle → rapor/export. **İş:** atomik dosya çıktıları, idempotent task sync, CSV injection güvenliği, hatalı input ve kısmi dosya başarısızlığı regresyonu; gerekiyorsa küçük sentetik rapor görüntüleyici. **Test:** property/boundary fixtures, SQLite temp DB integration, CLI exit codes, CI Python matrix, güvenli export kontrolü. **Teslim:** sentetik demo CSV/JSON, terminal görüntüleri, operasyon runbook, README data flow, otomatik paket artifact. **Bitti sayılması:** tekrar import duplicate task üretmez; kritik veri kalite kapısı downstream çıktıyı engeller; tüm testler main üzerinde yeşil.

## 21–25 Kasım — Flagship release hardening

Üç ana projede başarısız Actions run ve açık issue triage; dependency pin/Dependabot PR'ları tek tek test edilerek, breaking major'lar ayrı PR; README komutları temiz checkout'ta denenir; screenshot'lar güncel UI'dan alınır; LICENSE/SECURITY/CHANGELOG/AI-assistance notları kontrol edilir; release'ler için SHA/artifact/checksum ve HTTP/CLI smoke doğrulanır. Bir proje gate'i geçmediyse yeni özellik değil o engel çözülür.

## 26–30 Kasım — Profil ve teslim denetimi

Public profilin featured setini yalnız **kanıtlı** üç projeye göre güncelle; eksik olanları `in progress` olarak bırak. Eski BMI repoyu ancak kanonik kaynak + attribution + APK doğrulandıktan sonra arşivle. Demo ve release linklerini HEAD/HTTP/asset kontrolünden geçir; kırık linkleri çıkar. Ay sonu retrospektifini yaz.

## Ölçülebilir başarı hedefleri

- **Android:** 1 doğrulanmış kanonik repo, main üzerinde unit/lint/build/instrumentation, indirilebilir APK.
- **Python:** Moto Fitment için CLI + API negatif testleri, kurulabilir wheel/sdist ve doğrulanmış release.
- **Web:** Supplier Price Watch için gerçek HTTP ile doğrulanmış mobil uyumlu sentetik demo, otomatik Pages deploy, doğru Decimal raporu.
- **Operations:** Warehouse Ops idempotency + data quality regresyonları ve sentetik rapor.
- **Portfolio:** 0 doğrulanmamış `live`/release iddiası; 0 sahte commit; en az üç güncel README; her release aynı SHA ve CI ile ilişkilendirilebilir.

## Mülakat konuları

1. **Compose UDF:** UiState tek doğruluk kaynağı; UI event → ViewModel → domain; JVM ve instrumentation test farkı.
2. **Fitment fail-closed:** belirsiz OEM/lastik servis bilgisi kabul edilmez; API ile domain ayrı; homologasyon sınırı.
3. **Supplier Decimal ve statik demo:** para için floating-point yerine Decimal; deterministik sentetik JSON; Pages otomatik publish ve CI gate.
4. **Warehouse idempotency:** aynı stok hareketi yeniden işlendiğinde görev ve stok iki kez sayılmaz; quarantine ve transaction boundary.

## Resmi kaynaklar (1 Kasım 2026 kontrolü)

- Android Compose architecture: https://developer.android.com/develop/ui/compose/architecture
- Android app architecture: https://developer.android.com/topic/architecture
- Android testing: https://developer.android.com/training/testing
- FastAPI TestClient: https://fastapi.tiangolo.com/tutorial/testing/
- GitHub Pages Actions deployment: https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
- GitHub Pages publishing source: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- GitHub Dependabot: https://docs.github.com/en/code-security/dependabot
