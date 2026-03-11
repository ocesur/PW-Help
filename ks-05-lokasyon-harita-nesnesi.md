## []{#X843b1ed6cddccdc3cacd7a02b3ded4a641ea28b display="false"}Lokasyon (Harita) Nesnesi ile Saha ve Konum Bazlı Süreçler {#lokasyon-harita-nesnesi-ile-saha-ve-konum-bazlı-süreçler block-id="mm32yncg-tugfxg-057"}

## []{#genel-bakış display="false"}Genel Bakış {#genel-bakış block-id="mm32yncg-38uy63-058"}

Lokasyon (Harita) nesnesi, formlar üzerinde coğrafi konum bilgisinin
harita üzerinden seçilmesini sağlar. Kullanıcılar, Google Haritalar
üzerinden arama yaparak veya harita üzerindeki imleci hareket ettirerek
ilgili konumu belirleyebilir.

Bu nesne, özellikle saha, denetim, bakım, keşif ve lokasyon bazlı
bildirim gerektiren süreçlerde adres ve konum bilgilerinin doğru ve
standart şekilde toplanması amacıyla kullanılır.

## []{#ne-zaman-kullanılır display="false"}Ne Zaman Kullanılır? {#ne-zaman-kullanılır block-id="mm32ynch-y9uec5-061"}

Aşağıdaki durumlarda Lokasyon (Harita) nesnesinin kullanımı önerilir:

- Saha operasyonları ve dış lokasyonlu çalışmalar yürütülüyorsa

- Adres bilgisinin harita üzerinden doğrulanması gerekiyorsa

- Konum bilgisinin manuel yazım yerine seçilerek alınması isteniyorsa

- Denetim, bakım, keşif veya arıza bildirim süreçleri lokasyon bazlı
  yürütülüyorsa

- Harita destekli raporlama ve izleme hedefleniyorsa

## []{#nasıl-çalışır display="false"}Nasıl Çalışır? {#nasıl-çalışır block-id="mm32ynch-o2yjg5-069"}

Lokasyon (Harita) nesnesi, Google Haritalar altyapısını kullanarak
çalışır ve form tasarımı sırasında yapılandırılır.

Temel çalışma adımları:

1.  Lokasyon nesnesi, "Yazı" veri tipindeki bir tip alanına bağlanır

2.  Google Haritalar için gerekli API Anahtarı ve Map ID bilgileri temin
    edilir

3.  API Anahtarı ve Google Map ID, nesne özellikleri alanına girilir

4.  Kullanıcı form üzerinde harita aracılığıyla konum seçimini yapar

5.  Seçilen konum bilgisi form kaydı ile birlikte saklanır

Bu yapı sayesinde konum bilgileri standart, doğrulanabilir ve görsel
olarak seçilmiş şekilde toplanır.

## []{#kullanım-senaryoları display="false"}Kullanım Senaryoları {#kullanım-senaryoları block-id="mm32ynch-9v9c2n-079"}

### []{#saha-arıza-ve-bakım-bildirimleri display="false"}1. Saha Arıza ve Bakım Bildirimleri {#saha-arıza-ve-bakım-bildirimleri block-id="mm32ynci-d8vrw2-080"}

- Kullanıcı arıza veya bakım yapılacak noktayı harita üzerinden seçer

- Konum bilgisi form kaydına eklenir

- İlgili saha süreci doğru lokasyon bilgisi ile başlatılır

### []{#denetim-ve-keşif-süreçleri display="false"}2. Denetim ve Keşif Süreçleri {#denetim-ve-keşif-süreçleri block-id="mm32ynci-nwoch3-085"}

- Denetim veya keşif yapılan alan harita üzerinden işaretlenir

- Konum bilgisi kayıt altına alınır

- Denetim raporları lokasyon bilgisi ile birlikte ilerler

### []{#isg-ve-uygunsuzluk-bildirimleri display="false"}3. İSG ve Uygunsuzluk Bildirimleri {#isg-ve-uygunsuzluk-bildirimleri block-id="mm32ynci-2sa8ev-090"}

- Riskli alan veya uygunsuzluk tespit edilen nokta harita üzerinden
  seçilir

- Bildirim süreci konum bilgisi ile tetiklenir

- Sahaya yönelik aksiyonlar doğru lokasyonla planlanır

## []{#senaryo-akış-özeti display="false"}Senaryo Akış Özeti {#senaryo-akış-özeti block-id="mm32ynci-nfs824-095"}

- **Saha bildirimi:** Lokasyon seçilir → Form kaydedilir → Süreç
  başlatılır

- **Denetim süreci:** Konum harita üzerinden belirlenir → Kayıt
  oluşturulur → İnceleme yapılır

- **İSG bildirimi:** Riskli nokta işaretlenir → Bildirim gönderilir →
  Aksiyon alınır

## []{#iş-değeri display="false"}İş Değeri {#iş-değeri block-id="mm32ynci-vhtpes-100"}

- Konum bilgilerinde yazım ve yorum hataları azalır

- Saha süreçlerinde doğru lokasyona hızlı erişim sağlanır

- Bildirim ve raporlar coğrafi konum ile ilişkilendirilir

- Operasyonel süreçlerde izlenebilirlik artar

- Saha ekipleri ve merkez arasında doğru bilgi akışı sağlanır

## []{#teknik-notlar display="false"}Teknik Notlar {#teknik-notlar block-id="mm32ynci-ks2qnn-107"}

- Lokasyon nesnesi "Yazı" veri tipindeki alanlara bağlanabilir.

- Google Haritalar API Anahtarı ve Map ID alınması gerekmektedir.

- Web.config dosyasında Content Security Policy ayarlarında gerekli
  domainler tanımlı olmalıdır.

- Google Cloud Map API ücretli bir hizmettir ve kullanım bazlı
  faturalandırılır.
