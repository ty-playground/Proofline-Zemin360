# Yönetişim

Bu doküman, Proofline'ın kimin tarafından, hangi kurallarla yönetildiğini ve proje bittikten sonra ne olacağını tanımlar.

Deponun herkese açık olması tek başına sürdürülebilirlik üretmez. Bakımı yapan kimse yoksa, karar hakkı tanımlı değilse ve devir yolu belli değilse açık kaynak etiketi bir vaat olarak kalır. Bu doküman o boşluğu kapatmak için vardır.

## Mevcut yapı

**Bakımcılar:** Taylan Akgün, Yunus Hanifi Öztürk

Bakımcılar pull request birleştirme, sürüm çıkarma ve mimari kararlar konusunda yetkilidir.

**Program sahibi:** Zemin360 kapsamında Türkiye Girişimcilik Vakfı (GİRVAK). Ürün öncelikleri ve kapsam kararlarında program sahibinin ihtiyaçları belirleyicidir.

## Karar türleri

| Karar | Nasıl alınır |
|---|---|
| Hata düzeltmesi, dokümantasyon | Tek bakımcı onayı yeterlidir |
| Yeni özellik | İssue açılır, iki bakımcı mutabakatı aranır |
| Mimari değişiklik | İssue açılır, gerekçe yazılır, program sahibi bilgilendirilir |
| Tasarım ilkelerinin değişmesi | Yalnızca program sahibiyle birlikte |
| Kapsam dışı alanların açılması | Yalnızca program sahibiyle birlikte |

Tasarım ilkeleri [`CONTRIBUTING.md`](CONTRIBUTING.md) dosyasında listelenmiştir. Bunlar tartışmaya açıktır ancak sessizce değiştirilemez; değişiklik gerekçesiyle birlikte kayda geçer.

## Sürüm politikası

Anlamsal sürümleme kullanılır (`MAJOR.MINOR.PATCH`).

- Veri modeli veya API'de geriye dönük uyumsuz değişiklik → MAJOR
- Yeni özellik, uyumlu değişiklik → MINOR
- Hata düzeltmesi → PATCH

Her sürüm için değişiklik günlüğü ve gerekli veri tabanı göç betikleri yayımlanır. Göç betikleri geri alınabilir olacak biçimde yazılır.

## Devredilebilirlik

Proje, mevcut ekip ayrıldıktan sonra da çalışabilecek biçimde tasarlanmıştır. Bunun somut karşılıkları:

**Çok programlı yapı.** Her kayıt bir programa bağlıdır. Zemin360 ilk programdır, tek program değildir. Başka bir kalkınma ajansı, teknopark, teknoloji transfer ofisi veya hızlandırma programı aynı sistemi kendi verisiyle çalıştırabilir.

**Yapılandırılabilir akış.** Aşama tanımları, geçiş koşulları ve program hedefleri koda gömülü değildir. Farklı bir programın farklı bir akışı olabilir.

**Tek komutla kurulum.** `docker compose up` ile ayağa kalkar. Kurulumun belirli bir bulut sağlayıcısına bağımlılığı yoktur; kendi sunucusunda barındırılabilir.

**Belgelenmiş mimari.** Veri modeli, durum makinesi, metrik türetimi ve ekran akışları `docs/` altında yazılıdır. Kod okunmadan sistemin nasıl çalıştığı anlaşılabilir.

**Veri taşınabilirliği.** Tüm veri standart bir PostgreSQL şemasındadır ve dışa aktarılabilir. Tescilli bir formata bağlanma yoktur.

## Devir

Program sahibi projeyi devralmak veya başka bir bakımcıya devretmek istediğinde:

1. Depo sahipliği devredilir
2. Altyapı erişimleri aktarılır
3. Mevcut bakımcılar bir devir dokümanı hazırlar
4. Bir geçiş dönemi boyunca sorulara yanıt verilir

Lisans (Apache-2.0) hiçbir devirde değişmez; mevcut ve geçmiş sürümler açık kaynak kalır.

## Lisans

Apache-2.0. MIT'ten farklı olarak açık bir patent hükmü içerir; bu, kurumsal kullanımda hukuki belirsizliği azaltır.

Katkıda bulunanlar, katkılarının aynı lisansla yayımlanmasını kabul etmiş sayılır.
