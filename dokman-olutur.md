---
title: "Doküman Oluştur"
---

#### Yeni Doküman Oluştur

- Kullanıcı, ilgili klasörde yazma yetkisine sahip olduğunda Doküman Oluştur butonu aktif olur.
- Bu butona tıklayarak, seçili klasör içerisine yeni doküman eklemek için talepte bulunabilir.
- Sistem, dokümanın eklenmesini ve yetkili kullanıcılar tarafından erişilebilir olmasını sağlar.

![metin, ekran görüntüsü, yazı tipi, sayı, numara içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1772705202105.png)

#### **Doküman Oluşturma Ekranı**

- Kullanıcı, **"Doküman Oluştur"** butonuna tıkladığında aşağıdaki ekran aktif hale gelir.
- Bu ekranda, seçili klasör içerisine eklenecek yeni doküman ile ilgili gerekli bilgilerin girilmesi sağlanır.
- Ekrandaki alanlar, dokümanın türüne ve kuruluşun tanımlı parametrelerine göre görüntülenir.

![metin, ekran görüntüsü, sayı, numara, yazılım içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-cis98h7b.png)

#### **Doküman Oluşturma Alanları**

Yeni bir doküman eklerken doldurulacak alanlar şunlardır:

- **Firma:** Sistem tarafından otomatik olarak atanır. Doküman talebinin oluşturulduğu klasörde tanımlı firma bilgisi kullanılır.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → Firma
    Tanımlama**
- **Lokasyon:** Kullanıcı tarafından seçilir. Firmaya bağlı tanımlı lokasyonlar listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → Lokasyon
    Tanımlama**
- **Departman:** Kullanıcı tarafından seçilir. Lokasyona bağlı tanımlı departmanlar listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → DYS Departman
    Tanımlama**
- **Süreç:** Kullanıcı tarafından seçilir. Firma ve departmana bağlı tanımlı süreçler listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → Süreçler**
- **Doküman Türü:** Kullanıcı tarafından seçilir. Firma ve departmana bağlı doküman türleri listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → Sistem
    Dokümanları**
- **Standart:** Kullanıcı tarafından seçilir. Firma ve departmana bağlı tanımlı standartlar listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → Standartlar**
- **KVKK**: Kullanıcı tarafından seçilir. Tanımlı KVKK seçenekleri listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları → KVKK**
- **Sınıflandırma**: Kullanıcı tarafından seçilir. Tanımlı sınıflandırma seçenekleri listelenir.
  - Detaylar için: **Parametreler → Liste Tanımlamaları →
    Sınıflandırmalar**
- **Doküman Adı:** Yüklenen dokümanın adı, sistem tarafından otomatik olarak atanır.
- **Doküman Numarası**: Bu alan, dokümanın numarasını gösterir ve Parametreler alanında yapılan doküman numaralandırma tanımına bağlı olarak veri oluşur.
  - **Sistemin numara ataması "Hayır" ise:**
    - Kullanıcı, doküman numarasını **manuel olarak** girmelidir.
    - Sistem, kullanıcıya daha önce kullanılan numaraları gösteren bir **bilgilendirme ekranı** açar.
    - **Onay Süreci Olmadan Başlatılsın** seçeneği:
      - **Evet:** Numara, doküman oluşturma aşamasında girilir.
      - **Hayır:** Numara, **Dokümanın Yayınlanması** adımında tanımlanır.
  - **Sistemin numara ataması "Evet" ise:**
    - Doküman numarası alanları form üzerinde **zorunlu** hale gelir.
    - Sistem, seçimlere göre otomatik olarak bir **doküman numara** yapısı oluşturur.
    - Bu yapıda, parametre tanımlarında yer alan **Firma, Lokasyon,
      Departman, Doküman Türü vb**. kısaltmalar kullanılır.

> Bu özellik, dokümanların **benzersiz ve düzenli numaralandırılmasını** sağlar ve kullanıcıların hatalı numara girmesini önler.

![metin, ekran görüntüsü, yazı tipi, çizgi içeren bir resim Yapay zeka
tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-3x993ku6.png)

- **Talep Açıklaması:** Bu alan, doküman talebine neden ihtiyaç duyulduğunu belirtmek için kullanılır. Kullanıcı burada gerekli açıklamayı girer.
- **Onay Süreci Olmadan Başlatılsın?:** Bu alan, yalnızca **QMS_Tools
  ACL** yetkisine sahip kullanıcıların ekranında görünür.
  - **Evet:** Tüm onay süreçleri pas geçilir ve doküman doğrudan sisteme dahil edilir.
  - **Hayır:** Doküman, ilgili klasör için tanımlı olan **onay, görüş
    verme, ön değerlendirme ve yayınlama** kurallarına göre sisteme dahil edilir.
- **Şablon Kullanılsın mı?:**
  - Bu alan "Evet" olarak seçildiğinde, **Parametreler → Şablon
    Tanımlama** ekranında ilgili firma için tanımlanmış doküman şablonu kullanıcı bilgisayarına indirilir.
  - Kullanıcı, dokümanı doldurduktan sonra tekrar talep içerisine ekleyerek doküman talebini oluşturabilir.
  - Şablon kullanımı, dokümanların firmanın belirlediği standarda uygun olarak hazırlanmasını sağlar.

![metin, yazı tipi, çizgi, sayı, numara içeren bir resim Yapay zeka
tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-jzmychpm.png)

- **Doküman Yükleme:** Bu alan, sisteme alınmak istenen dokümanın yüklendiği bölümdür.
  - Doküman, **sürükle-bırak** yöntemi veya **dosya seçimi** yapılarak yüklenebilir.
  - Yükleme işlemi tamamlandığında doküman, seçili klasöre eklenir ve sistemde izlenebilir hale gelir.
- **İlgili Dokümanlar:** Bu alan, sistemdeki kalite dokümanlarının birbiriyle ilişkili olduğu durumları gösterir.
  - Yüklenen doküman, gerekirse diğer dokümanlarla ilişkilendirilebilir.

![metin, ekran görüntüsü, yazılım, web sayfası içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-q2ap06jt.png)

- **İlgili Standartlar:** Bu alan, sisteme yüklenen doküman ile **tanımlanmış standartlar** arasındaki ilişkinin kurulmasını sağlar.
  - Kullanıcı, dokümanın hangi standartlara uygun olduğunu bu alandan belirleyebilir.
  - Böylece dokümanların **uyumluluk ve kalite takibi** daha kolay ve düzenli bir şekilde yapılabilir.

![metin, yazılım, web sayfası, web sitesi içeren bir resim Yapay zeka
tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-jv3v92vz.png)

- **İlgili Ürünler:** Bu alan, sisteme yüklenen doküman ile **tanımlanmış ürünler** arasındaki ilişkiyi kurmanızı sağlar.
  - Kullanıcı, dokümanın hangi ürün(ler) ile ilgili olduğunu bu alandan belirleyebilir.
  - Bu sayede dokümanların **ürün bazlı takibi ve yönetimi** daha düzenli ve kolay bir şekilde yapılabilir.

![metin, yazılım, bilgisayar simgesi, web sayfası içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-82uw678q.png)

- **Onaycılar:** Bu alan, oluşturulan doküman talebine **onay verecek
  kullanıcılar veya grupları** gösterir.
  - Yeni doküman taleplerinde, onaycı bilgisi **dokümanın eklendiği
    klasör tanımlarından** otomatik olarak gelir.
  - Talep sahibi, mevcut tanımı **silemez**, ancak ilgili doküman için **yeni onaycı ekleyebilir**.
  - Bu sayede, dokümanların onay süreçleri **kontrollü ve esnek** bir şekilde yönetilir.

![metin, ekran görüntüsü, sayı, numara, yazılım içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-z8j72gt8.png)

- **Görüş Alınacak Kişiler:** Bu alan, oluşturulan doküman talebi için **görüş alınacak kullanıcılar veya grupları** gösterir.
  - Yeni doküman taleplerinde, bu bilgi **dokümanın eklendiği klasör
    tanımlarından** otomatik olarak gelir.
  - Talep sahibi, mevcut tanımı **silemez**, ancak ilgili doküman özelinde **yeni görüş alınacak kişi veya grup ekleyebilir**.
  - Bu sayede dokümanların görüş alma süreçleri **kontrollü ve esnek** bir şekilde yönetilir.

![metin, ekran görüntüsü, yazılım, web sayfası içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-o7bp9fj6.png)

- **Doküman Bilgilendirme:** Bu alan, oluşturulan doküman talebi **yayınlandıktan sonra bilgilendirilecek kullanıcılar veya grupları** gösterir.
  - Yeni doküman taleplerinde, bilgilendirme bilgisi **dokümanın
    eklendiği klasör tanımlarından** otomatik olarak gelir.
  - Talep sahibi, mevcut tanımı **silemez**, ancak ilgili doküman özelinde **yeni kullanıcı veya grup ekleyebilir**.
  - Bu sayede doküman yayınlandığında ilgili kişiler **otomatik olarak
    bilgilendirilir**, süreçler takip edilebilir ve iletişim kesintisiz sağlanır.

![metin, ekran görüntüsü, yazılım, web sayfası içeren bir resim Yapay
zeka tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-fjng7d2t.png)

- **Doküman Okunma Aksiyonu:** Bu alan, oluşturulan doküman talebi **yayınlandıktan sonra dokümanı okuyacak kullanıcılar veya grupları** gösterir.
  - Yeni doküman taleplerinde, okuma aksiyonu bilgisi **dokümanın
    eklendiği klasör tanımlarından** otomatik olarak gelir.
  - Talep sahibi, mevcut tanımı **silemez**, ancak ilgili doküman özelinde **yeni kullanıcı veya grup ekleyebilir**.
  - Bu sayede dokümanların okunma takibi yapılabilir ve kullanıcılar gerekli içeriklerden haberdar olur.

![metin, yazılım, yazı tipi, sayı, numara içeren bir resim Yapay zeka
tarafından oluşturulmuş içerik yanlış
olabilir.](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/dokman-olutur-image-vwftp1sm.png)

#### **Doküman Talebini Tamamlama**

- Tüm doküman talebi bilgileri girildikten sonra kullanıcı iki seçenekten birini kullanabilir:
  - **Onayla:** Talep için süreç akışı başlatılır ve doküman onay sürecine girer.
  - **Kaydet:** Talep, daha sonra tamamlanmak üzere **taslak** olarak kaydedilir.
- Oluşturulan tüm doküman taleplerine ilişkin detaylı bilgilere **İşlemler** sayfasından erişilebilir.
- > Doküman onay süreçleri tamamlandıktan sonra, **Word ve Excel
  > dokümanlarında** doküman şablon yapısına uygun olarak **Header ve
  > Footer bilgileri** sistem tarafından otomatik doldurulur.
  - > Bu işlemin doğru şekilde gerçekleştirilebilmesi için, kurulum ve uyarlama aşamasında kullanılan tüm doküman şablonlarının **PWQMS
    > Yazılım Ekibi** tarafından sisteme tanıtılmış olması gerekir.
  - Detaylar için: **Kurulum ve Uyarlama İşlemleri**