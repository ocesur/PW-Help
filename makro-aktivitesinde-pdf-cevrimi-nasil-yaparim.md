## PDF Çevirme {#pdf-çevirme block-id="mgje2zml-wphr3i-001"}

PaperWork BPM üzerinde **V6.1 sürümü** ile birlikte iş akış
aktivitelerine "**PDF Çevirme**" adıyla yeni bir nesne eklenmiştir.

Bu nesne sayesinde, artık makro üzerinde PDF çevirme işlemi için ek
kodlama yapılmasına gerek kalmadan, belge formatı dönüştürme işlemi
doğrudan akış içerisinde gerçekleştirilebilir.

PDF Çevirme aktivitesi, akışın eklentisinde yer alan Word (.docx)
uzantılı belgeleri PDF formatına dönüştürür. İşlem yalnızca akışın
eklentisinde bulunan belgeler üzerinde uygulanır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/PDF%20%C3%87evirme%20%C4%B0konu.png){.adv-wysiwyg-img
block-id="mgjh8dg6-wo6z26-045" mediatype="img" width="auto"
height="auto" dataalign="center" datadisplay="inline"
data-type="media-content" fixaspectratio="false" autoaspectratio="false"
shadow="no" border="no" round="no" link="" newtab=""
style="width:auto;height:auto;" _ngcontent-ng-c1691667138=""
cy="imageNodeView" data-align="center" display="inline"}**PDF Çevirme**
nesnesi hakkında detaylı bilgi almak için PDF Çevirme Nesnesi
Özellikleri
[sayfasını](https://paperworkbpm.document360.io/docs/a5x070402900){target="_self"
translate="no"} inceleyebilirsiniz.

## Nasıl Yaparım {#nasıl-yaparım block-id="mgjfctl0-lywxus-007"}

Aşağıda, PDF Çevirme nesnesinin bir iş akışında nasıl
kullanılabileceğini gösteren örnek bir senaryo paylaşılmıştır.

### Amaç {#amaç block-id="mgjfdwho-bs8u9y-008"}

Akışın eklentisinde yer alan Word belgesinin, süreç içerisinde otomatik
olarak PDF formatına dönüştürülmesi.

### Örnek Akış Yapısı {#örnek-akış-yapısı block-id="mgjfttev-0f12mb-009"}

1.  **Başlangıç Aktivitesi**

    1.  Akış başlatılır. Kullanıcı, eklentiye Word (.docx) formatında
        bir belge ekler.

    2.  Akışın eklentisi türü **Dosya Kartı** olarak seçilmiştir.

2.  **PDF Çevirme Aktivitesi**

    1.  Bu adımda akıştaki Word belgesi PDF formatına dönüştürülür.

    2.  Aktivite özelliklerinde aşağıdaki seçimler yapılmıştır:

        1.  **Taslak:** *Rapor* → Akış eklentisinde "Rapor" ifadesini
            içeren belge seçilecektir.

        2.  **Tüm Belgeleri PDF'e Çevir:** *İşaretli değil* → Yalnızca
            "Taslak" alanına uygun belge çevrilecektir.

        3.  **PDF Belgeyi Yeni Versiyon Olarak Kaydet:** *İşaretli* →
            Word belgesinin yeni majör versiyonu PDF olarak
            kaydedilecektir.

    3.  Çevrim tamamlandığında akış otomatik olarak sonraki adıma
        ilerler.

3.  **Onay Aktivitesi**

    1.  Akış eklentisinde artık PDF formatında belge bulunur.

    2.  İlgili kullanıcı, belgeyi görüntüleyip onay verir.

4.  **Bitiş Aktivitesi**

    1.  Akış başarıyla tamamlanır.

## PDF Çevrimi Esnasında Bekleme Süresi {#pdf-çevrimi-esnasında-bekleme-süresi block-id="mgjfybtp-aubt2w-024"}

PDF Çevirme aktivitesine ulaşan akış, çevrim işlemi sırasında kısa bir
süre bekler.

Belgeler sırayla PDF'e dönüştürülür. Dönüştürme tamamlandığında akış
otomatik olarak bir sonraki adıma ilerler.

### Dikkat Edilmesi Gerekenler {#dikkat-edilmesi-gerekenler block-id="mgjg2vhw-ok2lwh-033"}

- PDF Çevirme işlemi **yalnızca Word (.docx)** belgeleri için
  yapılmalıdır.

- PDF dosyaları tekrar PDF'e çevrilmemelidir.

- Akışın eklentisi **Arşiv tipi** ise "Tüm Belgeleri PDF'e Çevir" seçimi
  etkisizdir, çünkü Arşiv eklentilerinde tek belge bulunur.

- Akış eklentisi **Dosya Kartı** ise:

  - Çevrilen belge, kaynak belgeyle aynı klasöre kaydedilir.

  - "PDF Belgeyi Yeni Versiyon Olarak Kaydet" seçiliyse, eski belgenin
    yeni majör versiyonu oluşturulur.

- "PDF Belgeyi Yeni Versiyon Olarak Kaydet" seçeneği işaretlendiğinde,
  akışın eklentisi artık yeni oluşan PDF belgesidir.
