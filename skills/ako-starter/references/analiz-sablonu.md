# PROJE-ANALIZI.md şablonu

Başlıkları koru; boş kalan bölümü silme, "yok" yaz. Tablolar kısa olsun.

````markdown
# <Proje adı> — Proje analizi

<Tek paragraf: ne, kimin için, MVP'nin amacı.> Tarih: <YYYY-AA-GG>

## Kurulum

```bash
npx create-ako-app@latest <klasör> -y --web=<...> --<mobile|no-mobile> --<auth|no-auth> --<guest|no-guest> --<social|no-social> --<lang|no-lang> --no-sample
npx @mari-ui/cli theme --persona <ad>   # ya da --primary "#hex"
```

| Parça            | Karar           | Neden     |
| ---------------- | --------------- | --------- |
| Site             | var / yok       | ...       |
| Backoffice       | var / yok       | ...       |
| Mobil            | var / yok       | ...       |
| Backend          | var / cihazda   | ...       |
| Auth / misafir / sosyal | ...      | ...       |
| Diller           | tr, en / yalnız tr | ...    |
| Tema             | <persona / renk> | ...      |

**Örnek kod:** `Products`, `Todos` ve Akı Kahve içeriği silinir (ya da: X kalır çünkü ...).

## Roller

| Rol | Yapabildikleri |
| --- | -------------- |

## Özellikler

### <Özellik> (`Features/<Özellik>`)

- **Varlıklar:** `Entity` (alan: tip, zorunlu?, ilişki)
- **Uçlar:**
  | Yöntem | Adres | Kim | Not |
  | ------ | ----- | --- | --- |
- **Kurallar / hata kodları:** `<ozellik>.<kod>` — açıklama
- **Ekranlar:**
  | Uygulama | Ekran | mari-ui karşılığı |
  | -------- | ----- | ----------------- |

## Dış servisler

| İhtiyaç | Sağlayıcı | Şablonda var mı |
| ------- | --------- | --------------- |

## Aşamalar

1. **<Ad>** — kapsam; bitti tanımı.
2. ...

## Kapsam dışı (sonraya)

- ...

## Varsayımlar

- ... (kullanıcı onaylamadı; yanlışsa düzelt)

## Açık sorular

- ...
````
