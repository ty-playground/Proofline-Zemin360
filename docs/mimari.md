# Mimari

## Tasarım ilkesi

Sistem üç kural üzerine kuruludur:

1. **Makine hazırlar, insan karar verir, her şey kaydedilir.** Hiçbir eşleşme, onay veya karar otomatik verilmez; sistem öneriyi gerekçesiyle sunar, kararı insan verir, karar kaydı tutulur.
2. **Metrik ayrı bir veri girişi değildir.** Bütün ölçümler olay günlüğünden türetilir. Kullanıcı ayrıca hiçbir sayı girmez.
3. **Kayıt silinmez.** Olay günlüğü append-only'dir; düzeltme, yeni bir olay olarak yazılır.

---

## Veri modeli

### Ana varlıklar

| Varlık | Alanlar (özet) |
|---|---|
| **Kurum** | ad, sektör, program |
| **Kişi** | ad, rol, bağlı kurum (varsa) |
| **İhtiyaç** | kurum, dokuz kanvas alanı, olgunluk skoru, durum |
| **Taahhüt** | ihtiyaç, taahhüt tipi, söz verilen süre |
| **Vaka** | ihtiyaç, tanım, rubrik, süre sınırı, çözen, çözüm, değerlendirme durumu |
| **Pilot** | ihtiyaç, taraflar, kapsam, başarı eşiği, karar tarihi, durum, giriş yolu |
| **KilometreTaşı** | pilot, tanım, hedef tarih, kurum onayı, girişim onayı |
| **Olay** | tip, aktör, hedef varlık, zaman damgası, veri |

### İhtiyaç kanvası — dokuz alan

1. Problem
2. Mevcut durum (baseline, sayısal)
3. Ölçülebilir başarı kriteri (şu anki değer → hedef değer)
4. Veri ve sistem erişimi
5. Kısıtlar (güvenlik, uyum, entegrasyon)
6. Bütçe bandı
7. Karar tarihi
8. Karar verici
9. Başarılı olursa sonraki adım

Olgunluk skoru bu alanların doluluk ve ölçülebilirlik durumundan hesaplanır. Üçüncü ve yedinci alanlar sayısal doğrulamadan geçer.

---

## Durum makinesi

### İhtiyaç

```
TASLAK ──[olgunluk ≥ eşik]──► HAZIR ──► YAYIMDA ──► KAPALI
```

`TASLAK → HAZIR` geçişi olgunluk eşiği aşılmadan gerçekleşmez. Bu, sistemin tek sert kapısıdır.

### Pilot

```
AÇIK ──► AKTİF ──[vade doldu]──► KARAR_BEKLİYOR ──┬──► ÖLÇEKLE
                                                   ├──► DURDU
                                                   └──► UZATILDI (bir kez)
```

`KARAR_BEKLİYOR` durumunda yanıt gelmezse durum otomatik `DURDU` olur. Uzatma yalnızca bir kez ve gerekçeyle mümkündür.

### Kilometre taşı

```
AÇIK ──► KURUM_ONAYLADI ──┐
     └─► GİRİŞİM_ONAYLADI ─┴──[her ikisi]──► KAPALI
```

Tek taraflı onay durumu ilerletmez.

### Yapılandırılabilirlik

Aşama adları ve geçiş koşulları koda gömülü değildir; yapılandırma dosyasında tanımlanır. Farklı bir program kendi akışını, kendi eşiklerini ve kendi KPI tanımlarını girebilir.

---

## Olay günlüğü ve metrik türetimi

Her hareket olay günlüğüne yazılır. Metrikler bu günlükten hesaplanır:

| Metrik | Türetim |
|---|---|
| Yanıt süresi | `soru_soruldu` ile `yanıt_verildi` olayları arası fark, ortalaması |
| Değerlendirme süresi | `çözüm_gönderildi` ile `değerlendirildi` olayları arası fark |
| Taahhüt uyumu | Taahhüt edilen süre ile gerçekleşen sürenin karşılaştırması |
| Aşama süresi | Durum geçiş olayları arası fark |
| Kapanış nedeni dağılımı | `pilot_kapandı` olaylarının neden alanına göre gruplanması |
| Giriş yolu başarısı | Vakadan gelen ve doğrudan gelen pilotların sonuç dağılımı |

Bu tasarımın iki sonucu vardır: metrikler sahtelenemez (kullanıcı davranıştan bağımsız bir sayı giremez) ve ayrıca veri girişi gerektirmez (rapor, sistemin yan ürünüdür).

### Takma ad ve silme hakkı

Olay kaydı aktörü doğrudan kimliğiyle değil bir **takma ad referansıyla** saklar; kişisel veriler ayrı bir kayıtta tutulur.

Silme talebi geldiğinde kişi kaydı silinir veya anonim hale getirilir, olay günlüğündeki referans anonim bir değere döner. Zincirin bütünlüğü ve türetilmiş metrikler bozulmaz; silinen kişinin geçmişi artık hiçbir gerçek kişiyle ilişkilendirilemez.

Düzeltme talepleri geçmiş kayıt değiştirilerek değil **yeni bir düzeltme olayı yazılarak** karşılanır. Böylece denetlenebilirlik ile düzeltme hakkı birlikte sağlanır.

---

## Hazırlık paneli

Panel iki kaynaktan beslenir:

**Beyan sütunu** — kurumun kendi işaretlediği alanlar (sponsor, bütçe, veri, karar verici). Öz beyandır; sistem doğruluğunu iddia etmez.

**Ölçüm sütunu** — olay günlüğünden türetilen davranışsal sayılar. Kurumun kendi taahhüdüne göre değerlendirilir.

Sistem yeni bir kurum için ölçüm sütununu boş göstermez, "henüz veri yok" olarak gösterir. Bu da bir bilgidir: karşı taraf geçmişi olmayan bir kurumla çalıştığını bilerek karar verir.

Karşılaştırmalı sıralama üretilmez. Sözünü tutan kurum rozet kazanır; tutmayan yalnızca rozetsiz kalır. Aynı ölçüm girişim tarafında simetrik olarak işler.

---

## Teknoloji

| Katman | Seçim |
|---|---|
| Uygulama | Next.js, TypeScript |
| Veritabanı | PostgreSQL |
| ORM | Drizzle |
| Arayüz | Tailwind CSS, shadcn/ui |
| Dağıtım | Vercel (üretimde self-host edilebilir) |
| Yerel kurulum | Docker Compose |

### Dil modeli kullanımı

Yapay zeka sistemin **her aşamasında** yardımcı olarak çalışır; hiçbir aşamada son kararı vermez. Model hiçbir alanı kendi doldurmaz — öneri üretir, kullanıcı onaylar.

Tüm çağrılar tek bir servis katmanından geçer. Bu sayede üç şey tek yerde çözülür: servis erişilemez olduğunda devreye girecek kural tabanlı karşılıklar, çağrı öncesi kişisel veri süzgeci ve sağlayıcı değişimi.

Aşama bazında kullanım ve sınırlar için [`yapay-zeka.md`](yapay-zeka.md) dosyasına bakınız.

Temel kısıt bilinçlidir: modelin çıktısı hiçbir zaman doğrudan veritabanı gerçeği hâline gelmez.

---

## Kurulum

```bash
git clone <depo>
cd proofline
cp .env.example .env
docker compose up
npm run seed
```

Tohum veri seti sekiz kurum, altı ihtiyaç, yirmi beş vaka çözümü ve üç pilot içerir. Veriler tamamen kurgusaldır; gerçek kurum adı veya kişisel veri içermez.
