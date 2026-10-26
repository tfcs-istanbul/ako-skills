# Analiz soruları

Sırayla git; kullanıcının anlattığından cevaplanmış olanı atla. Parantez içi: hangi karara/bayrağa dönüştüğü.

## A. Ürün

1. Proje ne yapıyor, kimin için? Tek cümle. (planın özeti)
2. Proje/marka adı ne? Klasör adı ne olsun? (`create-ako-app <klasör>`)
3. Kullanıcı türleri kimler? Ziyaretçi, üye, yönetici, başka rol? (auth, roller)
4. MVP'de mutlaka olması gereken 3-5 iş ne? Sonraya kalabilecekler? (aşamalar, kapsam dışı)

## B. Platform

5. Web sitesi olacak mı? Yönetim paneli (backoffice) gerekiyor mu? (`--web=site,backoffice|site|backoffice|none`)
6. Mobil uygulama olacak mı? (`--mobile` / `--no-mobile`)
7. Yalnızca mobilse: veri sunucuda mı, cihazda mı kalsın? (`--backend` / `--no-backend`)
8. SEO önemli mi? Hangi sayfalar herkese açık? (loader + cache vs. TanStack Query)

## C. Kimlik ve dil

9. Giriş/kayıt gerekli mi? (`--auth`; backoffice varsa zorunlu)
10. Misafir kullanım olsun mu (kayıt olunca veri hesaba taşınır)? (`--guest`)
11. Sosyal giriş? Hangileri: Google, Apple, Facebook, GitHub, X, LinkedIn. (`--social`; iOS'ta başka sosyal giriş varsa Apple zorunlu)
12. Hangi diller? Tek dilse `--no-lang`. (`--lang`; varsayılan tr, en, de)

## D. Veri ve iş kuralları

Her özellik için:

13. Hangi kayıtlar tutuluyor ve alanları neler? İlişkiler? (entity'ler)
14. Kim ne yapabilir: herkes okur / sahibi düzenler / admin yönetir? (public, kullanıcıya özel, `Actions/Admin`)
15. Kurallar ve hata durumları? (ör. "stok yoksa sipariş olmaz" → `orders.out_of_stock`)
16. Dosya/görsel yükleme, arama/filtre, sayfalama gerekiyor mu?

## E. Dış servisler

17. Ödeme, e-posta, SMS/push bildirim, harita, analitik, dış API? Hangi sağlayıcı? (şablonda yoksa "eklenecek")

## F. Tasarım

18. Hazır bir kişilik mi: kurumsal, oyunbaz, minimal, editoryal, lüks? Yoksa marka rengi (hex) mi? (`mari-ui theme --persona` / `--primary`)
19. Referans aldığın site/uygulama var mı? (yapı için; görünüm mari-ui token'larından gelir)
20. Açık/koyu tema ikisi de mi?

## G. Yayın

21. Nerede yayınlanacak (VPS + Docker Compose, bulut, mağazalar)? Alan adı belli mi? (`compose.prod.yaml`, Aşama 4)
