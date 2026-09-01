# September 2026 Portfolio Roadmap

This month is about release quality, not repository count. The portfolio will focus on three flagship tracks: a Kotlin Android app, a motorcycle fitment product, and a procurement/operations product. Existing Python projects that are already CI-backed will be maintained, but new repositories should not be opened unless one of these tracks is complete.

## August review

### Shipped or materially strengthened

- `moto-fitment-engine` gained manufacturer-traceable fitment records, strict dataset validation, tyre-notation handling, geometry screening tests, and combined OEM lookup + catalogue screening.
- `supplier-price-watch` gained strict CSV/XLSX supplier snapshot comparison, versioned supplier profiles, margin-risk analysis, atomic report writes, regression tests, packaging checks, and CI.
- `cari-360` gained an offline/synthetic finance demo, aging-report logic, security isolation, dependency-audit CI, and stronger public documentation.
- `turkmopet-warehouse-ops`, `turkmopet-marketplace-intelligence`, `turkmopet-b2b-growth-suite`, and `turkmopet-seo-content-engine` now represent real business-domain work rather than empty placeholders.

### Not yet verified as finished

- `bmi-hesaplama-mobile-app` still has an open Android PR whose final Actions result, APK artifacts, instrumentation artifacts, and conflict resolution are not verified.
- `supplier-price-watch` describes itself as a `v0.1.0` release candidate, but there is currently no GitHub Release published.
- No public web demo is counted as complete until the URL is independently verified after deployment.

## September goals

1. Finish one Android release with verified CI and an installable artifact.
2. Turn `moto-fitment-engine` into the strongest domain-engine project in the portfolio, with a small API/demo surface and explicit provenance.
3. Ship `supplier-price-watch` v0.1.0 with reproducible artifacts and a polished operator-facing report/demo.
4. Reduce portfolio noise: maintain existing Python repos, but do not split attention across six simultaneous feature streams.

---

## Track A — Kotlin Android: BMI app release

Repository: https://github.com/enesakn16/bmi-hesaplama-mobile-app

### Problem

Deliver a compact Android app that demonstrates modern Compose state management, accessibility, deterministic domain rules, automated testing, and a reproducible release pipeline.

### Target users

General users who want a simple BMI/healthy-weight-range calculator. The app must remain clearly informational rather than presenting medical advice.

### Architecture target

- Jetpack Compose UI
- Unidirectional data flow
- `ViewModel` as screen state holder
- lifecycle-aware Flow collection where Flow is used
- pure Kotlin domain calculation/validation layer
- no plaintext credential storage and no fake authentication feature

### 1–5 September — unblock and verify

- Resolve the open PR conflict safely instead of force-merging.
- Confirm unit tests, lint, debug APK build, and emulator/instrumentation tests all run on the PR head and on `main` after merge.
- Inspect Actions logs rather than relying only on the presence of workflow YAML.
- Verify generated APK artifacts exist and are downloadable.
- Remove obsolete credential/authentication remnants if any are still carried from the old repository history.
- Keep the build-tool upgrade conservative: do not combine a large AGP/Gradle/Kotlin migration with the release unblock unless the existing build is itself unsupported.

### 6–8 September — polish and release

- Final accessibility pass: semantics, focus order, keyboard actions, content descriptions only where meaningful.
- Add 3–5 current screenshots to README/release assets.
- Add `CHANGELOG.md` if missing.
- Publish the first GitHub Release only after the exact release commit passes CI.
- Attach a verified APK produced from the release commit/workflow.

### Test strategy

- JVM unit tests for BMI category boundaries and healthy-weight calculations.
- ViewModel/state tests for valid/invalid input transitions.
- Compose instrumentation tests for primary happy path and accessibility semantics.
- Android lint on PR and `main`.

### Release criteria

- PR merged without unresolved conflict.
- Unit tests: pass.
- Lint: pass.
- Instrumentation: pass.
- APK artifact: present and verified.
- Release notes and screenshots: present.

### Interview talking points

- Why unidirectional data flow reduces UI/domain coupling.
- Difference between JVM unit tests and Compose instrumentation tests.
- Why a release artifact is stronger evidence than merely having a workflow file.

---

## Track B — Python + API: Moto Fitment Engine

Repository: https://github.com/enesakn16/moto-fitment-engine

### Problem

Motosiklet marka + model + yıl girdisinden doğrulanmış OEM lastik ölçülerini bulmak ve alternatif ölçüleri yalnızca kontrollü bir geometry screen olarak değerlendirmek.

### Target users

Motorcycle-parts e-commerce teams, catalog managers, workshops, customer-support agents, and future B2B integrations.

### Architecture target

- Dependency-light Python domain core remains the source of truth.
- Verified fitment JSON stays separate from demo-only in-module examples.
- Small FastAPI adapter only after the domain contract is stable.
- API responses must expose provenance and rejection reasons; they must not silently convert a geometry screen into a fitment guarantee.

### 9–13 September — decision reasons and data contract

- Replace boolean-only alternative screening with structured decision reasons.
- Add explicit result codes such as rim mismatch, diameter delta exceeded, width delta exceeded, missing verified OEM record.
- Add load/speed/rim-width fields only where authoritative source data is available; unknown must remain unknown rather than guessed.
- Add dataset schema/version metadata and regression tests for backward compatibility.

### 14–17 September — API and demo surface

- Add a small FastAPI adapter around the tested domain layer.
- Endpoints: health, verified fitment lookup, alternative screening.
- Auto-generated OpenAPI docs are acceptable as the first interactive demo surface.
- Add request/response examples that use synthetic or redistributable data only.
- Add Dockerfile and container smoke test if it improves reproducibility; do not add orchestration complexity that the project does not need.

### 18 September — verification gate

- Run full unit/regression suite.
- Validate verified dataset in CI.
- Build/install package in CI.
- Container/API smoke test if the API layer shipped.
- Verify public demo only if deployment can be automated and the actual URL responds correctly; otherwise document local Docker/uvicorn run commands and do not claim a live demo.

### Release criteria

- No ambiguous lookup silently returns a match.
- Every production-style record has source provenance and verification date.
- Structured screening reasons are tested.
- API layer, if included, delegates to the domain core rather than duplicating rules.
- README contains architecture diagram/data flow and clear safety limits.

### Interview talking points

- Fail-closed matching versus fuzzy matching.
- Provenance as a data-quality requirement.
- Why transport/API code should not contain core fitment rules.

---

## Track C — Python procurement product: Supplier Price Watch v0.1.0

Repository: https://github.com/enesakn16/supplier-price-watch

### Problem

Compare recurring supplier price files without guessing product identity, detect cost changes and catalogue deltas, and surface margin risk before selling prices become stale.

### Target users

Procurement, e-commerce pricing, category management, and finance/operations teams.

### Architecture target

- Strict ingestion/profile layer
- Deterministic comparison domain using `Decimal`
- Explicit catalogue enrichment
- Report/output layer isolated from comparison rules
- CLI remains first-class; web UI only if it adds actual operator value

### 19–23 September — release hardening

- Create verified synthetic fixtures that resemble real supplier header patterns without exposing commercial data.
- Add controlled barcode/EAN or explicit SKU-alias mapping; do not introduce fuzzy auto-matching.
- Add XLSX report output with clear review status and risk categories if the output contract can be tested deterministically.
- Test interrupted/failed output writes so existing reports are preserved.
- Review dependency versions and security alerts before the release.

### 24–26 September — operator demo

- Produce a reproducible synthetic before/after supplier scenario.
- Add screenshots or short report previews to README.
- If a web surface is added, keep it read-only and lightweight; it must consume the existing domain API rather than fork business rules.
- Prefer automatic deployment from `main`. If hosting requires a one-time account action, document the blocker and keep the release local/CLI until it is done.

### 27 September — v0.1.0 release gate

- Tests on supported Python versions: pass.
- Package build/install smoke test: pass.
- CLI `--help` and synthetic full-flow smoke test: pass.
- Dependency/security audit: pass or explicitly documented.
- Publish GitHub Release `v0.1.0` with wheel/source archive only after the release commit passes CI.

### Interview talking points

- Why `supplier + SKU + currency` is safer than fuzzy name matching.
- Why `Decimal` is used for financial calculations.
- Why atomic file replacement matters for operational reports.

---

## 28–30 September — portfolio consolidation

No new product features unless a release blocker requires them.

- Update profile README to feature only projects with current evidence.
- Verify every badge, README link, release link, and demo URL.
- Add or refresh screenshots for the three flagship tracks.
- Close stale draft PRs or clearly mark why they remain open.
- Review Dependabot PRs individually; do not batch unrelated major framework migrations into one blind upgrade.
- Keep `cari-360`, Warehouse Ops, Marketplace Intelligence, B2B Growth Suite, and SEO Content Engine in maintenance mode: security, broken CI, documentation accuracy, and small bug fixes only.
- Decide whether `Enes-Nevra-Davetiye` should be archived after the BMI migration so there is one canonical Android repository.

## September completion scorecard

The month is successful only if most of these are true:

- 1 verified Android GitHub Release with an APK artifact.
- `moto-fitment-engine` has structured compatibility/screening reasons and a tested service boundary.
- `supplier-price-watch` has a published `v0.1.0` GitHub Release.
- At least two flagship repositories have current screenshots/demo evidence.
- Every claimed CI/release/demo status is verifiable from the public repository.
- No new empty repository was created.
- Duplicate BMI ownership is resolved or explicitly archived/documented.

## Engineering policy for this month

- Real work may produce multiple commits in a day, but commits should map to implementation, tests, refactoring, documentation, CI, or release work.
- No fake activity, backdating, empty commit spam, or misleading status badges.
- A project is not called released until the release commit has passed its required checks and its artifact/demo has been verified.
- Public repositories use synthetic/non-sensitive business data unless redistribution is explicitly safe.
