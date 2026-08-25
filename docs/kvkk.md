# KVKK Uyumu

Bu doküman, Proofline'ın 6698 sayılı Kişisel Verilerin Korunması Kanunu kapsamındaki yaklaşımını aşama aşama açıklar. Amaç hukuki mütalaa vermek değil, sistemin hangi tasarım kararlarını hangi hukuki gerekçeyle aldığını kayda geçirmektir. Üretim öncesi bir hukuk görüşü alınması öngörülmektedir.

**Uygulanan mevzuat:** 6698 sayılı Kanun (7499 sayılı Kanun ile değişik; değişiklikler 1 Haziran 2024'te yürürlüğe girmiştir) · Kişisel Verilerin Yurt Dışına Aktarılmasına İlişkin Usul ve Esaslar Hakkında Yönetmelik (RG 10.07.2024, S. 32598) · Kişisel Verilerin Silinmesi, Yok Edilmesi veya Anonim Hale Getirilmesi Hakkında Yönetmelik · Kurumun Üretken Yapay Zekâ ve Kişisel Verilerin Korunması Rehberi (Kasım 2025).

---

## 0. Rol dağılımı

| Taraf | Sıfat |
|---|---|
| Programı işleten kurum (Zemin360 kapsamında GİRVAK) | **Veri sorumlusu** |
| Proofline geliştirici ekibi | **Veri işleyen** |
| Barındırma ve altyapı sağlayıcıları | Alt veri işleyen |

Veri sorumlusu ile veri işleyen arasında yazılı bir veri işleme sözleşmesi imzalanması gerekir. Aydınlatma metninin hazırlanması, VERBİS yükümlülüğünün değerlendirilmesi ve ilgili kişi başvurularının yanıtlanması veri sorumlusunun yükümlülüğüdür; sistem bu yükümlülükleri yerine getirmeyi teknik olarak mümkün kılacak biçimde tasarlanmıştır.

VERBİS kayıt yükümlülüğü, Kurul kararlarıyla belirlenen çalışan sayısı ve mali bilanço eşiklerine göre veri sorumlusunun kendi durumuna bağlıdır; yazılımın kendisi bu yükümlülüğü doğurmaz veya ortadan kaldırmaz.

---

## 1. Hukuki dayanak tercihi

Sistem, **açık rızayı varsayılan hukuki sebep olarak kullanmaz.**

Bunun nedeni tercih değil zorunluluktur: Kanun'un 5'inci maddesindeki şartlardan biri mevcutken açık rıza istemek, rızayı hizmetin ön şartına dönüştürür ve rızanın özgür iradeye dayanma niteliğini zedeler. Açık rıza; belirli bir konuya ilişkin, bilgilendirmeye dayalı ve özgür iradeyle verilmiş olmalıdır.

Bu nedenle her işleme faaliyeti için dayanak ayrı ayrı belirlenmiştir:

| Faaliyet | Dayanak (KVKK m.5) |
|---|---|
| Kurum temsilcisi hesabı ve iletişim bilgisi | Sözleşmenin ifası (m.5/2-c) |
| İhtiyaç kanvası içeriği | Sözleşmenin ifası; kurumsal veri ağırlıklı |
| Vaka başvurusu, çözüm, değerlendirme | Sözleşmenin ifası (m.5/2-c) |
| Pilot yürütme kayıtları | Sözleşmenin ifası; hak tesisi (m.5/2-e) |
| Kurum düzeyi davranış metrikleri | Meşru menfaat (m.5/2-f) — denge testiyle |
| Anonim ekosistem istatistikleri | Anonim hale getirildiği için kapsam dışı |
| Kamuya açık profil yayımı | Açık rıza (opsiyonel özellik) |

Açık rıza yalnızca **gerçekten opsiyonel** olan tek bir yerde kullanılır: kişinin doğrulanmış kayıtlarını herkese açık bir profil sayfasında yayımlaması. Bu rıza verilmediğinde sistemin geri kalanı aynen çalışır.

**Özel nitelikli kişisel veri işlenmez.** Kanun'un 6'ncı maddesinde sınırlı sayıda sayılan veriler (sağlık, biyometrik, genetik, ırk, etnik köken, din, dernek/vakıf/sendika üyeliği, ceza mahkûmiyeti vb.) sistemin hiçbir alanında toplanmaz ve serbest metin alanlarında girilmemesi için uyarı gösterilir.

---

## 2. Aşama aşama

### 2.1 İhtiyaç

**İşlenen veri:** Kurum bilgileri (tüzel kişi verisi, Kanun kapsamı dışında), ihtiyaç kanvasının dokuz alanı, karar vericinin adı ve kurumsal iletişim bilgisi.

**Risk:** Serbest metin alanlarına istenmeyen kişisel veri girilmesi. Kurum "X müdürü onay vermiyor" gibi bir cümle yazabilir.

**Tedbirler:**
- Serbest metin alanlarında kişisel veri girilmemesi yönünde alan içi uyarı
- Karar verici alanı için ad ve kurumsal e-posta ile sınırlı; özel iletişim bilgisi istenmez
- Taslak ihtiyaçlar varsayılan olarak yalnızca kuruma görünür
- Anonim vaka kütüphanesine ancak açık onayla ve kişi/kurum adları çıkarılarak girer

---

### 2.2 Hazırlık paneli — **en yüksek riskli aşama**

Bu aşama sistemin en özgün parçası olduğu kadar hukuken en dikkat gerektiren parçasıdır.

**Temel tasarım kararı: metrikler tüzel kişi düzeyinde tutulur, gerçek kişi düzeyinde değil.**

Sistem "Ahmet Bey sorulara geç cevap veriyor" demez; "X Kurumu'nun ortalama yanıt süresi 6 saat" der. Metrik hesaplaması kurum kimliği üzerinden yapılır, kullanıcı kimliği metriğe girmez. Tüzel kişiye ilişkin veriler Kanun'un koruma kapsamı dışındadır; bu ayrım, davranışsal ölçümün kişi profillemesine dönüşmesini engelleyen ana güvencedir.

**Otomatik karar alma sınırı.** Kanun'un 11'inci maddesinin (g) bendi, işlenen verilerin münhasıran otomatik sistemler vasıtasıyla analiz edilmesi suretiyle kişi aleyhine bir sonucun ortaya çıkmasına itiraz hakkı tanır. Sistem bu riski tasarımdan kaldırır:

- Ölçüm sütunu hiçbir kararı otomatik vermez; **gösterir**, karar insana aittir
- Sistem hiçbir tarafı otomatik olarak elemez, sıralamaz veya reddetmez
- Karşılaştırmalı sıralama (leaderboard) üretilmez
- Kurumlar birbirine karşı puanlanmaz; her kurum yalnızca kendi taahhüdüne göre değerlendirilir

**Meşru menfaat denge testi.** Ölçümün dayanağı meşru menfaattir ve bu dayanak bir denge testi gerektirir. Testin sonucu şu unsurlara dayanır:

| Unsur | Değerlendirme |
|---|---|
| Menfaat | Karşı tarafın aylarca sürecek bir sürece girmeden önce gerçek hazırlık durumunu bilmesi |
| Veri türü | Kurumsal süreç verisi; özel nitelikli veri yok, kişi düzeyi yok |
| Beklenti | Kurum taahhüdü kendisi giriyor; ölçüleceğini bilerek giriyor |
| Etki | Kişi üzerinde doğrudan hukuki sonuç doğurmuyor |
| Alternatif | Aynı bilgi daha az müdahaleci bir yolla üretilemiyor |

**Ek güvenceler:**
- Ölçüm dışarıdan dayatılan bir standarda göre değil, kurumun kendi girdiği taahhüde göre yapılır
- Kurum, metriği yayımlanmadan önce kendi panelinde görür ve gerekçe notu düşebilir; not karşı tarafa da görünür
- İlk pilot süresince metrik yalnızca kuruma görünür
- Yanıt olarak sayılma koşulu eyleme dönük olmaktır (veri paylaşımı, onay, karar); yalnızca "aldım, bakıyorum" mesajı metriği düşürmez
- Aynı ölçüm girişim tarafında simetrik olarak işler

---

### 2.3 Vaka

**İşlenen veri:** Başvuranın adı, iletişim bilgisi, teslim ettiği çıktı, kurum onayı, süre bilgisi.

**Tedbirler:**
- Gerçek müşteri verisi veya üretim verisi kullanılan görev açılamaz; görev tanımında bu kural hatırlatılır
- Teslim edilen çıktının fikri mülkiyeti katılımcıda kalır
- Değerlendirme ölçütü (rubrik) başvuru öncesinde görünür
- Görev süresi üst sınırla kısıtlıdır; üretimde doğrudan kullanılabilir tam çözüm talep edilemez
- Reddedilen başvurulara ait veriler tanımlı bir süre sonunda silinir

Bu kurallar yalnızca hukuki değil etik gerekçeye de dayanır: ücretsiz görev akışının karşılıksız iş gücüne dönüşmemesi gerekir. Dört aylık geliştirme fazında ücretlendirme altyapısı planlanmıştır.

---

### 2.4 POC

**İşlenen veri:** İki taraftan isimli sorumluların adı ve kurumsal iletişim bilgisi, kilometre taşı onayları, karar kayıtları.

**Tedbirler:**
- Yalnızca kurumsal iletişim bilgisi; özel telefon veya adres istenmez
- Pilot içeriği taraflar ve program yöneticisi dışında görünmez
- Kapanış nedeni serbest metin değil, önceden tanımlı seçenek listesidir — bu, kişi hakkında olumsuz serbest yorum yazılmasını yapısal olarak engeller

---

### 2.5 Olay günlüğü — silme hakkıyla gerilim

Sistem, ekleme-esaslı (append-only) bir olay günlüğü tutar; kayıtlar geriye dönük değiştirilmez. Bu, Kanun'un 7'nci maddesindeki silme ve yok etme yükümlülüğüyle ilk bakışta çelişir.

**Çözüm: günlük kişisel veri taşımaz, takma ad taşır.**

Olay kaydı aktörü doğrudan kimliğiyle değil, bir aktör referansıyla saklar. Kişisel veriler ayrı bir kayıtta tutulur. Silme talebi geldiğinde:

1. Kişi kaydı silinir veya anonim hale getirilir
2. Olay günlüğündeki referans anonim bir değere döner
3. Zincirin bütünlüğü ve türetilmiş metrikler bozulmaz
4. Silinen kişinin geçmişi artık hiçbir gerçek kişiyle ilişkilendirilemez

Aynı şekilde düzeltme talepleri, geçmiş kaydı değiştirerek değil **yeni bir düzeltme olayı yazarak** karşılanır. Böylece hem denetlenebilirlik hem düzeltme hakkı birlikte sağlanır.

Saklama süreleri veri kategorisi bazında tanımlanır ve bir saklama ve imha politikasında yazılı hale getirilir. Süresi dolan kayıtlar için periyodik imha uygulanır.

---

### 2.6 Pano ve raporlar

Panodaki bütün toplu istatistikler anonim hale getirilmiş verilerden üretilir. Anonim hale getirilmiş veri Kanun kapsamı dışındadır; ancak anonimleştirmenin gerçek olması gerekir.

**Yeniden kimliklendirme riskine karşı eşik kuralı:** Bir istatistik, arkasındaki kayıt sayısı belirlenen eşiğin altındaysa gösterilmez. On kurumun bulunduğu bir programda "pilotların %40'ı veri erişimi nedeniyle kapandı" ifadesi, kayıt sayısı düşükse tek bir kurumu işaret edebilir. Sistem bu durumda istatistiği gizler.

Dışa aktarılan raporlar kişi adı içermez.

---

## 3. Yapay zeka kullanımı ve yurt dışına aktarım

Sistem yapay zekayı her aşamada yardımcı olarak kullanır; tüm çağrılar tek bir servis katmanından geçer ve kişisel veri süzgeci bu katmanda uygulanır.

Türkiye'de yerleşik bir veri sorumlusunun kişisel veri içeren istemleri yurt dışındaki bir sağlayıcıya göndermesi, Kanun'un 9'uncu maddesi kapsamında yurt dışına aktarım sayılır. 7499 sayılı Kanun ile değişik 9'uncu madde uyarınca aktarım için yeterlilik kararı, bunun yokluğunda standart sözleşme veya bağlayıcı şirket kuralları gibi uygun güvencelerden birinin bulunması gerekir; usul ve esaslar 10.07.2024 tarihli Yönetmelik ile düzenlenmiştir.

**Tedbirler:**
- Dil modeline yalnızca ihtiyacın **kurumsal problem tanımı** gönderilir; kullanıcı kimliği, iletişim bilgisi ve karar verici bilgisi gönderilmez
- Gönderim öncesi kişisel veri süzgeci uygulanır; süzgeç bir eşleşme bulursa gönderim engellenir ve kullanıcı uyarılır
- Model çıktısı hiçbir alanı doğrudan doldurmaz; öneri üretir, kullanıcı onaylar — bu, çıktının doğruluğunu denetleme yükümlülüğünün karşılığıdır
- Sağlayıcıyla veri işleme sözleşmesi bulunmadan üretim kullanımı yapılmaz
- Dört aylık geliştirme fazında yerel model seçeneği değerlendirilir; bu durumda yurt dışına aktarım tamamen ortadan kalkar
- Servis devre dışıyken kural tabanlı kontrol listesi çalışır, yani sistem dil modeli olmadan da işlevini korur

Kurumun Üretken Yapay Zekâ ve Kişisel Verilerin Korunması Rehberi'nde ortaya konan yaklaşım esas alınır.

---

## 4. Dört aylık fazda planlanan e-Devlet doğrulaması

Dört aylık geliştirme fazında belge doğrulaması planlanmaktadır. Bu, mevcut kapsamın dışındadır ve ek yükümlülük doğurur.

**Tasarım ilkesi:** Doğrulama kullanıcı aracılıdır. Sistem herhangi bir kamu veri tabanına doğrudan erişmez; kişi kendi belgesini kendisi üretir ve doğrulama sürecini kendisi başlatır.

**Veri minimizasyonu:** Belgenin kendisi saklanmaz. Yalnızca doğrulama sonucu kaydedilir: doğrulandı bilgisi, kaynak ve tarih. Belgenin içeriğindeki diğer kişisel veriler işlenmez.

**Kapsam sınırı:** Özel nitelikli kişisel veri içerebilecek belge türleri doğrulama akışına dahil edilmez.

**Ön koşul:** Bu özellik, ayrı bir aydınlatma metni ve hukuk görüşü olmadan devreye alınmaz.

---

## 5. Teknik ve idari tedbirler

| Alan | Tedbir |
|---|---|
| Erişim | Rol bazlı yetkilendirme; her kullanıcı yalnızca tarafı olduğu kayıtları görür |
| Aktarım | Uçtan uca şifreli bağlantı |
| Saklama | Şifreli veri tabanı; yedeklerin şifrelenmesi |
| İzleme | Yönetici erişimlerinin kaydı |
| Geliştirme | Üretim verisiyle geliştirme yapılmaz; tohum veri seti tamamen kurgusaldır ve gerçek kurum adı içermez |
| Sızıntı | İhlal bildirimi süreci `SECURITY.md` dosyasında tanımlıdır |
| Silme | Saklama ve imha politikası uyarınca periyodik imha |

---

## 6. İlgili kişi haklarının teknik karşılığı

Kanun'un 11'inci maddesindeki her hak için sistemde bir karşılık bulunur:

| Hak | Sistemdeki karşılığı |
|---|---|
| Bilgi talep etme | Hesap üzerinden kendi verilerini görüntüleme |
| Amacı öğrenme | Aydınlatma metni ve alan bazlı açıklamalar |
| Aktarılan üçüncü kişileri bilme | Alt işleyen listesi dokümantasyonda yayımlanır |
| Düzeltme | Düzeltme talebi yeni bir olay olarak yazılır |
| Silme / yok etme | Kişi kaydı silinir, olay günlüğü anonimleşir |
| Otomatik analize itiraz | Sistem münhasıran otomatik olumsuz karar üretmez; her karar aşamasında insan onayı bulunur |

---

## 7. Açık konular

Dürüstlük gereği, bu tasarımın henüz kapatılmamış noktaları:

1. Meşru menfaat denge testinin yazılı ve tarihli biçimde belgelenmesi gerekir; taslak hazırlanmıştır, hukuk görüşüyle kesinleştirilecektir.
2. Saklama sürelerinin veri kategorisi bazında sayısallaştırılması, veri sorumlusunun kurumsal politikasıyla uyumlu olmalıdır.
3. Anonim istatistik eşik değeri, gerçek kullanım hacmine göre kalibre edilecektir.
4. Yurt dışı aktarım güvencesinin hangi yöntemle sağlanacağı, seçilecek sağlayıcıya göre belirlenecektir.
5. Aydınlatma metni ve veri işleme sözleşmesi taslakları dört aylık fazın ilk ayında tamamlanacaktır.

Bu doküman bir hukuk görüşü değildir; sistemin hangi tasarım kararlarını hangi gerekçeyle aldığını gösterir ve hukuk görüşü alınırken temel oluşturmak üzere hazırlanmıştır.
