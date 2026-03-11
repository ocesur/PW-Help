#### Form üzerinden E-Posta gönderme

Elektronik posta gönderimi için kullanılan form üzerinden elektronik
postayı kime göndereceğimiz, bilgi alanına kimlerin ekleneceği, mailin
konusu ve mail şablonunu belirleyebildiğimiz basit bir arayüz oluşturmak
mümkündür.

Öncelikte aşağıdaki gibi basit bir form tasarımı yapılmalı.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679655317473.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Bu noktada kendi yazacağımız ve "Mail Gönder" butonu arkasında
çalıştıracağımız fonksiyonu yazmamız gerekiyor. Kodlama kısmında aşağıda
bulunan örnek kod parçası üzerinden çalışmalarımızı yaparak mail
gönderimini sağlayabiliriz.

``` {.javascript code-id="section-1679655392314" data-language="javascript"}
function SendMail() {
    PwForm.getPL("/Services/Lookup/GetMailBodyTemplates", { templateName: PwForm.get('MAIL_SABLONU') }).then(fobject => {
        for (var template of fobject) {
            if (template.Name === PwForm.get('MAIL_SABLONU')) {
                var mt = PwForm.newTemplate();          //Yeni mail taslağı oluşturmak için kullanılır.
                mt.From = "argus";                      //Maili gönderen kişinin adı ve adresini belirtmek için kullanılır.
                mt.To = PwForm.get('MAIL_TO');          //Maili alanın adresi tanımlamak için kullanılır.
                mt.Subject = PwForm.get('MAIL_KONU');   //Mailin başlığını tanımlamak için kullanılır.
                mt.CC = PwForm.get('CC_EKLENEN');       //Mailin bir kopyasını göndermenize olanak tanır.
                mt.BodyTemplateId = template.ObjectId;
                PwForm.sendMail(PwForm.ObjectId, mt, true).then(result => {     //PwForm.sendMail() geliştime katmanı üzerinden mailin gönderilmesini sağlayan fonksiyondur.
                    if (result.ErrorCode !== 0)                                 //Parametre olarak akışın ObjectId değeri, mail taslağı ve mailin gerçek zamanlı gönderilmesini sağlayan (true/false) değer gönderilir. 
                        PwForm.Info("Hata", "Eposta gönderilemedi : " + result.Message);     //Mail gönderim sırasında bir hata ile karşılaşılıp karşılaşılmadığına dair uyarı mesajı almamıza olanak tanır.
                });
            }
        }
    });
}
```

Form dizayn alanımız içerinde "Mail Gönder" butonu üzerine faremiz ile
geldiğimizde çıkan çark işareti ile butonumuzun ayarlarını açtıktan
sonra "Özel İşlem" alanına kodlama kısmında yazdığımız fonksiyonun
tanımlamasını yaparak çalışmasını sağlıyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679655443991.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Bu işlemlerin ardından "Mail Gönder" butonuna tıkladığımızda kullanıcıya
gönderilen mailin içeriği aşağıdaki gibi olacaktır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679655478912.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Oluşturulan mail taslağı üzerinden mail içeriği detaylandırılıp
göndermek istenilen mail tasarımı yapılabilir.

#### Seçilebilir Veri Tablosunda Otomatik Seçim Nasıl Yapılır?

Tablomuzun önceki hali aşağıdaki şekildedir. Malzeme Adı listesinden
seçilen değere eşit olan tüm satırları toplu sekilde seçip
belirginleştirmek istiyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680176967108.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Global Fonksiyonlara yazdığımız TopluSec fonksiyonunu, "Toplu Seç"
butonu arkasında çağırarak, buton tıklamasında bu işlemi
gerçekleştirebiliriz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680176993244.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

``` {.javascript code-id="section-1680177023738" data-language="javascript"}
function TopluSec() {

    PwForm.component("MASRAF_LISTESI").redraw();
    var grid = $('#' + "T_YAZILIM_MALIYET" + "_" + "MASRAF_LISTESI").data("kendoGrid");

//$("# + Tip Adı +  _  + Tablo Tipi Alan Adı).data("kendoGrid");  “kendoGrid” kısmı sabit olmalıdır.

    for (var i = 0; i < grid._data.length; i++) {
        if (PwForm.get("MalzemeAdi") === grid._data[i].MALZEME_ADI) {
            var row = grid.table.find("[data-uid=" + grid.dataSource._data[i].uid + "]");
            grid.select(row);
        }
    }
}
```

Sayfalanabilir veri tablosu nesnelerinde, sayfa değiştiğinde otomatik
olarak seçim isleminin yapılması istendiği takdirde, yükleme sonrasına
yazılacak aşağıdaki kod parçacığı ile istediğimiz işlem
gerçekleşecektir.

NOT: Bu işlemin çalışması için ilk önce en az bir kez sıralama işlemi
yapılmalıdır. (TopluSec metodu çalıştırılmalıdır). Ayrıca veri tablosuna
satır ekle, düzenle ve sil işlemlerinde seçimler kalkacaktır.

``` {.javascript code-id="section-1680177100278" data-language="javascript"}
var grid = $('#' + "T_YAZILIM_MALIYET" + "_" + "MASRAF_LISTESI").data("kendoGrid");

grid.bind("dataBound", TopluSec);

grid.dataSource.fetch();
```

#### Veri Tablosunda Otomatik Filtreleme İşlemi Nasıl Yapılır?

Tablomuz başlangıçta aşağıdaki gibidir. Yükleme sonrasında, Malzeme Adı
alanındaki değere göre veri tablomuzdaki datayı Malzeme Adı kolonu
üzerinde filtrelemek istiyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680177252553.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

``` {.javascript code-id="section-1680177315596" data-language="javascript"}
function OtomatikFiltrele() {
 
    var ds = $('#' + "T_YAZILIM_MALIYET" + "_" + "MASRAF_LISTESI").data("kendoGrid").dataSource;
//$("# + Tip Adı +  _  + Tablo Tipi Alan Adı).data("kendoGrid");  “kendoGrid” kısmı sabit olmalıdır.

    try {
//Mevcut filtre varsa getirilir. Mevcut filte yok ise catch’e düşer.
        var curr_filters = ds.filter().filters;
//Yeni filtre oluşturulur.
        var new_filter = { field: "MALZEME_ADI", operator: "eq", value: PwForm.get("MalzemeAdi") };
//Yeni filtre, mevcut filtrelere eklenir.
        curr_filters.push(new_filter);
//Veri kaynağındaki filtreler güncellenir.
        ds.filter(curr_filters);
//İstenirse logic değiştirilir.
        ds._filter.logic = 'and'
//Veri kaynağı tekrar yüklenir.
        $('#' + "T_YAZILIM_MALIYET" + "_" + "MASRAF_LISTESI").data("kendoGrid").dataSource.read();
    } catch (ex) {
        var new_filter = { field: "MALZEME_ADI", operator: "eq", value: PwForm.get("MalzemeAdi") };
        ds.filter(new_filter);
        ds._filter.logic = 'and'
        $('#' + "T_YAZILIM_MALIYET" + "_" + "MASRAF_LISTESI").data("kendoGrid").dataSource.read();
    }
}
```

Verilebilecek operator değerleri aşağıdaki gibidir.

- \"neq\" =\> eşit değil
- \"eq\" =\> eşit
- \"startswith\" =\> ile başlar
- \"contains\" =\> içeriyor
- \"doesnotcontain\" =\> içermiyor
- \"endswith\" =\> ile biter
- \"isnull\" =\> null (bir value değeri vermeyi gerektirmez.)
- \"isnotnull\" =\> null değil (bir value değeri vermeyi gerektirmez.)
- \"isempty\" =\> boş (bir value değeri vermeyi gerektirmez.)
- \"isnotempty\" =\> boş değil (bir value değeri vermeyi gerektirmez.)
- \"isnullorempty\" =\> null veya boş (bir value değeri vermeyi
  gerektirmez.)
- \"isnotnullorempty\" =\> null veya boş değil (bir value değeri vermeyi
  gerektirmez.)

Verilebilecek logic değerleri aşağıdaki gibidir.

- \"and\" =\> ve
- \"or\" =\> veya

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680177417895.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680177426689.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 1047px;"}

::::: {.section .infoBox}
::: title
Not
:::

::: content
Satır ekle, sil ve düzenle işlemlerinde filtre kalkacaktır. Tekrar
filtrelenmesi halinde OtomatikFiltrele fonksiyonu tekrar çağırılmalıdır.
:::
:::::

#### Elektronik Formlarda Seçilen Satıra Göre Tablonun Düzenle ve Kaldır Butonlarının Kaldırılması

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680246081622.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Hazırlayacağımız fonksiyonun tablonun seçilen değiştiğinde alanında
çağırılması gerekmektedir.

Kendi isimi ile kaydedilen açıklama tablosu satırını düzenleyebiliyor
veya kaldırabiliyor.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680246112630.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

``` {.javascript code-id="section-1680246125824" data-language="javascript"}
function onRowChanged() {
  debugger;
  if (PwForm.component('ACIKLAMA_TABLOSU').SelectedRow != null) {
    if (PwForm.component('ACIKLAMA_TABLOSU').SelectedRow.ACIKLAMA_SAHIBI != CurrentUser.UserName) {
      PwForm.component("ACIKLAMA_TABLOSU").bar.children[1].remove();//düzenle butonu
      PwForm.component("ACIKLAMA_TABLOSU").bar.children[1].remove();//sil butonu
      //ilk buton silindikten sonra diğer butonların indexleri değiştiği için iki butonun indekside 1'e denk geldi. Bu yüzden ikisi içinde index 1 olmalıdır.
      //Veya aşağıdaki gibi component özelliklerinden ilerleyerek, tablonun düzenleme ve silme özelliklerini kaldırabilriz.
      PwForm.component("ACIKLAMA_TABLOSU").component.editable = false;
      PwForm.component("ACIKLAMA_TABLOSU").component.deleteable = false;
      PwForm.component("ACIKLAMA_TABLOSU").redraw();
      }
   }
}
```

\

\

\
