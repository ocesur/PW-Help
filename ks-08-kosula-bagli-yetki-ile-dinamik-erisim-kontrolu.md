## []{#Xd63e85f29a50b6ef68b9bdfe456189829d3916c display="false"}Koşula Bağlı Yetki ile Dinamik Erişim Kontrolü {#koşula-bağlı-yetki-ile-dinamik-erişim-kontrolü block-id="mm35z3ub-ayypqj-054"}

## []{#genel-bakış display="false"}Genel Bakış {#genel-bakış block-id="mm35z3uc-0iwsoa-055"}

Koşula Bağlı Yetki özelliği, belge veya dosya kartı kayıtlarının erişim
yetkilerinin; kayıt sırasında tip alanlarına girilen değerlere göre
otomatik olarak belirlenmesini sağlar. Bu sayede yetkilendirme, sabit
rol veya kullanıcı tanımlarına bağlı kalmadan dinamik şekilde uygulanır.

Bu yapı, özellikle farklı senaryolarda farklı kullanıcı gruplarının
erişmesi gereken arşiv ve dosya kartı kayıtlarında güvenli ve esnek bir
erişim kontrolü sağlar.

## []{#ne-zaman-kullanılır display="false"}Ne Zaman Kullanılır? {#ne-zaman-kullanılır block-id="mm35z3uc-ahxfd1-058"}

Aşağıdaki durumlarda Koşula Bağlı Yetki kullanımı önerilir:

- Aynı arşiv tipinde farklı içeriklere farklı kullanıcıların erişmesi
  gerekiyorsa

- Yetkilendirmenin, form alanlarına girilen değerlere göre değişmesi
  isteniyorsa

- Statik rol tanımları yerine dinamik erişim kontrolü hedefleniyorsa

- Belge ve dosya kartı kayıtlarında veri gizliliği kritikse

## []{#nasıl-çalışır display="false"}Nasıl Çalışır? {#nasıl-çalışır block-id="mm35z3uc-zab9lw-065"}

Koşula Bağlı Yetki, **klasör yetkileri etkin olmayan kabinetlerde**
arşiv tipleri ve dosya kartı tipleri üzerinde yapılandırılarak çalışır.

Temel çalışma adımları:

1.  Arşiv tipi veya dosya kartı tipinde "Yetkiler" sekmesi açılır

2.  "Koşula Bağlı Yetki" seçimi aktif edilir

3.  Tip alanlarına bağlı koşullar tanımlanır

4.  Her koşul için ilgili yetki seti belirlenir

5.  Kayıt sırasında girilen değerlere göre yetkilendirme otomatik
    uygulanır

Yetkilendirme işlemi, belge veya kayıt oluşturulurken gerçekleştirilir.

## []{#kullanım-senaryoları display="false"}Kullanım Senaryoları {#kullanım-senaryoları block-id="mm35z3ud-0zrw65-075"}

### []{#birim-bazlı-belge-erişimi display="false"}1. Birim Bazlı Belge Erişimi {#birim-bazlı-belge-erişimi block-id="mm35z3ud-0w88fc-076"}

- Belge arşivlenirken "Birim" alanı doldurulur

- Tanımlı koşula göre ilgili birime ait yetki seti uygulanır

- Belgeler yalnızca yetkili kullanıcılar tarafından görüntülenir

### []{#gizlilik-seviyesine-göre-yetkilendirme display="false"}2. Gizlilik Seviyesine Göre Yetkilendirme {#gizlilik-seviyesine-göre-yetkilendirme block-id="mm35z3ud-ovy63n-081"}

- Form üzerinde gizlilik seviyesi seçilir

- Seçilen değere bağlı olarak farklı yetki setleri devreye alınır

- Hassas belgeler sınırlı erişimle saklanır

### []{#proje-bazlı-dosya-kartı-erişimi display="false"}3. Proje Bazlı Dosya Kartı Erişimi {#proje-bazlı-dosya-kartı-erişimi block-id="mm35z3ud-habk0r-086"}

- Dosya kartı oluşturulurken proje bilgisi girilir

- Projeye özel yetki seti otomatik atanır

- Yetkisiz erişimler kayıt aşamasında engellenir

## []{#senaryo-akış-özeti display="false"}Senaryo Akış Özeti {#senaryo-akış-özeti block-id="mm35z3ud-ams2ud-091"}

- **Belge arşivleme:** Alan değerleri girilir → Koşullar değerlendirilir
  → Yetki seti atanır

- **Dosya kartı kaydı:** Tip alanları doldurulur → Dinamik yetkilendirme
  uygulanır → Kayıt oluşturulur

- **Erişim kontrolü:** Kullanıcı yalnızca yetkili olduğu kayıtları
  görüntüler

## []{#iş-değeri display="false"}İş Değeri {#iş-değeri block-id="mm35z3ud-lvkw9j-096"}

- Dinamik ve esnek yetkilendirme yapısı sağlanır

- Veri gizliliği ve erişim güvenliği artar

- Manuel yetki yönetimi ihtiyacı azalır

- Hatalı veya yetkisiz erişimler engellenir

- Farklı senaryolar tek arşiv tipi altında yönetilebilir

## []{#teknik-notlar display="false"}Teknik Notlar {#teknik-notlar block-id="mm35z3ue-6kyl3l-103"}

- Koşula Bağlı Yetki yalnızca **klasör yetkileri etkin olmayan
  kabinetlerde** kullanılabilir.

- Klasör yetkileri etkin olan kabinetlerde tüm yetkiler kabinet
  seviyesinden yönetilir.
