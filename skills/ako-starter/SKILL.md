---
name: ako-starter
description: Yeni bir projeyi ako-starter (create-ako-app) + mari-ui üzerine planlar ve kurar. Kullanıcının anlattığı fikirden ihtiyaç analizi çıkarır (platformlar, auth, dil, özellikler, veri modeli, ekranlar, tema), onay alınca projeyi oluşturup özellikleri iskeletler. "/ako-starter", "ako-starter ile yeni proje", "create-ako-app", "bu projeyi analiz et ve hazırla" dendiğinde kullan.
---

# ako-starter: analiz → plan → kurulum

Kullanıcı bir proje fikri anlatır; sen onu **ako-starter** şablonunun (`create-ako-app`) ve **mari-ui** tasarım sisteminin diline çevirirsin. Üç aşama vardır ve her aşamanın sonunda **dur, onay al**:

1. **Analiz** — fikri dinle, eksikleri sor, ihtiyaçları çıkar.
2. **Plan** — `PROJE-ANALIZI.md` yaz (şablon: [references/analiz-sablonu.md](references/analiz-sablonu.md)).
3. **Kurulum** — onaylanan planla projeyi oluştur ve özellikleri iskeletle.

Kullanıcının dilinde yaz (varsayılan Türkçe). Kısa ve somut ol; teknoloji dersi verme.

## Şablonun sabitleri (tartışmaya açma)

Bunlar ako-starter'ın kararıdır; analizde "seçenek" olarak sunma, gerekirse yalnızca sonucu söyle:

- pnpm workspaces + Turborepo; Node 24 LTS.
- `apps/api`: .NET 10 Minimal API, **tek proje + vertical slice** (`Features/<Özellik>/{Actions,Contracts,Data}` + `<Özellik>Endpoints.cs`), EF Core + PostgreSQL, ProblemDetails, `Result/Error` (`<ozellik>.<hata>` kodları), FluentValidation, resx ile tr/en.
- `apps/web/<ürün>`: React Router (framework modu) + Hono BFF; tarayıcı API'ye doğrudan gitmez, token httpOnly çerezde. İş mantığı loader'a yazılmaz.
- `apps/mobile`: Expo + `@mari-ui/native`; API'ye doğrudan, token SecureStore'da. Backend'siz modda veri cihazda (SQLite + Drizzle).
- `packages/api-client`: OpenAPI → Orval → fetch + TanStack Query hook'ları. **Elle contract yazılmaz**; API değişince `pnpm generate`.
- Admin uçları her özelliğin `Actions/Admin/` klasöründe, `/admin/...` adresinde; backoffice ayrı web uygulamasıdır.
- Her uygulama tek başına silinebilir; ortak kod yalnızca `packages/` altında.
- UI: mari-ui bileşen/modülleri dışında kendi bileşen kütüphanesi kurulmaz; görünüm tema (persona/renk) ile değişir.

Projede `DECISIONS.md` varsa oradaki güncel karar bu listeyi geçersiz kılar; kurulumdan sonra önce onu oku.

## 1. Analiz

Kullanıcının mesajını oku, cevabı zaten verilmiş soruları **sorma**. Kalanları [references/sorular.md](references/sorular.md) sırasıyla, **tek seferde en fazla 4 soru** olacak şekilde sor (mümkünse seçmeli soru aracıyla, önerilen seçenek ilk sırada). Tahmin edebildiğin yerde varsayım yap ve varsayımı açıkça yaz; kullanıcı düzeltir.

Çıkarman gerekenler:

- **Platformlar**: site / backoffice / mobil / backend → `create-ako-app` bayrakları.
- **Kimlik**: auth, misafir, sosyal giriş, roller (Admin/User dışında rol varsa not et).
- **Dil**: tek dil mi, çoklu mu (`--lang`).
- **Özellikler**: her biri bir vertical slice. Her özellik için varlıklar (alanlar, ilişkiler), use case'ler (public / kullanıcıya özel / admin), iş kuralları ve hata kodları.
- **Ekranlar**: site sayfaları, backoffice sayfaları, mobil ekranlar → hangi mari-ui modülü/bileşeni karşılıyor.
- **Tasarım**: persona (`corporate`, `playful`, `minimal`, `editorial`, `luxury`) ya da özel renk; marka rengi varsa hex.
- **Dış bağımlılıklar**: ödeme, e-posta, dosya yükleme, harita, bildirim, arama… Şablonda olmayanları "eklenecek" diye işaretle.
- **Kapsam dışı / sonraya**: MVP'ye girmeyenler.

mari-ui'da hazır modüller (web: `@mari-ui/modules`, native: `@mari-ui/native-modules`): about, auth, basket, blog, checkout, contact, dashboard, error, faq, filters, home, landing, list, portfolio, pricing, products, profile, reports, services, standard, team, testimonials. Ekranı önce bunlarla eşle; karşılığı yoksa mari-ui bileşenleriyle (table, field, modal, tabs, upload, chart…) kurulacağını yaz. Kurulu projede güncel listeyi `node_modules/@mari-ui/*` içinden ya da mari-ui AI kural dosyasından doğrula.

Analiz bitince kısa bir özet ver ve "Planı yazayım mı?" diye **dur**.

## 2. Plan

Onay gelince `PROJE-ANALIZI.md` dosyasını [references/analiz-sablonu.md](references/analiz-sablonu.md) yapısında yaz. Proje henüz yoksa dosyayı çalışma dizinine yaz; kurulumdan sonra proje köküne taşı. Planın en önemli çıktıları:

- Tek satırlık **`create-ako-app` komutu** (bayraklar sorusuz, `-y` ile).
- **Silinecek örnekler** (Akı Kahve: `Products`, `Todos` …) ve korunacaklar.
- **Özellik tablosu** (varlık, uçlar, ekranlar) ve **sıra** (bağımlılığa göre aşamalar; her aşama ayrı branch/PR olabilecek büyüklükte).
- **Açık sorular**: cevabı olmadan başlanamayacak şeyler.

Planı göster, "Kurulumu başlatayım mı?" diye **dur**.

## 3. Kurulum

Onaydan sonra sırayla:

1. `npx create-ako-app@latest <klasör> -y <bayraklar>` (komutu kullanıcıya önce göster). Klasör boş olmalı; doluysa sor.
2. Proje kökündeki `README.md`, `DECISIONS.md`, `ROADMAP.md` ve AI kural dosyalarını (`CLAUDE.md`/`AGENTS.md`, mari-ui kuralları) oku; plandaki varsayımlarla çelişen varsa kullanıcıya söyle.
3. Tema: `npx @mari-ui/cli theme --persona <ad>` ya da `--primary "#hex" [--accent "#hex"]`; ardından `npx @mari-ui/cli sync`.
4. `PROJE-ANALIZI.md`'yi proje köküne koy; `ROADMAP.md`'ye plandaki aşamaları ekle.
5. **Yalnızca ilk aşamayı** uygula, sonra dur. Her özellik için sıra:
   - API: `Features/<Özellik>/Data` (entity + EF ayarı) → migration → `Actions/*.cs` (İstek → Doğrulama → İş mantığı → Endpoint) → `<Özellik>Endpoints.cs` → hata kodları + resx metinleri → xUnit testi.
   - `pnpm generate` ile api-client'ı yenile (elle düzenleme yok).
   - Web: `app/features/<özellik>/{pages,components,hooks}`, adres `app/routes.ts`'te; metin anahtarları `locales/tr.json`'a.
   - Mobil: aynı özelliği ekran olarak, `@mari-ui/native` ile.
6. Doğrula: `pnpm typecheck`, `pnpm lint`, `pnpm test`, `pnpm generate:check`, `dotnet test`. Kırmızı varsa düzelt; düzeltemiyorsan çıktıyla birlikte söyle.
7. Ne yapıldığını, neyin kaldığını (sonraki aşama) ve açık soruları kısaca raporla.

## Kurallar

- Kullanıcı açıkça istemedikçe commit atma, push etme, uzak repo açma.
- Şablonun sabitlerini değiştirmen gerekiyorsa (ör. başka veritabanı) önce sor ve `DECISIONS.md`'ye gerekçesiyle yaz.
- Gizli değer (ClientId/secret, bağlantı dizesi) uydurma; `.env`/user-secrets'ta boş bırak, plana "kullanıcı dolduracak" diye yaz.
- Örneklerde uydurma marka yerine kullanıcının verdiği adı kullan; ad yoksa sor.

## Skill'i geliştirme

Bu skill kullanıldıkça iyileştirilir. Çalışırken aksayan yerleri not et: gereksiz ya da eksik soru, yanlış bayrak, plan şablonunda eksik bölüm, kurulumda hata veren adım, güncelliğini yitirmiş şablon bilgisi. İş bitince kullanıcıya "Skill'de şunları iyileştirebiliriz" diye kısa bir liste öner; onay gelirse bu skill'in dosyalarını güncelle.
