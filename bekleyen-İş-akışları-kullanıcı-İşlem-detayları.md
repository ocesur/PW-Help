Denetim Yönetimi İş Akışı kapsamında kullanıcılar tarafından yerine
getirilen işlem adımları ve bu adımlara ilişkin detaylı açıklamalar
aşağıda yer almaktadır.

- #### [**Denetim Planının Onaylanması İşlem Adımı**]{type="spanMark" style="color:rgb(41, 98, 246);"} {#denetim-planının-onaylanması-işlem-adımı block-id="mmiyl4cv-o0t34t-228"}

  - Sistem parametrelerinde **"Denetim planının onaylanması"** **Evet**
    olarak seçilmişse, denetim planını yapan kullanıcının **yöneticisi**
    tarafından planın onaylandığı işlem adımıdır.

  - Denetime ilişkin tüm bilgiler görüntülendikten sonra ilgili
    kullanıcı **Onay**, **Ret** veya **Revize** kararı verebilir:

  - **Revize Kararı:** Denetim planı, revize edilmesi için ilgili
    kullanıcıya yönlendirilir.

  - **Ret Kararı:** Denetim planı reddedilir ve ilgili kullanıcıya
    e-posta ile bilgilendirme yapılır, süreç sonlandırılır.

  - **Onay Kararı:** Denetim planı yayınlanır ve denetimin
    gerçekleştirilmesi adımlarına yönlendirilir.

  - Yayınlanan plan ile birlikte plan kapsamında yer alan tüm kişilere
    (**Baş Denetçi, Katılımcılar, Denetçi, Denetim Sorumlusu, Denetim
    Planlayan Kişi**) denetim takvimleri posta eklentisi olarak e-posta
    ile iletilir.

  - Sistem parametrelerinde **"Denetim planının onaylanması"** **Hayır**
    olarak seçilmişse, süreç bu adıma uğramadan denetim planı doğrudan
    yayınlanır ve denetim gerçekleştirilir.

    ![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-5LMQPNBW.png){.adv-wysiwyg-img
    block-id="mmj9j83y-6nyze0-050" mediatype="img" width="628"
    height="auto" dataalign="left" datadisplay="flex"
    data-type="media-content" fixaspectratio="false"
    autoaspectratio="true" shadow="yes" border="yes" round="no" link=""
    newtab="" style="width:628px;"}

<!-- -->

- #### [**Denetim Planının Onaylanması_Alt Akış İşlem Adımı:** ]{type="spanMark" style="color:rgb(41, 98, 246);"} {#denetim-planının-onaylanması_alt-akış-işlem-adımı block-id="mmiz3v8l-7khrsi-281"}

  - Baş denetçi, mevcut denetim takvimini onaylayabilir veya **yeni
    takvim önerisinde** bulunabilir.

    - **Yeni Takvim Öner** alanından **Evet** seçilirse, **Önerilen
      Başlangıç Tarihi** ve **Önerilen Bitiş Tarihi** alanları görünür
      olur.

      - Bu durumda plan sahibine, takvim değişikliğini onaylaması için
        süreç yönlendirmesi yapılır.

    - Takvim değişikliği talep edilmeyecekse, **"İşlem Seç"** alanından
      **Onayla** seçilerek denetim planı onaylanır.

      ![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-C94G4HSF.png){.adv-wysiwyg-img
      block-id="mmiz3v8m-ve48rq-295" mediatype="img" width="545"
      height="auto" dataalign="left" datadisplay="flex"
      data-type="media-content" fixaspectratio="false"
      autoaspectratio="true" shadow="yes" border="yes" round="no"
      link="" newtab="" style="width:545px;"}

<!-- -->

- #### **Revize Talebi Değerlendirme_Alt Akış İşlem Adımı:** {#revize-talebi-değerlendirme_alt-akış-işlem-adımı block-id="mmizbekg-09m5ye-307"}

  **Revize Talebi Değerlendirme** adımı, baş denetçi tarafından **yeni
  takvim önerildiğinde** plan sahibi tarafından yapılan önerinin
  değerlendirildiği aşamadır.

  Plan sahibi, bu aşamada aşağıdaki seçenekleri kullanabilir:

  - **Onayla:** Değişiklik onaylanır. Sistem, mevcut planı revize eder
    ve yeni takvim ilgili kişilerle paylaşılır.

  - **Revize:** Değişiklik için revize isteyebilir. Bu durumda baş
    denetçi, takvimi tekrar değerlendirir.

  - **Ret:** Değişiklik reddedilir. Denetim, yapılan ilk plan üzerinden
    gerçekleştirilir.

  - **İptal:** Planlanan tüm denetimler iptal edilir. Ana denetim
    planındaki tüm denetimler iptal edilir ve katılımcılara **denetim
    takvimi iptal bilgilendirme e-postası** gönderilir.

<!-- -->

- #### [**Denetimin Gerçekleştirilmesi_Alt Akış İşlem Adımı:** ]{type="spanMark" style="color:rgb(41, 98, 246);"} {#denetimin-gerçekleştirilmesi_alt-akış-işlem-adımı block-id="mmizy3fl-fzn1gb-365"}

  **Denetimin Gerçekleştirilmesi** adımı, baş denetçi tarafından
  denetimin fiilen yürütüldüğü aşamadır.

  - **Düzenle Butonu:** Bu butona basılarak denetim soru listesi
    görüntülenir ve soruların cevaplanması sağlanır.

    > Not: Bu adımda baş denetçi, denetim sürecinde tüm ilgili soruları
    > yanıtlayarak denetim verilerini sisteme kaydeder.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-6MG1DHI2.png){.adv-wysiwyg-img
block-id="mmj0gkk8-dv1ni2-376" mediatype="img" width="771" height="auto"
dataalign="center" datadisplay="inline" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:771px;"}

**Denetim Soru Listesi -- Baş Denetçi Görünümü**

Denetim planlaması aşamasında **Soru Listesi** seçimi yapılmışsa, baş
denetçi ekranında ilgili soru listesi içeriğini görüntüler.

- Baş denetçi, denetim sırasında:

  - İlgili soruları yanıtlayabilir,

  - Bölümler veya sorular arasında geçiş yaparak denetimini
    sürdürebilir.

> **Not:** Bu yapı, denetimin esnek ve sistematik bir şekilde
> yürütülmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-4H5PVIAB.png){.adv-wysiwyg-img
block-id="mmj9j840-uxti18-052" mediatype="img" width="667" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:667px;"}

**Denetçi -- Soru Cevap Durumu**

Denetçi, bölüm içerisinde **cevapladığı soru sayısını** ilgili ekrandan
görüntüleyebilir.

> **Not:** Bu özellik, denetçinin ilerlemesini takip etmesini ve eksik
> kalan soruları kolayca görmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-FXB72IZC.png){.adv-wysiwyg-img
block-id="mmj9j840-mp81h7-053" mediatype="img" width="434" height="173"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:434px;height:173px;"}

**Özel Soru ve Cevap Ekleme -- Baş Denetçi Görünümü**

Denetim planlaması aşamasında **Soru Listesi seçimi yapılmamışsa**, baş
denetçi ekranında **Özel Soru ve Cevap Ekleme** ekranı görüntülenir
(aşağıdaki görselde gösterildiği gibi).

- Baş denetçi, denetim sırasında:

  - Sorduğu soruları girer,

  - Sorulara verilen cevapları kaydeder,

  - Gerekli yorumları ekleyerek denetimini tamamlar.

> **Not**: Bu yapı, denetim sırasında esnek soru ekleme ve değerlendirme
> imkânı sağlar.

**Eklenen Sorular** başlığı altında, baş denetçi tarafından eklenen tüm
sorular:

- Görüntülenebilir,

- Gerekirse değiştirilebilir veya güncellenebilir.

> **Not:** Bu alan, baş denetçinin denetim sırasında eklediği sorular
> üzerinde tam kontrol sahibi olmasını sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-ASGXBFYN.png){.adv-wysiwyg-img
block-id="mmj9j841-n6yn7r-060" mediatype="img" width="616" height="135"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:616px;height:135px;"}

**Denetimin Tamamlanması**

Denetim tamamlandığında, **"İşlem Seç"** alanından **Tamamla** seçeneği
işaretlenerek denetim süreci sonlandırılır.

Bu adımın ardından süreç, **denetim bulgularının değerlendirilmesi** ve
**denetim raporunun yayınlanması** için **Denetim Sorumlusu**na
yönlendirilir.

> **Not:** Denetimi tamamlamak, sistemin raporlama ve bulguların
> işlenmesi adımlarını başlatmasını sağlar.

#### [**Denetim Sonuç Raporunun Oluşturulması İşlem Adımı:** ]{type="spanMark" style="color:rgb(41, 98, 246);"} {#denetim-sonuç-raporunun-oluşturulması-işlem-adımı block-id="mmj0zost-n6wew4-419"}

Denetim tamamlandıktan sonra, **Baş Denetçi/ler** tarafından yürütülen
denetim sürecinin ardından, **Denetim Sorumlusu** tarafından:

- Denetim sonuçlarının değerlendirilmesi,

- Bulguların sınıflandırılması,

- İhtiyaç ve uygulamaya bağlı olarak **CAPA**, **Aksiyon** ve **NCR**
  kayıtlarının girilmesi

işlemleri gerçekleştirilir.

> **Not:** Bu adım, denetim sürecinin raporlanması ve bulguların
> sistematik olarak takip edilmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-CW36HBA1.png){.adv-wysiwyg-img
block-id="mmj16orz-3ux21r-446" mediatype="img" width="574" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:574px;"}

- **Denetim Sonuç Değerlendirme Alt Alanı:** Bu aşamada, denetime
  ilişkin **genel bilgi girişleri** yapılır (aşağıdaki görselde alanlar
  gösterilmektedir):

- **Denetim Sonuç Sınıfı:** Denetime ilişkin sonuçların
  sınıflandırılmasının girildiği alandır.

- **Denetim Genel Sonuç Sınıflandırması:** Denetimin genel sonuç
  sınıflandırmasının girildiği alandır.

- **Denetim Genel Sonuç Öneriler:** Denetim sırasında yapılan öneri ve
  tavsiyelerin girildiği alandır.

- **Denetim Genel Sonuç Olumlu Noktalar:** Denetimde tespit edilen
  olumlu yönlere ilişkin geri bildirimlerin girildiği alandır.

- **Denetim Genel Sonuç Negatif Noktalar:** Denetimde tespit edilen
  olumsuz yönlere ilişkin geri bildirimlerin girildiği alandır.

- **Denetim Bulgu Sayısı:** Denetimde bulunan bulgu sayısının girildiği
  alandır.

> **Not:** Bu alanlar, denetim sonrası raporlamanın ve bulguların
> sistematik olarak takip edilmesinin temelini oluşturur.

**Denetim Detayları Alt Alanı:** Bu alanda, planlanan tüm denetimlere
ait **baş denetçi/ler tarafından girilen bilgiler** görüntülenir.

- **Cevapları Gör:** Bu seçeneğe tıklanarak, denetime ait detaylı
  bilgilere ulaşılabilir ve denetim süreciyle ilgili tüm yanıtlar
  incelenebilir.

> **Not:** Bu alan, denetim sonuçlarının ve denetim sürecinde girilen
> tüm verilerin merkezi olarak görüntülenmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-FUUL9D6E.png){.adv-wysiwyg-img
block-id="mmj9j843-9c2e5f-061" mediatype="img" width="755" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:755px;"}

**"Cevapları Gör" Seçimi**

**"Cevapları Gör"** seçeneği tıklandığında, aşağıdaki ekran açılır ve
denetime ait tüm detaylı bilgiler görüntülenir:

- Bu ekran, baş denetçi/yardımcı denetçiler tarafından girilen **soru
  cevapları**, **yorumlar** ve **ek bilgiler** dahil olmak üzere tüm
  denetim verilerini içerir.

- Kullanıcılar, bu ekran üzerinden denetim detaylarını inceleyebilir ve
  raporlamada referans olarak kullanabilir.

> **Not:** Bu özellik, denetim sonuçlarının merkezi ve sistematik olarak
> takip edilmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-7F9AHEYI.png){.adv-wysiwyg-img
block-id="mmj9j843-luocm1-064" mediatype="img" width="696" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:696px;"}

**Bulgu Sınıflandırması ve Aksiyon Girişi**

Denetim sırasında, bir soru için **"Uygun Değil"** veya **"İyileştirme
Gerekli"** seçimi yapıldığında:

- **Bulgu Sınıflandırması** alanı görünür olur.

  - Bu alandan, ilgili bulgunun **Değerlendirme Türü** ve **Risk
    Seviyesi** sınıflandırması yapılır.

- İlgili bulgu için aksiyon başlatılması gerekiyorsa, **"NCR"**,
  **"CAPA"** veya **"Aksiyon"** alanlarına tıklanarak gerekli bilgiler
  girilir.

**NCR Girişi**

- **NCR** seçildiğinde, aşağıdaki ekran açılır ve NCR'a ait bilgi
  girişleri yapılır.

- Sistemde **istediğiniz sayıda NCR girişi** gerçekleştirilebilir.

> **Not:** Bu yapı, bulguların sistematik olarak takip edilmesini ve
> gerekli düzeltici/önleyici aksiyonların uygulanmasını sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-H8WOMW2O.png){.adv-wysiwyg-img
block-id="mmj9j844-mtenje-068" mediatype="img" width="538" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:538px;"}

**Aksiyon Girişi**

Denetim sırasında **"Aksiyon"** seçimi yapıldığında:

- Aşağıdaki ekran açılır ve aksiyon ile ilgili bilgi girişi yapılır.

- Sistemde **istediğiniz sayıda aksiyon girişi** gerçekleştirilebilir.

> **Not:** Bu alan, denetim bulgularına ilişkin gerekli düzeltici veya
> iyileştirici aksiyonların sistematik olarak kaydedilmesini sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-T3UYRDY9.png){.adv-wysiwyg-img
block-id="mmj9j844-txrp46-071" mediatype="img" width="535" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:535px;"}

**CAPA Girişi**

Denetim sırasında **"CAPA"** seçimi yapıldığında:

- Aşağıdaki ekran açılır ve CAPA'ya ait bilgi girişi yapılır.

- Sistemde **istediğiniz sayıda CAPA girişi** gerçekleştirilebilir.

> **Not:** CAPA alanı, denetim bulgularına ilişkin düzeltici ve önleyici
> faaliyetlerin planlanması, kaydedilmesi ve takibinin yapılmasını
> sağlar.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-028JFC4R.png){.adv-wysiwyg-img
block-id="mmj9j845-j9kgcl-074" mediatype="img" width="549" height="auto"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:549px;"}

**Bulgulardan Bağımsız Aksiyon, NCR ve CAPA Girişi**

Denetim bulgularından bağımsız olarak, **Aksiyon**, **NCR** ve **CAPA**
girişi yapmak istenirse:

- **Denetim Detayları** alanı üzerinden ilgili bilgi girişi
  gerçekleştirilebilir.

- Bu yöntem, bulgu oluşmasa bile gerekli düzeltici veya önleyici
  kayıtların sisteme eklenmesini sağlar.

> **Not:** Bu özellik, kullanıcıların denetim sürecinde esnek bir
> şekilde aksiyon, CAPA veya NCR kayıtlarını yönetmesine olanak tanır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-OOW2R2HH.png){.adv-wysiwyg-img
block-id="mmj9j845-28c6q7-077" mediatype="img" width="719" height="289"
dataalign="left" datadisplay="flex" data-type="media-content"
fixaspectratio="false" autoaspectratio="true" shadow="yes" border="yes"
round="no" link="" newtab="" style="width:719px;height:289px;"}

**Denetim Değerlendirmesinin Tamamlanması ve Onaylama**

Denetime ilişkin değerlendirme tamamlandıktan sonra, **"İşlem Seç"**
alanından **"Onayla"** seçimi yapıldığında sistem tarafından aşağıdaki
işlemler otomatik olarak gerçekleştirilir:

- **NCR, CAPA ve Aksiyon Atamaları:** İlgili kayıtlar sistemde
  oluşturulur ve gerekli kişilere atanır.

- **Denetim Raporu Oluşturma:** Denetim raporu sistem tarafından
  hazırlanır.

- **Bildirim Gönderimi:** Denetim kapsamında tanımlı kişilere (**Denetim
  Katılımcıları, Baş Denetçi, Denetçi, Denetim Sorumlusu, Denetim
  Planlayan**) rapor ve bilgilendirme **e-posta ile iletilir**.

> **Not:** Bu adım, denetim sürecinin resmi olarak tamamlanmasını,
> bulguların paylaşılmasını ve aksiyonların uygulanmasını sağlar.

- #### [**Denetim Planının Revize Edilmesi_Üst Akış:** ]{type="spanMark" style="color:rgb(41, 98, 246);"} {#denetim-planının-revize-edilmesi_üst-akış block-id="mmja4wax-px4cz9-103"}

  [**Denetim Planının Revize Edilmesi** aşaması, plan sahibi tarafından
  denetim planının güncellendiği adımdır.Plan sahibi bu aşamada
  aşağıdaki kararları verebilir:]{type="spanMark"}

  - [**Denetim İptal:** Denetim planının iptal edilmesi gereken
    durumlarda seçilir ve denetim kapatılır.]{type="spanMark"}

  - [**Onayla:** Talep edilen revizyonlar gerçekleştirilir ve plan,
    **aksiyon ve onaya** yönlendirilir.]{type="spanMark"}

  > [**Not:** Bu adım, denetim planlarının esnek bir şekilde
  > güncellenmesini ve sürecin doğru kişiler tarafından onaylanmasını
  > sağlar.]{type="spanMark"}
