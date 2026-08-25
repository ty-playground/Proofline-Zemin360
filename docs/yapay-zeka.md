# Yapay Zeka Katmanı

## İlke

Sistemin her aşamasında yapay zeka çalışır. Hiçbir aşamada son kararı vermez.

> **Makine hazırlar, insan karar verir, her şey kaydedilir.**

Bu ayrım üç gerekçeye dayanır:

**Hukuki.** Kanun'un 11'inci maddesinin (g) bendi, münhasıran otomatik sistemlerle alınan ve kişi aleyhine sonuç doğuran kararlara itiraz hakkı tanır. Sistem hiçbir tarafı otomatik olarak elemediği, sıralamadığı veya reddetmediği için bu riski tasarımdan çıkarır.

**İstatistiksel.** Programın hedef ölçeği onlarca aktördür. Bu ölçekte bir uyum skoru üretmek gerçekte hiçbir şey ölçmeyen bir sayı üretmek anlamına gelir.

**Kavramsal.** Sistemin tezi, hazırlığın beyanla değil kanıtla gösterilmesidir. Kanıtlanamayan bir skor üretmek bu tezle çelişir.

---

## Aşama aşama kullanım

| Aşama | Yapay zekanın işi | Kararı veren |
|---|---|---|
| İhtiyaç | Olgunluk eleştirisi: eksik alan, ölçülemeyen kriter, belirsiz kapsam tespiti | Kurum |
| İhtiyaç | Benzer geçmiş vakaları bulup uyarı: "bu tipte üç pilot veri erişimi nedeniyle kapandı" | Kurum |
| Vaka | İhtiyaç metninden vaka taslağı önerisi | Kurum |
| Vaka | Gönderilen çözümün rubriğe göre ön incelemesi | Kurum |
| Pilot | Kapsam metninden kilometre taşı taslağı çıkarma | İki taraf |
| Pilot | Risk erken uyarısı: yanıt sürelerindeki bozulmayı işaretleme | Program yöneticisi |
| Kapanış | Sonuç belgesi taslağının derlenmesi | İki taraf |
| Pano | Kapanış nedenlerinden okunabilir ekosistem özeti | — (anonim veri) |
| Pano | Program yöneticisi için dönemsel brifing metni | Program yöneticisi |

---

## Yapmadıkları

- Uyum skoru veya yüzdelik eşleşme oranı üretmez
- Aday sıralaması yapmaz
- Otomatik eleme veya ret kararı vermez
- Bir kurumu veya kişiyi puanlamaz
- Hiçbir alanı kullanıcı onayı olmadan doldurmaz

Eşleştirme bağlamında yapay zeka **karşılaştırma tablosu** üretebilir — hangi kriterin karşılandığı, hangisinin eksik olduğu. Sıralı liste veya skor üretmez. Fark önemlidir: tablo gerekçe gösterir, skor gizler.

---

## Mimari

Tüm çağrılar tek bir yapay zeka servis katmanı üzerinden geçer. Aşamalar bu katmana bağlanır; her aşama kendi sağlayıcısını çağırmaz.

Bunun üç sonucu vardır:

1. **Yedeklilik tek yerde çözülür.** Servis erişilemez olduğunda kural tabanlı karşılıklar devreye girer; sistemin hiçbir aşaması durmaz.
2. **Kişisel veri süzgeci tek yerde uygulanır.** Çağrı öncesinde kişisel veri taraması yapılır; eşleşme bulunursa gönderim engellenir.
3. **Sağlayıcı değiştirilebilir.** Yerel model kullanımına geçiş tek katmanda yapılır.

---

## Kapsam sırası

Hackathon çıktısında yapay zeka üç yerde çalışır:

- İhtiyaç olgunluk eleştirisi
- Risk erken uyarısı
- Pano özeti

Kalan kullanımlar dört aylık geliştirme fazında sırayla devreye alınır. Servis katmanı ilk günden hepsini destekleyecek biçimde kurulur; eksik olan yetenekler değil, açılmamış uçlardır.

---

## Veri koruma

Yapay zeka çağrılarına ilişkin kişisel veri yaklaşımı ve yurt dışına aktarım değerlendirmesi için [`kvkk.md`](kvkk.md) dosyasına bakınız.

Özet: çağrılara kullanıcı kimliği, iletişim bilgisi veya karar verici bilgisi gönderilmez; yalnızca kurumsal problem metni gönderilir. Model çıktısı hiçbir alanı doğrudan doldurmaz.
