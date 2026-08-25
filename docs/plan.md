# Geliştirme Planı

Online geliştirme dönemi: **18 Eylül – 7 Ekim** (20 gün)
Yüz yüze final: **9–11 Ekim, İstanbul**

Plan gün bazında bölünmüştür. Her günün sonunda çalışan bir sürüm bırakılır; yarım kalmış özellikle gün kapatılmaz.

---

## Hafta 1 — Temel ve ihtiyaç katmanı

| Gün | İş | Gün sonunda elde olan |
|---|---|---|
| 1 | Proje kurulumu, veri modeli, sekiz tablo, migration | Boş ama çalışan veritabanı |
| 2 | Tohum veri seti, kimlik doğrulama, üç rol | `npm run seed` çalışıyor, sistem dolu |
| 3 | İhtiyaç kanvası formu (dokuz alan) | Kurum ihtiyaç girebiliyor |
| 4 | Olgunluk skoru — kural tabanlı hesaplama | Skor ve eksik alan listesi görünüyor |
| 5 | Yayımlama kapısı | Skor eşiğin altındaysa yayımlanamıyor |
| 6 | Dil modeli eleştirmeni | Eksik alanlara alan-özel eleştiri geliyor |
| 7 | Yedek yol ve cila | Servis erişilemezse kural listesi devreye giriyor |

**Tohum veri neden ikinci gün:** Boş ekranda geliştirme yapılamaz. Pano yazarken hiç pilot yoksa ekranın doğru çalışıp çalışmadığı görülmez; hazırlık paneli yazarken hiç olay kaydı yoksa metrik hesaplanamaz. Sekiz kurum, altı ihtiyaç, yirmi beş vaka çözümü ve üç pilot içeren sentetik veri seti en başta yazılır ve her ekran dolu veriyle geliştirilir. Veriler tamamen kurgusaldır; gerçek kurum adı kullanılmaz.

---

## Hafta 2 — Hazırlık ve vaka

| Gün | İş | Gün sonunda elde olan |
|---|---|---|
| 8 | Taahhüt girişi | Kurum kendi süre sözlerini giriyor |
| 9 | Hazırlık paneli — beyan sütunu | İki sütunlu ekran, sol tarafı çalışıyor |
| 10 | Vaka: yayımlama ve başvuru | Kurum vaka açıyor, aday başvuruyor |
| 11 | Vaka: çözüm, değerlendirme, profile kayıt | Akış uçtan uca tamam |
| 12 | Pilot oluşturma ve kilometre taşları | Pilot açılabiliyor |
| 13 | Çift taraflı onay | Tek taraf kilometre taşını kapatamıyor |
| 14 | Olay günlüğü (append-only) | Her hareket kaydediliyor, geriye dönük değişmiyor |

---

## Hafta 3 — Karar, ölçüm, pano

| Gün | İş | Gün sonunda elde olan |
|---|---|---|
| 15 | Vade motoru, karar formu, kapanış nedeni | Süre dolunca karar sorusu geliyor, yanıtsızlık durdurma sayılıyor |
| 16 | Ölçüm hesaplayıcı → hazırlık panelinin ölçüm sütunu | Yanıt ve onay süreleri olay günlüğünden türetiliyor |
| 17 | Program panosu ve rapor dışa aktarımı | KPI'lar ve tablo çıktısı hazır |
| **18** | **Özellik geliştirme kapanır** — hata temizliği, cila | Ürün donduruldu |
| 19 | Tohum veri zenginleştirme, demo senaryosu | Üç farklı kurum profili (geçmişi iyi / kötü / hiç yok) |
| 20 | Sunum metni ve prova | Pitch hazır |

**Ölçüm motoru neden on altıncı gün:** Olay günlüğü on dördüncü günde tamamlandığı için metrikler tek günde türetilebilir hale gelir. Daha erken yazılırsa üzerinden hesaplanacak veri bulunmaz.

---

## Yüz yüze etap — 9–11 Ekim

Üç gün yeni özellik geliştirme dönemi değildir. İstanbul'a çalışan bir ürünle gidilir.

| Gün | İş |
|---|---|
| 9 Ekim | Kurulum, mentör geri bildirimi, son rötuş |
| 10 Ekim | Demo senaryosu provası, kenar durum temizliği |
| 11 Ekim | Sunum |

---

## Üç kural

1. **On sekizinci günde özellik geliştirme durur.** Kalan iki gün demo ve sunuma ayrılır. Bu kuralı ihlal eden projeler sunum günü çöken demo gösterir.
2. **Her akşam çalışan bir sürüm bırakılır.** Ertesi güne yarım kalmış iş devredilmez.
3. **Tohum veri ilk günlerde yazılır.** Sonradan veri eklemek, dolu veriyle hiç test edilmemiş ekranlarda zincirleme hataya yol açar.

---

## Risk ve azaltma

| Risk | Azaltma |
|---|---|
| Geliştirme dönemi okul dönemine denk geliyor | Modüller birbirinden bağımsız; gerekirse alt modüller dört aylık faza kayar |
| Dil modeli servisi demo sırasında erişilemez olabilir | Kural tabanlı yedek yol yedinci günde tamamlanır |
| GİRVAK'ın gerçek operasyon akışı varsayımımızdan farklı olabilir | Aşama tanımları yapılandırma dosyasında; koda gömülü değil |
| İki kişilik ekipte biri hastalanır | Sabit rol ayrımı yok; her iki geliştirici de tüm katmanlarda çalışıyor |

---

## Takip

Bu plan GitHub Projects panosunda gün bazında kart olarak takip edilir. Haftalar milestone olarak tanımlanmıştır. Her commit CI üzerinden lint ve build kontrolünden geçer; `main` dalına doğrudan push kapalıdır.
