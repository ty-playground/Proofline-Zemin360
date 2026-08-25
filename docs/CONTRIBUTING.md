# Katkıda Bulunma

Proofline açık kaynak bir projedir. Katkılar hata bildirimi, dokümantasyon düzeltmesi, öneri veya kod olarak gelebilir.

## Geliştirme ortamı

```bash
git clone https://github.com/ty-playground/Proofline-Zemin360.git
cd Proofline-Zemin360
cp .env.example .env
docker compose up -d
npm install
npm run db:migrate
npm run seed
npm run dev
```

Uygulama `http://localhost:3000` adresinde çalışır. Tohum veri seti tamamen kurgusaldır; gerçek kurum adı veya kişisel veri içermez.

## Dal ve commit

`main` dalına doğrudan gönderim kapalıdır. Değişiklikler bir dalda yapılır ve pull request ile birleştirilir.

Dal adları: `feat/ihtiyac-kanvasi`, `fix/vade-hesabi`, `docs/kvkk-guncelleme`

Commit mesajları konvansiyonel biçimdedir:

```
feat: ihtiyaç olgunluk skoru hesaplayıcı
fix: vade sayacı hafta sonlarını atlamıyor
docs: KVKK dokümanına saklama süreleri eklendi
refactor: olay günlüğü yazma katmanı ayrıştırıldı
test: çift taraflı onay senaryoları
chore: bağımlılık güncellemesi
```

## Pull request

Bir PR şunları içermelidir:

- Ne değiştiğinin kısa açıklaması
- İlgili issue numarası (varsa)
- Arayüz değişikliği varsa ekran görüntüsü
- Yeni davranış varsa test

CI kontrolleri (lint, tip kontrolü, build) geçmeden birleştirme yapılmaz. En az bir onay gerekir.

## Tasarım ilkeleri

Katkılar aşağıdaki ilkeleri bozmamalıdır. Bunlar tercih değil, sistemin temelidir:

**1. Makine hazırlar, insan karar verir, her şey kaydedilir.**
Hiçbir özellik münhasıran otomatik olarak bir tarafı elemez, sıralamaz veya reddetmez. Yapay zeka öneri üretir; kararı kullanıcı verir.

**2. Ölçüm olay günlüğünden türetilir.**
Metrikler ayrı bir alana yazılmaz. Kullanıcının doğrudan girebildiği bir metrik, sahtelenebilir bir metriktir.

**3. Olay günlüğü değiştirilemez.**
Geçmiş kayıtlar güncellenmez veya silinmez. Düzeltme, yeni bir olay yazılarak yapılır.

**4. Metrikler tüzel kişi düzeyindedir.**
Gerçek kişi puanlanmaz, sıralanmaz veya profillenmez.

**5. Aşama tanımları yapılandırmadadır.**
Durum adları ve geçiş koşulları koda gömülmez; farklı programlar kendi akışını tanımlayabilmelidir.

**6. Kapsam dışı olanlar kapsam dışıdır.**
Eşleştirme algoritması, uyum skoru, mesajlaşma, sosyal akış, blok zinciri ve rozet/puan mekanikleri bilinçli olarak yapılmamaktadır. Bu alanlarda katkı önerisi getirmeden önce bir issue açıp tartışılması beklenir.

## Kişisel veri

Kişisel veri işleyen bir katkı gönderiyorsanız [`docs/kvkk.md`](docs/kvkk.md) dosyasını okuyun. Yeni bir veri alanı ekliyorsanız PR açıklamasında hukuki dayanağını ve saklama süresini belirtin.

Test ve geliştirme yalnızca tohum veri seti ile yapılır; gerçek veri kullanılmaz.

## Güvenlik

Güvenlik açığı bildirimleri için [`SECURITY.md`](SECURITY.md) dosyasına bakınız. Güvenlik açıklarını herkese açık issue olarak bildirmeyin.

## Karar süreci

Mimari değişiklikler ve kapsam kararları için [`GOVERNANCE.md`](GOVERNANCE.md) dosyasına bakınız.
