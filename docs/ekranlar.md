# Ekranlar

Sistem altı ekrandan oluşur. Hepsi aynı veri zincirinin farklı görünümüdür; ayrı modüller değildir.

---

## 1. İhtiyaç Kanvası

**Kim kullanır:** Kurum temsilcisi

**Düzen:** Solda dokuz alanlı form, sağda canlı olgunluk paneli.

**Alanlar:** Problem · Mevcut durum (sayısal) · Başarı kriteri (şu an → hedef) · Veri ve sistem erişimi · Kısıtlar · Bütçe bandı · Karar tarihi · Karar verici · Başarılı olursa sonraki adım

**Sağ panel:** Olgunluk skoru (0–100), eksik alan listesi ve alan bazlı eleştiriler. Eleştiri metni yapay zekadan gelir; servis erişilemezse kural tabanlı kontrol listesi devreye girer ve panel aynı yapıda çalışmaya devam eder.

**Kritik davranış:** Skor eşiğin altındayken "Yayımla" düğmesi devre dışıdır. Düğmenin yanında tek satır gerekçe görünür.

**Alan içi uyarı:** Serbest metin alanlarında kişisel veri girilmemesi hatırlatılır.

---

## 2. Hazırlık Paneli

**Kim kullanır:** Girişim ve birey (görüntüleme), kurum (kendi panelini yönetme)

**Düzen:** İki sütun.

| Sol — Beyan | Sağ — Ölçüm |
|---|---|
| Kurumun kendi işaretlediği alanlar | Olay günlüğünden türetilen davranış |
| Sponsor, bütçe, veri erişimi, karar verici | Yanıt süresi, onay süresi, taahhüt uyumu, geçmiş pilot sonuçları |
| Değiştirilebilir | Değiştirilemez |

**Metrikler kurum düzeyindedir.** Hiçbir gerçek kişi puanlanmaz, sıralanmaz veya profillenmez.

**Taahhüt kutusu:** Kurum kendi süre sözlerini girer ("sorulara üç iş günü içinde döneriz"). Ölçüm dışarıdan bir standarda göre değil, bu söze göre yapılır.

**Yeni kurum durumu:** Ölçüm sütunu boş bırakılmaz, "henüz veri yok (0 etkileşim)" olarak gösterilir. Karşı taraf geçmişi olmayan bir kurumla çalıştığını bilerek karar verir.

**Gerekçe notu:** Kurum bir metriğin yanına açıklama düşebilir; not karşı tarafa da görünür.

**Rozetler:** Sözünü tutan kurum rozet kazanır (Hızlı Yanıt Veren, Veri Erişimi Sağlar, Kararını Zamanında Verir). Kırmızı karne veya karşılaştırmalı sıralama üretilmez.

---

## 3. Vaka

**Kim kullanır:** Kurum (açan), birey veya girişim (yapan)

**Üç görünüm:**

**Liste** — Açık işler; süre, konu ve ihtiyaç bağlantısıyla.

**Detay** — Görev tanımı, değerlendirme ölçütü (rubrik, başvuru öncesi görünür), süre üst sınırı, çıktı sahipliği notu.

**Teslim** — Dosya veya bağlantı yükleme, kurum onayı/reddi, gerekçe.

**Onay sonrası:** Yapanın profiline doğrulanmış kayıt düşer. Kurumun onay süresi olay günlüğüne yazılır ve hazırlık panelini besler.

**Kural:** Gerçek müşteri verisi veya üretim verisi içeren görev açılamaz.

---

## 4. Pilot

**Kim kullanır:** Her iki taraf ve program yöneticisi

**Üst blok:** Kapsam, kapsam dışı, sayısal başarı eşiği, iki taraftan isimli sorumlu, **karar tarihi** ve kalan gün sayacı.

**Orta blok — kilometre taşları:** Her satırda iki onay kutusu (kurum / girişim). Tek taraf işaretlediğinde satır "karşı taraf bekleniyor" durumunda kalır. Tek taraflı kapatma denendiğinde sistem açık bir uyarı verir.

**Alt blok — olay günlüğü:** Kim, ne zaman, ne yaptı. Salt okunur. Geçmiş bir kaydı değiştirme girişimi reddedilir; düzeltme yeni bir olay olarak yazılır.

**Vade uyarısı:** Karar tarihine yaklaşıldığında üst blokta uyarı belirir. Tarih geçtiğinde pilot otomatik olarak karar bekleyen duruma geçer.

---

## 5. Karar ve Kapanış

**Kim kullanır:** Her iki taraf

**Karar formu:** Tek soru, üç seçenek — **Ölçekle / Durdur / Bir kez uzat (gerekçeyle)**. Yanıt gelmezse durum "durdu" olur.

**Kapanış nedeni:** Önceden tanımlı seçenek listesi — bütçe çıkmadı, karar verici değişti, veri erişimi verilemedi, teknik uyumsuzluk, girişim teslim edemedi, kurum içi öncelik değişti, başarılı (ölçeğe geçiyor). Serbest metin değildir; bu, kişi hakkında olumsuz yorum yazılmasını yapısal olarak engeller.

**Sonuç belgesi:** Hedef, gerçekleşen, süre ve karar otomatik derlenir. İki tarafın profiline doğrulanmış kayıt olarak işlenir.

---

## 6. Program Panosu

**Kim kullanır:** Program yöneticisi

**Üst şerit:** Aktif kurum, aktif girişim, açık pilot, karara gelen pilot sayıları ve program hedeflerine göre ilerleme.

**Huni:** İhtiyaç → yayımlanan → vaka → pilot → sonuç. Her aşamada kayıp oranı ve ortalama süre.

**Tıkanma listesi:** Vadesi geçmiş pilotlar, uzun süre taslakta bekleyen ihtiyaçlar, değerlendirme bekleyen vaka çözümleri.

**Kapanış nedeni dağılımı:** Ekosistem düzeyinde okunabilir istatistik. Bir istatistiğin arkasındaki kayıt sayısı eşiğin altındaysa gösterilmez — az sayıda kayıt tek bir kurumu işaret edebilir.

**Giriş yolu karşılaştırması:** Vakadan gelen pilotlar ile doğrudan gelen pilotların sonuç dağılımı.

**Rapor:** Tek tıkla dışa aktarım. Kişi adı içermez.

**Hedef tanımları:** "Eşleşme" ve "pilot" sayımının hangi aşamada yapılacağı yapılandırılabilir; sabit değildir.

---

## Ortak ilkeler

- Her kullanıcı yalnızca tarafı olduğu kayıtları görür
- Hiçbir ekranda otomatik eleme, sıralama veya uyum skoru yoktur
- Sistem gösterir; kararı insan verir
- Boş durum "veri yok" olarak dürüstçe gösterilir, gizlenmez
