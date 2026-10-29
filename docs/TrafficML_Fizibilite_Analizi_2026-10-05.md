# TrafficML veri ve pilot fizibilitesi

5 Ekim 2026

## Karar özeti

TrafficML'nin küçük bir yol ağı üzerinde alternatif tasarımları simüle eden ve simülasyon sonuçlarından öğrenen yazılımı teknik olarak geliştirilebilir. Ankara'da gerçek trafik davranışını temsil eden ve fiziksel veya sinyal müdahalelerini güvenilir biçimde değerlendiren ürün için ise gerekli veri paketi henüz doğrulanmış değildir. Şehir çapında, çok modlu ve sürekli güncellenen sistem bugünkü kanıtla taahhüt edilemez.

Ankara'dan vazgeçmek için erken; bütün kapsamı Ankara'da gerçekleştirebileceğimizi söylemek için de erken. Yeni bir seçenek var: TomTom Traffic Stats Traffic Volume belgesi Türkiye için belirli yol sınıflarında geçmiş toplam araç geçişi tahminlerini listeliyor. Bu, standart Flow Segment Data hizmetinden ayrı bir üründür. Helsinki ise sensör çeşitliliği ve belediyenin coğrafi verileri nedeniyle güçlü bir araştırma adayıdır; sinyal planları, dönüş eşlemesi, yaya verisinin seçilen kavşakla örtüşmesi ve gözlem indirme güvenilirliği ayrıca doğrulanmalıdır.

Benim değerlendirmem: proje için devam kararı verilebilir; gerçek şehir pilotu için karar, belirli bir alanda alınmış ve incelenmiş örnek veriye bağlanmalıdır. İlk araştırma çıktısının savunulabilir kapsamı, küçük bir ağda tanımlı sinyal ve fiziksel düzenlemelerin karşılaştırılması ve ML'nin aday seçimine katkısının ölçülmesidir.

## İncelenen malzeme ve kanıt düzeyi

Downloads altındaki TrafficML_Rapor_Paketi_v0.1/TrafficML_Rapor_Paketi klasöründe README, özet, sekiz ana raporun Markdown kaynakları, kaynak kataloğu, araştırma sınırları, 37 gereksinimin izlenebilirliği ve üç Mermaid şeması incelendi. Word ve PDF sürümleri paket tarafından aynı içeriklerin sunum sürümleri olarak tanımlanıyor; bunları birbirinden bağımsız araştırma kanıtları olarak saymadım. Gereksinim JSON'unda 37 farklı FR kimliği ve her biri için kabul metni bulunuyor.

Bu sohbetin yerel sources/ klasörü inceleme sırasında boştu. Paketin dayandığı K01 özgün FR PDF'si, K02 özgün ön araştırması ve K03 arayüz görseli ayrı özgün dosyalar olarak erişilebilir değildi. Onlara ilişkin değerlendirme, paketteki aktarımlara dayanıyor; özgün metinlerle bağımsız karşılaştırma yapıldığı iddia edilmiyor.

Kanıtları üç düzeyde değerlendirdim:

- **Belge kanıtı:** Resmî açıklama veya API şeması gereken alanı tanımlıyor.
- **Erişim kanıtı:** Gerçek bir istekle kaynak, sensör veya veri kaydı alınabiliyor.
- **Pilot yeterliliği:** Verinin seçilen alan, zaman, hareket ve kalite ihtiyacını birlikte karşıladığı gösteriliyor.

İlk iki düzey, üçüncünün yerine geçmez. Bu çalışma kapsamında ücretli TomTom/HERE hesabıyla Ankara sorgusu, simülasyon, model eğitimi veya saha ölçümü yapılmadı. Helsinki'de metadata erişimi, Digitraffic'te metadata ve ölçüm erişimi denendi; aşağıda sonuçları ayrıldı. Kaynak raporlar değiştirilmedi.

## Rapor paketinin değerlendirmesi

Paketin güçlü tarafı, gözlem, varsayım, kestirim ve simülasyon çıktısını ayırmasıdır. Mevcut düzen ile alternatiflerin ortak dış talep altında değerlendirilmesi, topoloji değişince eski durum kaydının doğrudan kullanılamayacağının belirtilmesi, bitmeyen yolculukların sonuçlarda tutulması ve ML'nin son adayları yeniden simülasyona göndermesi doğru bir araştırma çerçevesi oluşturuyor. FR-20'nin tasarım performansı tahmini olarak korunması da önemli: gelecek trafik tahmini ile başka bir yol tasarımının etkisini tahmin etmek farklı görevlerdir.

Ancak paket, uygulanabilirlik ispatı değil, araştırma ve tasarım önerisidir. Sekiz rapor, 36 kaynak ve 37 gereksinimin bulunması; yerel veri edinildiğini, çalışan model bulunduğunu veya süre/bütçenin yeterli olduğunu göstermiyor. Tasarım kabul maddeleri ile gerçekleştirilmiş test sonuçlarını ayırmak gerekir.

Karar vermeden önce şu noktalar güncellenmelidir:

| Paketteki konu | Bu incelemenin değerlendirmesi |
|---|---|
| Ankara öncelikli, 3–5 bağlantılı kavşak | Başlangıç tercihi olabilir; veri erişimi ve saha ölçümü kapasitesi görülmeden pilot büyüklüğü sabitlenmemeli. Tek kavşakla başlanırsa dahi kuyruk ve komşu etki alanı kapsanmalı. |
| TomTom Flow Segment Data | Bu uç noktanın hız ve seyahat süresi kapsamı doğru aktarılmış. Ancak TomTom'un bütün ürünleri için araç sayısı bulunmadığı sonucu çıkarılmamalı; Traffic Volume ayrı değerlendirilmelidir. |
| Gerçek veri doğrulamasının M2'de derinleşmesi | Gerçek şehir iddiası hedefleniyorsa veri ve mevcut durum doğrulaması büyük geliştirme yatırımından önce karar kapısı olmalı. Sentetik yazılım çalışması bu kapıdan bağımsız ilerleyebilir. |
| M1'de sinyal, fiziksel şablon, metrikler ve 3D | Birden fazla zor işi birlikte içeriyor. Ekip ve takvim bilinmeden tamamına süre taahhüdü verilemez. Sade 3D yeterli; fotogerçekçi çevre ilk kanıtı güçlendirmiyor. |
| 20 tasarım × 3 talep × 5 tekrar = 300 koşu | 300 ayrı tasarım değildir: 20 tasarım, 60 tasarım-talep birleşimi ve tekrarlarıdır. Bu iş yükü önerisi eğitim yeterliliği veya şehirler arası genelleme kanıtı sayılmamalı. |
| Olası neden analizi | Hızdan kesin kök neden çıkarımı yapılamaz. İlk hipotezler sayım, sinyal ve kuyruk gözlemi bulunabildiği ölçüde sınanabilir. |
| Fiziksel uygulanabilirlik ve maliyet | Harita üzerindeki boşluk, kullanılabilir yol kesiti veya mülkiyet hakkı anlamına gelmez. Yaklaşık metraj hesabı ile uygulama keşfi farklı sonuçlardır. |

## Hangi ürün için hangi veri gerekir

Trafik verisine ilişkin sorunu tek bir liste olarak görmek yanıltıyor. Gereken veri, verilecek kararın türüne bağlıdır.

| Hedef | Veri ve yöntem ihtiyacı | Bugünkü karar |
|---|---|---|
| Yoğunluk ve hız izleme | Yol segmenti, zaman, hız/seyahat süresi veya sağlayıcının sıkışıklık göstergesi | Ankara için mevcut akışınız ve uygun API kapsamıyla ilerlenebilir; alan ve zaman kalitesi denetlenmeli. |
| Kısa vadeli hız veya trafik durumu tahmini | Yeterli süreli ve tutarlı gözlem serisi; zaman sıralı bağımsız değerlendirme | Koşullu olarak yapılabilir. Sadece anlık görüntüler arşivlenmemiş geçmiş eğitim verisi oluşturmaz. |
| Sinyal düzenlemesini değerlendirme | Şerit ve hareket eşlemesi, zamana bağlı giriş/dönüş talebi, mevcut kontrol, kuyruk veya seyahat gözlemi | Ankara'da kritik girdiler açık; Helsinki'de de sinyal planı tamamlanmış değil. |
| Şerit veya kavşak geometrisini değiştirme | Önceki veriler + dönüş cebi ve bağlantılar, kesit ve müdahale kısıtları, rota varsayımları | Küçük ve doğrulanmış pilotta mümkün; yalnız hız API'siyle güvenilir saha önerisi üretilemez. |
| Yaya ve bisiklet etkisini değerlendirme | İlgili geçitlerin talebi, yönleri, süreleri ve araçlarla etkileşim modeli | Haritada geçit/bisiklet yolu bulunması yeterli değil. |
| Simülasyon sonuçlarından öğrenen ML | Geçerli simülasyon, tanımlı tasarım uzayı, çeşitlilik ve grup ayrımlı test | Gerçek şehir verisi eksik olsa da yöntem araştırması yapılabilir; sonuçların geçerliliği simülasyon varsayımlarıyla sınırlıdır. |
| Şehir çapında sürekli dijital ikiz | Geniş alanlı güncel talep ve kontrol, bakım, entegrasyon ve sürekli doğrulama | Bu kaynakların bulunması tek başına bu kapsama yetmiyor. |

Hız, akış ve yoğunluk farklı ölçülerdir. Araç/saat akış; araç/km yoğunluk; km/saat hızdır. Sağlayıcının renk veya jamFactor ölçeği bunlardan birine otomatik dönüşmez. Aynı düşük hız, fazla talep, kısa yeşil, aşağı akım tıkanması veya başka bir işletim koşulunda oluşabilir. Hız tek başına bu durumları ayırt etmez.

## Veri eksiklerinin önceliği

| Veri | İlk gerçek trafik pilotundaki rolü | Eksikse savunulabilir davranış |
|---|---|---|
| Giriş ve hareket bazlı araç sayısı | Talebin ölçeğini ve yön dağılımını kurmak için kritik | Tahmin/varsayım senaryoları yapılabilir; gerçek talep doğrulanmış sayılmaz. |
| Dönüş sayımları ve şerit bağlantıları | Dönüş cebi ve kavşak alternatifleri için kritik | Toplam yol sayımı dönüş oranlarına tek başına dönüşmez; oran duyarlılığı raporlanır. |
| Sinyal fazları, süreleri ve kontrol türü | Sinyalize pilotun mevcut düzeni için kritik | Varsayımsal sinyal deneyi yapılır; mevcut şehrin iyileştirmesi olarak sunulmaz. |
| Kuyruk veya koridor seyahat gözlemi | Modelin mevcut durumu temsil ettiğini sınamak için kritik | Ayrı gözlem bulunmadan saha geçerliliği kabul edilmez. |
| Araç türü dağılımı | Ağır araç, otobüs ve boşalma davranışı için önemli | Varsayım açık tutulur, farklı karışımlarla sonuç duyarlılığı ölçülür. |
| Yaya/bisiklet hareket ve talebi | Bu grupların etkisi raporlanacaksa kritik | Envanter/görsel çıktı yapılabilir. İşletim karşılaştırmasında göz ardı edilen etki bir sınırlılık olarak kalır. |
| Yol kesiti ve müdahale alanı | Fiziksel alternatifin model içinde uygunluğuna ve metraja temel | Yalnız uzman/veri incelemesi bekleyen alternatif sunulur. |
| Bina ayak izleri ve yükseklik | İlk gecikme modelinde çoğunlukla ikincil; çevre ve alan kısıtında yararlı | Sade çevre kullanılabilir. Bina yokluğu bilgisiyle arazi kullanılabilir ilan edilmez. |
| Arazi yükseltisi | Eğim, köprü ve çevre bağlamı için yararlı | Çalışma amacı gerektiriyorsa ayrıntılı yükselti aranır; geniş ölçekli raster şerit ölçümü yerine geçmez. |
| Arazi kullanımı ve mülkiyet | Talep üretimi veya inşa edilebilirlik hedefinde önem kazanır | Anlık kavşak talebi doğrudan ölçülüyorsa ayrıntılı şehir arazi kullanımı ilk zorunluluk olmayabilir. |

Bütün binaların veya bütün şehrin arazi verisinin eksikliği ilk simülasyon çalışmasını tek başına durdurmaz. Talep, kontrol ve bağımsız doğrulama eksikleri ise verilecek trafik kararını doğrudan sınırlar. Yaya talebi, sayısal çıktı olarak gösterilmese bile sinyal hizmetini etkileyebileceğinden, etkili bir pilotta yok sayılmamalıdır.

## Kaynakların somut katkısı

### Yandex ve mevcut yoğunluk akışı

Kullanıcı mevcut yoğunluk verisini aldığını belirtiyor; paket içinde bu akışın örnek kaydı veya veri sözleşmesi bulunmuyor. Bu nedenle hız, zaman çözünürlüğü, gerçek ölçüm zamanı, segment yönü, geçmiş saklama ve kullanım koşulları bu incelemede doğrulanmış değildir. İlk sorulacak teknik soru, "Yandex var mı?" yerine "hangi alanları, hangi yol kesiti ve hangi zamanda alıyoruz?" olmalıdır.

Bu verinin uygun rolü, yavaşlayan kesimleri ve zaman düzenini gözlemek, veri uygunsa seyahat/hız karşılaştırmasına katkı vermektir. Araç sayısı, otomobil/ağır araç oranı, yaya hareketi veya sinyal programı örnek şemada açıkça yoksa, yoğunluk göstergesinden var sayılmamalıdır.

### TomTom

**Flow Segment Data:** En yakın yol fragmenti için hız ve seyahat süresi ile serbest akış değerleri ve kalite alanları tanımlanıyor. Standart şema araç/dönüş sayımı ve sinyal fazı sunmuyor. Ankara'da hangi fragmentin ve yönün seçildiği denetlenmeli. [Resmî Flow Segment Data belgesi](https://docs.tomtom.com/traffic-api/documentation/tomtom-maps/v1/traffic-flow/flow-segment-data).

**Traffic Stats Traffic Volume:** 24 Eylül 2026 tarihli belge, geçmiş toplam araç geçişlerini modelle kestiren ayrı servisi ve Türkiye'de 2024'ten itibaren FRC 0–3 kapsamını listeliyor. Türler birlikte veriliyor; zaman pencereleri tam saat sınırlarıyla seçiliyor. Ankara'nın belirli küçük yolları için erişim kanıtı veya sayaç ölçümü olduğu sonucu çıkarılamaz. [Resmî Traffic Volume belgesi](https://docs.tomtom.com/traffic-stats/documentation/api/traffic-volume).

**O/D Analysis v2:** Seçilen bağlantı çevresindeki yolculuk dağılımlarını araştırmak için ilgili bir ürün. VOLUME geliştirmesi de model tahmini; uygun harita, dönem ve tek segment koşulları bulunuyor. Örneklemde görülen yolculuk sayısı ile toplam trafik tahmini ayrı alanlar olarak okunmalı. [Selected Link sonuç açıklaması](https://docs.tomtom.com/od-analysis/documentation/v2/user-guide/selected-link-analysis/view-report/link-results), [analiz koşulları](https://docs.tomtom.com/od-analysis/documentation/v2/analysis/selected-link-analysis/analysis-creation).

Dokümantasyonda ayrıca bir uyumsuzluk var: Historical Traffic Volumes genel kapsam sayfasındaki daha kısa ülke listesi Türkiye'yi göstermiyor, Traffic Stats Traffic Volume sayfası ise gösteriyor. Bu farkın nedeni bu incelemede doğrulanmadı. Ankara için erişim kararı, genel ürün adına değil tam servis, yol, dönem ve hesap yetkisine bağlanmalı. [Genel kapsam listesi](https://docs.tomtom.com/historical-traffic-volumes/documentation/product-information/market-coverage).

Projeye çıkarımım: Ankara'da toplam yol talebine başlangıç kestirimi edinme ihtimali önceki paketin aktardığından daha güçlü. Buna karşılık tahmin edilmiş toplam geçiş, ölçülmüş kavşak dönüşleri ve mevcut sinyal işletimini karşılamıyor. Bu incelemede ücretli sorgu çalıştırılmadı; kota, fiyat ve kullanım koşulları kesinleştirilmedi.

### HERE

Traffic API v7 Flow; hız, serbest akış hızı, jamFactor, geçilebilirlik ve confidence alanlarını tanımlıyor. Hızlar m/s; jamFactor 0–10 ölçeğinde. Confidence hız bilgisinin gerçek zamanlı veya tarihsel kökenini ayırmak için anlam taşıyor. Gelişmiş şerit verisi ayrı özellik ve kapsam gerektiriyor. [Resmî HERE Flow belgesi](https://docs.here.com/traffic-api/docs/flow).

Bu servisi Ankara'nın hız ve sıkışıklık gözlemi için aday olarak değerlendiriyorum. Standart Flow şemasını araç sayacı, araç türü ayrımı veya sinyal programı sağlayan servis gibi kullanmak doğru değil. Şerit düzeyinde hız bulunması da şerit düzeyinde talep veya dönüş sayımı bulunduğunu göstermez. Anahtarlı Ankara kapsamı test edilmedi.

### Digitraffic

Finlandiya'nın TMS/LAM kaynakları, gerçek sensörlerden araç geçişi ve hız verisi sağlar. Ham kayıt şeması zaman, yön, şerit, hız, uzunluk, araç sınıfı ve hata bayrağını içerir. Bazı akış alanları son beş dakikalık geçişlerin saatlik orana dönüştürülmüş halidir; doğrudan beş dakikalık sayı gibi okunmamalı. [TMS/LAM belgeleri](https://www.digitraffic.fi/en/road-traffic/lam/), [yol trafiği servisleri](https://www.digitraffic.fi/en/road-traffic/).

Erişim yalnız belge üzerinden değerlendirilmedi. 20002 numaralı Espoo Hirvisuo istasyonundan 5 Ekim tarihli güncel hız ve geçiş alanları alındı. 4 Ekim 2026'ya ait günlük ham dosya da indirildi: **29.879 kayıt; kaynak hata bayrağına göre 29.805 geçerli ve 74 hatalı kayıt**. Bu, sınıflı ve zamanlı veriye gerçek erişim kanıtıdır; istasyonun temsiliyeti veya kapsamlı kalite onayı değildir. [Güncel ölçüm uç noktası](https://tie.digitraffic.fi/api/tms/v1/stations/20002/data), [indirilen günlük ham kaynağı](https://tie.digitraffic.fi/api/tms/v1/history/raw/lamraw_20002_26_277.csv).

Önce yakınlığa göre seçilen 20028 istasyonunun örneğinde güncel zaman damgasına rağmen değerler sıfırdı; pilot uygunluğu kabul edilmedi. Bu örnek, "servis yanıt verdi" ile "veri işe yarıyor" ayrımının neden gerekli olduğunu gösteriyor.

Digitraffic Ankara verisi sağlamaz. Helsinki yakınındaki devlet/ana yol sayımlarının başka bir kentsel kavşağın bütün giriş, dönüş ve yaya ihtiyaçlarını karşıladığı da varsayılamaz. Uygun istasyonla hız/akış/sınıf araştırması için güçlü; sinyal optimizasyonu için eksiksiz paket olarak değerlendirilmemeli.

### Helsinki LIDO-TIKU

OpenAPI şeması, kaynak açıklamaları ve sensör kataloğu doğrudan alındı. Şema count/speed gözlemleri, süre, araç türü, yön, birim, değer, tarih ve counter alanlarını tanımlıyor. Açık uç noktalar sensörler, kaynaklar, gözlemler ve toplulaştırılmış gözlemler için; bu şemada faz/sinyal planı uç noktası görülmedi. Lisans CC BY 4.0 olarak belirtiliyor. [Swagger](https://lidotiku.api.hel.fi/swagger), [kaynak açıklamaları](https://lidotiku.api.hel.fi/api/metadata/sources/?format=json&language=en).

Kaynakların işlevi aynı değil:

| Alt kaynak | Belgelenen veri | Pilot için önemli sınır |
|---|---|---|
| SmartJunction | Sanal dedektörlerle sayım, hız, ivme ve sınıflandırma; geliş/gidiş şerit bilgileri | Belirli Jätkäsaari çevresi; radar/şerit/hareket eşlemesi kontrol edilmeli. |
| LIVA | Sinyalize kavşakların loop dedektör sayımları, 15 dakikalık aralık | Metadata yön gruplamasının ve güvenilirliğin değişken olduğunu belirtiyor; sinyal fazı verisi değil. |
| HEL LAM | Belediyenin sayım ve bazı cihazlarda hız/sınıf verisi | Her cihazın aynı alanları vermesi beklenmemeli. |
| Fintraffic | Ana yol LAM ölçümleri, saatlik sayım/hız | Başka konumların kaydı kentsel pilotla doğrudan birleştirilmemeli. |
| EcoCounter | Yaya ve bisiklet sayımı | Kaynak açıklamasında yön ayrımı yok; belirli kavşak geçitlerine eşitlenemez. |
| Marksman ve InfoTripla | Tarihsel kaynaklar | Aktif günlük veri kaynağı olarak varsayılmamalı. |

Belediyenin 30 Ekim 2025 sunumu da farklı alt kaynakların çözünürlük ve kapsama sahip olduğunu gösteriyor. Sunumdaki sensör/kavşak sayıları güncel envanter sayısı diye kullanılmadı. [Belediye teknik sunumu](https://www.hel.fi/static/avoindata/dokumentit/tapahtumat/2025-10_HRI_Loves_Dev_Liikenne_ja_liikkuminen/Kurtto_Jonas_LIDO-TIKU-projekti.pdf).

Bu incelemedeki metadata bulguları:

- SmartJunction 4255 sensörü için son kayıt zamanı 4 Ekim 2026 23.45 olarak listeleniyor. Bu, gözlemin indirildiği anlamına gelmez.
- HEL LAM 4667 kaydı için de 4 Ekim 2026 tarihli son gözlem metadata'sı görüldü.
- Alınan LIVA envanterindeki son gözlem zamanlarının en ilerisi 5 Mart 2026'ydı. Güncel sinyal kavşağı akışı olarak kabul edilmedi.
- EcoCounter katalog kayıtlarında bu anlık görüntüde gözlem tarih alanları boştu. Yaya kaynağının varlığı belgeyle destekli, indirilebilir çalışma dönemi ise doğrulanmamış durumda.
- Sayfalı katalog toplam 3.571 satır bildirdi. Alınan kayıtlarda bazı sayısal ID'ler farklı kaynak isimlerinde tekrarlandı; tek başına ID'nin küresel benzersizliği varsayılmamalı. Kaynak, kimlik ve fiziksel eşleme birlikte doğrulanmalı. Satır sayısı fiziksel kavşak sayısı değildir.

Gözlem sorguları zaman aşımı/503 hatası verdi. Seçilmiş sensör ve tek günle daraltılmış iki sorgu da 503 ile sonuçlandı. Bu nedenle LIDO-TIKU için **belge ve katalog erişimi doğrulandı; bu oturumda gözlem dosyası erişimi doğrulanamadı**. Geçici hata, verinin bulunmadığının kanıtı değildir; pilotun bugün hazır olduğunun kanıtı da değildir. Örnek veri alınmadan Helsinki'yi kesin pilot olarak seçmem.

### QGIS ve coğrafi katmanlar

QGIS; vektör, raster ve diğer coğrafi katmanların görüntülenmesi, eşlenmesi ve analiz edilmesi için araçtır. Yol, bina, sensör, yükselti ve analiz sınırı aynı projede birleştirilebilir. Katmanları ekleyebilmek için ilgili veri kaynaklarına ayrıca erişmek gerekir. [QGIS GIS giriş belgeleri](https://docs.qgis.org/3.44/en/docs/gentle_gis_introduction/index.html).

TrafficML'de uygun rolü: pilot sınırı hazırlama, sensörün hangi yola baktığını kontrol etme, koordinat dönüşümleri, geometrilerin denetimi ve katmanların karşılaştırılmasıdır. Trafik talebi veya sinyal programı üretmez. Yol merkez çizgisi, şerit geometrisi, kullanılabilir yol alanı, bina ayak izi ve kadastro farklı katmanlardır; biri diğerinin yerine geçmez.

OSM, ilk yol ağını kurmak için başlangıç sağlayabilir. SUMO'nun resmî içe aktarma belgesi, eksik hız ve bağlantı bilgilerinin tahmin edilebildiğini ve düzeltme gerekebildiğini açıklıyor. Otomatik oluşturulan sinyal gerçek plan sayılmaz. [SUMO OSM içe aktarma](https://sumo.dlr.de/docs/Networks/Import/OpenStreetMap.html).

### Copernicus DEM ve bina verisi

Copernicus GLO-30 yaklaşık 30 metre örneklem aralığına sahip küresel bir yüzey modelidir. Resmî tanımında bina, altyapı ve bitki örtüsü dahildir. Çıplak arazi modeli veya tek tek binaların vektör envanteri olarak okunmamalı. [Copernicus DEM açıklaması](https://documentation.dataspace.copernicus.eu/Data/Others/CCM.html#copernicus-dem).

Genel yükselti ve çevre bağlamına katkısı olabilir. Şerit genişliği, bordür, dönüş cebi veya dar yol kesitinin ölçümünü karşılaması beklenmez; daha sık grid'e dönüştürmek yeni ölçüm ayrıntısı kazandırmaz. Binaların yüzey modeline dahil olması, ayrı bina yüksekliği/ayak izi bilgisinin verildiği anlamına gelmez.

Helsinki'nin resmî harita servisi bina/taşınmaz kayıtları, imar, 3D arazi ve tarama verilerini listeliyor. Bu çeşitlilik statik çevre açısından avantajdır. Ancak seçilen katmanın tarihi, lisansı, indirilebilirliği ve şerit/kesit doğruluğu pilot bazında kontrol edilmelidir. [Helsinki harita servisi](https://www.hel.fi/en/decision-making/information-on-helsinki/maps-and-geospatial-data/helsinki-map-service).

## Ankara ve Helsinki seçeneklerinin karşılaştırılması

| İhtiyaç | Ankara | Helsinki / yakın çevresi |
|---|---|---|
| Hız ve seyahat durumu | Kullanıcının mevcut akışı; TomTom/HERE belge kapsamı | Ticari kaynaklar ve bazı kamu sensörleri |
| Toplam araç geçişi | TomTom Volume model tahmini için yeni aday; kurumsal/saha erişimi gerekli | Digitraffic gerçek kaydı alındı; LIDO gözlem indirme bu oturumda başarısız |
| Araç türleri | Seçilen kamu/kurum/saha kaynağı henüz yok; Volume birlikte veriyor | LAM ve SmartJunction tür alanları destekli; pilotta ayrıntı doğrulanmalı |
| Kavşak dönüşleri | Doğrulanmış örnek yok | Şerit/dedektör verisi umut verici; her dönüşü temsil ettiği doğrulanmadı |
| Mevcut sinyal işletimi | Doğrulanmış plan veya olay kaydı yok | LIDO şeması plan/faz sağlamıyor; ayrı kaynak gerekiyor |
| Yaya ve bisiklet | Pilot sayımı veya kurum kaynağı gerekli | EcoCounter belgeli; geçit/yön/zaman örtüşmesi ve erişim açık |
| Statik çevre | OSM/DEM başlangıcı; yerel ayrıntı kontrolü gerekli | Belediye katmanları nedeniyle daha güçlü aday |
| Yerinde doğrulama | Ekip Ankara'daysa pratik avantaj | Uzaktan pilotta geometri/kontrol boşluklarını kapatmak daha zor olabilir |
| Ankara için sonuç iddiası | Yerel doğrulama başarılırsa doğrudan ilgili | Ankara'ya aktarım ayrıca yerel veriyle sınanmalı |

Bu tablo, iki şehirde bütün kaynakların tarandığı veya yokluğun kesin kanıtlandığı iddiası değildir. İncelenen kaynakların ve erişim denemelerinin karar açısından karşılaştırmasıdır.

Ankara'da kurumun veri topluyor olması mümkündür ve resmî raporlar trafik etüt/sayım faaliyetlerinden söz eder; açık, yeniden kullanılabilir pilot verisinin ekibe verileceği bundan çıkarılamaz. Sorun "Ankara'da veri üretilmiyor" diye tanımlanmamalı; "gerekli alan, dönem ve ayrıntıda veriye erişimimiz doğrulanmadı" diye tanımlanmalı. [ABB trafik etütleri ve sayımlarına ilişkin 2021 raporu](https://s.ankara.bel.tr/files/2022/04/20/82a847b1e04a4e9f7d6b48d7e8ff52db.pdf), [Şeffaf Ankara tanıtımı](https://www.ankara.bel.tr/mobil-uygulamalar/seffaf-ankara).

## Kaynakları birleştirmek neden tek başına yetmiyor

Bir şehir için hız, başka bir yol için araç sayısı, farklı bir yıl için yaya sayısı ve genel bir sinyal varsayımı bir araya getirildiğinde gerçek bir eşzamanlı trafik durumu oluşmaz. Gerçek pilotta şu eşleşmeler gerekir:

1. Aynı fiziksel yol, yön, şerit veya hareket. Sağlayıcı segmenti, OSM yolu ve sensör kimliği farklı olabilir.
2. Aynı ya da açıklanabilir biçimde örtüşen dönem. Saatlik ortalama, 15 dakikalık sayım ve saniyelik sinyal olayı farklı amaçlarla korunmalı.
3. Aynı ölçü ve birim. m/s ile km/saat, sayı ile saatlik oran, örneklem ile toplam tahmin ayrılmalı.
4. Kaynağın kapsadığı kullanıcı grubu. Otomobil/hafif araç ayrımı, tramvay ve bisiklet sınıfları ortak sözlüğe bilinçli eşlenmeli.
5. Ölçüm anı ve alınma anı. Güncel metadata veya servis yanıtı eski gözlemi yeni yapmaz.
6. Kalite ve eksik veri. Sensör arızası/boş kayıt, sıfır trafik değildir.

Finlandiya'nın günlük ham LAM dosyasında yerel EET/EEST kullanıldığı belgeleniyor; farklı kaynakların saat dilimleri doğrudan birleştirilmemeli. Türkiye ve Finlandiya gösterim/saklama tercihleri kaynak ofsetleri korunarak yönetilmeli. [LAM zaman ve dosya formatı](https://www.digitraffic.fi/en/road-traffic/lam/#description-of-the-result-file-format).

Sıkışmış ağda çıkışta gözlenen geçiş sayısı da dışarıdan gelmek isteyen toplam talebe eşit olmayabilir. Modelin yalnız tamamlanan araçlara bakarak "iyileşme" üretmesini önlemek için girişte kalanlar, tamamlanmayanlar ve ağ sınırına taşan kuyruklar hesaba katılmalıdır. Bu, paketin metrik yaklaşımını korumayı gerektirir.

## ML araştırmasının yapılabilirliği

Gerçek şehirdeki bütün değişkenlere erişmeden simülasyon deneyleri üzerinden bir model eğitilebilir. Bunun dürüst iddiası, "tanımlı ağ ve talep alanında simülasyon performansını yaklaştırıyoruz" olur. Bu iddia, gerçek Ankara müdahalesinin etkisini doğru bildiğimiz anlamına gelmez.

Üç görev ayrı değerlendirilmelidir:

- **Gelecek trafik tahmini:** Gözlem serisinin ilerideki hız/akışını öğrenir. Yeni yol tasarımının etkisini otomatik çözmez.
- **Tasarım performansı tahmini:** Geometri, kontrol ve talep girdilerinden simülasyon ölçütlerini öğrenir. Paketin FR-20 hedefidir.
- **Müdahale seçimi:** Kısıtları geçen seçenekler arasında tercih yapar. Hızlı tahminin gerçek katkısı, aynı hesaplama bütçesinde daha iyi aday bulup bulmadığıdır.

İlk modelin derin öğrenme veya GNN olması gerekmez. Basit referanslar ve uygun regresyonlarla başlanabilir. Başarı yalnız R² üzerinden değil, gecikme/kuyruk hatası, aday sıralaması, kötü yan etkileri kaçırma ve yanlış aday seçmenin kaybı üzerinden değerlendirilmelidir. Aynı tasarımın tekrarlarını rastgele eğitim/test satırlarına bölmek iyimser sonuç üretir; ayrı tasarım ve talep grupları gerekir.

Simülasyonun ürettiği etiketi aynı simülasyona karşı test etmek ML'nin taklit başarısını ölçer. Saha geçerliliği için bağımsız gözlem gerekir. Bir sağlayıcının tahminini giriş ve doğrulama hedefi olarak kullanmak da sağlayıcının kendi varsayımlarını tekrar doğrulama riski taşır.

Helsinki verisiyle kurulan davranış/talep modeli Ankara'da yeniden kalibre edilmeden yerel başarı iddiası taşıyamaz. FHWA da varsayılan simülasyon parametrelerinin kalibre edilmiş model olmadığını ve yerel koşullarla uyarlama gerektiğini belirtir. [FHWA model kalibrasyonu](https://ops.fhwa.dot.gov/publications/fhwahop18036/chapter5.htm).

## Fiziksel alternatifler ve maliyet için sınır

İlk fiziksel şablon, kullanılabilir kesiti ve hareketleri doğrulanabilen dar bir değişiklik olmalı. Dönüş cebi veya şerit kullanım değişikliği bu tür bir araştırma için aday olabilir; hangi seçeneğin gerçekten uygun olduğu alan görülmeden söylenemez.

Bina ayak izleri, arazi yükseltisi ve yol çizgileri; kamulaştırma, altyapı hatları, mevcut kotlar ve yapım koşulları yerine geçmez. Bu veriler yoksa simülasyon sonucu hesaplanabilir ama "uygulanabilir inşa projesi" sonucu verilmez. Maliyet, bilinen metraj ve fiyatların yaklaşık hesabı olarak kalır; bilinmeyen kalemler sıfırlaştırılmamalıdır.

KGM/YFK kaynaklarının mevcut olması, pilot poz eşlemesi ve gerçek maliyet çıkarıldığı anlamına gelmez. Pakette de bu çalışma yapılmamış. Helsinki senaryosunun maliyeti hesaplanacaksa Türkiye fiyatları yerel Helsinki uygulama bedeli olarak sunulmamalı; para birimi, ülke, tarih ve iş kapsamı belirtilmelidir.

## Pilot kararını kesinleştirecek kanıtlar

Bu bölüm geliştirme talimatı veya uygulanmış takvim değil, sonraki görüşmede kullanılabilecek karar ölçütleridir.

| Karar kapısı | Görülmesi gereken somut kanıt | Sağlanmazsa kapsam sonucu |
|---|---|---|
| Veri erişimi | Seçilen alandan indirilen örnek ölçüm; alan, zaman, birim ve kaynak açıklaması | Belgeye dayalı aday olarak kalır. |
| Ağ ve hareket eşlemesi | Girişler, dönüşler, sensör kapsamı, şerit ve bağlantı denetimi | Kavşak/geometri etkisi yerine daha dar hız/akış çalışması düşünülür. |
| Mevcut kontrol | Faz-hareket eşlemesi ve uygun dönem planı; uyarlanabilir ise gerçek işleyişi temsil eden bilgi | Varsayımsal kontrol çalışması yapılabilir; mevcut şehrin sinyal iyileştirmesi iddiası verilmez. |
| Ayrı doğrulama | Kalibrasyondan ayrılmış dönem ve ölçüt; kuyruk/seyahat/akış davranışı | Gerçek şehir modeli kabul edilmez. |
| Fiziksel müdahale | Kesit, korunan alan ve uygulama sınırları | Yalnız parametreli araştırma senaryosu veya inceleme bekleyen aday sunulur. |
| Ekip ve kaynak | Görev kapasitesi, teslim tarihi, veri maliyeti ve küçük koşu ölçümü | Süre ve bütçe taahhüdü verilmez. |

Hız/akış tahmininde yeterli veri sayılan bir seri, saniyelik sinyal işletimi için yeterli olmayabilir. Aynı şekilde çok uzun bir zaman serisi bütün dönüşlerin gözlenmediği bir kavşağın eksik hareketlerini tamamlamaz. Başarı eşikleri kullanım amacı ve gözlem değişkenliği görüldükten sonra belirlenmeli; keyfî doğruluk veya kazanç yüzdesi konulmamalı.

## Tavsiye edilen karar

**Teknik yöntem araştırması için devam:** SUMO tabanlı küçük ağ, bir işletim ve bir fiziksel alternatif, ortak talep altında deney, metrikler ve ML ön değerlendirmesi savunulabilir çekirdektir. Bu, paketteki özgün gereksinimlerin otomatik değiştirilmesi değildir; bütün FR'lerin teslim kapsamı ekip/danışman değerlendirmesinde ayrıca korunmalı veya revize edilmelidir.

**Gerçek Ankara pilotu için koşullu devam:** Önce mevcut yoğunluk akışının şeması, TomTom Volume'un seçilen yoldaki gerçek erişimi ve eksik sayım/sinyal bilgisini edinme yolu somutlaştırılmalıdır. Dar bir alan ve erişilebilir saha gözlemi, bütün şehrin açık veriye dönüşmesini beklemekten daha gerçekçi olabilir. Belediye verisinin verileceği veya saha ölçümünün yeterli olacağı varsayılmıyor.

**Helsinki için güçlü aday:** Öncelik belge sayısından çok aynı alandaki güncel ve indirilebilir gözlemlerin örtüşmesi olmalı. SmartJunction çevresi incelemeye değer, fakat gözlem indirme başarısı, mevcut kontrol ve gerekli yaya hareketleri çözülmeden kesin seçime gidilmemeli. Digitraffic'in çalışan akışı daha dar hız/akış/sınıf araştırması için ayrıca kullanılabilir.

**Şehirler arası aktarım için ayrı kanıt:** Helsinki'nin veri avantajı Ankara'nın veri açığını kapatmaz. Yöntemi yabancı bir pilotta sınayıp Ankara'yı daha sonra yerel verilerle doğrulamak, proje açısından mümkün bir yön; Ankara sonuçlarının doğruluğu ayrı araştırma sorusudur.

En belirleyici açık konu yazılım aracının bulunması değil, tek bir pilotta **geometri + talep + mevcut kontrol + bağımsız performans gözlemi** zincirinin tamamlanmasıdır. Projenin hangi iddiayla yürütülebileceği bu zincirin elde edilen kısmına bağlanmalıdır.

## Erişim denemelerinin kayıtları

analysis/evidence/ altında Helsinki OpenAPI şeması, kaynak açıklamaları, sensör listesi, metadata özeti, başarısız gözlem sorgularının durumları, Digitraffic güncel ölçümleri ve günlük ham örneği saklandı. Bunlar erişim anının görüntüleridir; canlı servislerin sonraki durumunu garanti etmez.

LIDO gözlem sorgularında zaman aşımı/503; HRI katalog sayfasını web aracıyla doğrudan açmada 403 oluştu. Katalog için arama kaydı, belediyenin teknik belgesi ve doğrudan API metadata'sı birlikte kullanıldı. Bu hatalar verinin genel yokluğuna dönüştürülmedi.

TomTom/HERE için resmî güncel belgeler incelendi; anahtarlı pilot sorgusu çalıştırılmadı. Ankara kamu kaynaklarında yeniden kullanılabilir, eşzamanlı pilot veri paketi bu taramada doğrulanmadı. Kaynak kataloğundaki 36 kaynağın her biri için yeni deneysel yeniden üretim veya yeni erişim doğrulaması yapıldığı iddia edilmiyor.
