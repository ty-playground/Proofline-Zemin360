# Güvenlik

## Açık bildirimi

Bir güvenlik açığı bulduysanız **herkese açık bir issue açmayın.**

Bildirim için GitHub'ın özel güvenlik danışma kanalını kullanın: depo → **Security** → **Report a vulnerability**

Bildiriminizde şunlar bulunursa değerlendirme hızlanır:

- Açığın türü ve etkilenen bileşen
- Yeniden üretme adımları
- Olası etki

**Yanıt süresi:** Bildirim üç iş günü içinde onaylanır. Değerlendirme sonucu ve düzeltme planı iki hafta içinde paylaşılır.

Açık düzeltilene kadar kamuya açıklanmamasını rica ederiz. Düzeltme yayımlandıktan sonra, isterseniz bildirimde adınız anılır.

## Kapsam

| Kapsam içi | Kapsam dışı |
|---|---|
| Kimlik doğrulama ve yetkilendirme atlatma | Sosyal mühendislik |
| Yetkisiz veri erişimi (yatay/dikey yetki yükseltme) | Fiziksel erişim gerektiren saldırılar |
| Enjeksiyon açıkları | Üçüncü taraf servislerdeki açıklar |
| Olay günlüğünün değiştirilebilmesi | Otomatik tarama raporları (doğrulanmamış) |
| Metriklerin manipüle edilebilmesi | Hız sınırı olmayan uçlar (bilinen eksiklik) |
| Yapay zeka katmanından veri sızıntısı | |

**Olay günlüğünün değiştirilebilmesi ve metriklerin manipüle edilebilmesi** bu proje için kritik sınıftadır: sistemin tüm güven modeli bu iki kaydın sahtelenemez olmasına dayanır.

## Uygulanan tedbirler

| Alan | Tedbir |
|---|---|
| Erişim | Rol bazlı yetkilendirme; her kullanıcı yalnızca tarafı olduğu kayıtları görür |
| Aktarım | Uçtan uca şifreli bağlantı (HTTPS) |
| Saklama | Şifreli veri tabanı; yedeklerin şifrelenmesi |
| Oturum | Sunucu tarafında doğrulanan oturum belirteçleri |
| Girdi | Tüm kullanıcı girdisinde şema doğrulaması |
| Olay günlüğü | Ekleme-esaslı yazım; güncelleme ve silme yetkisi uygulama katmanında bulunmaz |
| Yapay zeka | Çağrı öncesi kişisel veri süzgeci; eşleşme bulunursa gönderim engellenir |
| Gizli anahtarlar | Ortam değişkenlerinde tutulur; depoya işlenmez |
| Bağımlılıklar | Otomatik güvenlik güncellemesi ve denetimi |

## Geliştirme kuralları

- Üretim verisiyle geliştirme yapılmaz; yalnızca kurgusal tohum veri seti kullanılır
- Gizli anahtarlar, belirteçler ve bağlantı dizeleri hiçbir koşulda depoya işlenmez
- `.env` dosyası `.gitignore` içindedir; `.env.example` yalnızca örnek değerler taşır

## Kişisel veri ihlali

Kişisel veri içeren bir ihlal tespit edilirse, 6698 sayılı Kanun'un 12'nci maddesi uyarınca veri sorumlusunun Kurula ve ilgili kişilere bildirim yükümlülüğü doğar. Bu durumda geliştirici ekip, veri sorumlusunu gecikmeksizin bilgilendirir ve teknik inceleme desteği sağlar.

Ayrıntı: [`docs/kvkk.md`](docs/kvkk.md)

## Bilinen sınırlamalar

Hackathon sürümünde henüz uygulanmamış olanlar; dört aylık geliştirme fazında ele alınacaktır:

- Uçlarda hız sınırlaması
- Kurumsal tekil oturum açma (SSO)
- İki aşamalı doğrulama
- Yönetici erişimlerinin ayrı denetim kaydı
- Otomatik yedek doğrulama testleri
