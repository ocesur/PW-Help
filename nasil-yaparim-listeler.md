####  

#### Formda bir [liste ](/tr/docs/b008){rel="nofollow" translate="no"}nasıl sistem listesine bağlanır?

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1647615653007.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

[Liste bileşeni ](/tr/docs/b008){rel="nofollow" translate="no"}sürükle -
bırak ile elektronik form üzerine bırakılır. Özellikler bölümünden Veri
Kaynağı tipi liste seçilir. Hemen altından kullanılmak istenilen liste
seçilir.

Listeler birden fazla kolonlu olabilir. Bu nedenle kaydedilecek ve
görüntülenecek kolonların belirlenmesi gerekir. Kolonlar sıra ile Key1,
Key2.. olarak gider. Görünüm bölümü özellikle bu şekilde bırakılmıştır.
Listelerde her satır için ikon görüntülemek mümkündür.

::::: {.section .warningBox}
:::: title
::: content
Liste alanlarının isimlerinin büyük harf ile başladığı unutulmamalıdır.
Yanlış yazımlarda liste çalışmaz.
:::
::::
:::::

####  Formda ilişkili iki liste nasıl oluşturulur?

Örneğin iller ve ilçeler listelerimiz olsun;

  --------- ----------------
  İl Kodu   İl Adı
  01        Adana
  02        Adıyaman
  03        Afyonkarahisar
  \...      \...
  --------- ----------------

  --------- ----------
  İl Kodu   İlçe Adı
  01        Alemdağ
  01        Ceyhan
  01        Çukurova
  \...      \...
  --------- ----------

Bu durumda 1nci listemizin özellikleri şu şekilde olmalıdır;

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  [Bileşen Adı]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}          [Müşteri İl]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Veri Kaynağı tipi ]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}   [Liste]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Liste Kaynağı]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}        [İller]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Listeyi Dinamik Çağır]{style="color: rgb(184, 49, 47);"}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      [False]{style="color: rgb(184, 49, 47); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; float: none; display: inline !important;"}
  [Kaydedilecek alan]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}    [Key1]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Liste görünümü]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}       \<span\>{{ item.Key2 }}\</span\>
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2nci listemizin özellikleri şu şekilde olmalıdır;

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  [Bileşen Adı]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}           [Müşteri İlçe]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Veri Kaynağı tipi ]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}    [Liste]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Liste Kaynağı]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}         [İlçeler]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Listeyi Dinamik Çağır]{style="color: rgb(184, 49, 47);"}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       [True]{style="color: rgb(184, 49, 47); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; float: none; display: inline !important;"}
  [*Ana Liste Kaynağı*]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}   [Müşteri İl]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Kaydedilecek alan]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}     [Key2]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
  [Liste görünümü]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}        \<span\>{{ item.Key2 }}\</span\>
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Bu durumda her 1nci listeden seçim yapıldığında 2nci liste buna göre
filtrelenir.

::::: {.section .infoBox}
:::: title
::: content
**Listenin Filtrelenmesi**\
Örneğin 2nci listede Liste filtresi alanına A yazılır ise 1nci listede
Adana seçildiğinde 2nci listede sadece A ile başlayan satırlar (Alemdağ)
listelenir.
:::
::::
:::::

\

#### Formda bir [listeye ](/tr/docs/b008){rel="nofollow" translate="no"}dinamik veri nasıl bağlanır?

Aşağıdaki örnek aracılığı ile ilk önce bir liste oluşturulmuş, daha
sonra formun yükleme olayında bu liste ara yüzde bulunan listeye
atanmıştır.

``` {.javascript code-id="section-1660572720830" data-language="javascript"}
//------------ Global Fonksiyonlar----------------------
var userList = [
    { Name:"ali"   , label :"Ali"   },
    { Name:"mehmet", label :"Mehmet"},
    { Name:"yunus" , label :"Yunus" }];
//--------------------------------------------------------
```

``` {.javascript code-id="section-1660572720832" data-language="javascript"}
//------------ Yükleme Sonrası----------------------------
var  listName = "pwselect";
var  key      = "Name";
var  label    = "label"; 
PwForm.fillList(listName, key, label, "userList");
//----------------------------------------------------------
```

Bu kodlar yazıldıktan sonra listenin liste görünümünde görüntülenecek
kolon da yazılmalıdır: \<span\>{{ item.label}}\</span\>

#### Formda bir listenin seçilen değeri nasıl alınır?

Aşağıda pwselect isimli [liste ](/tr/docs/b008){rel="nofollow"
translate="no"}bileşeninin seçili değeri alınmıştır.

``` {.javascript code-id="section-1660572720833" data-language="javascript"}
var listName = "pwselect";
var value    = PwForm.component(listName).SelectedRow.Name;
```

**Çok satırlı bir listede filtreleme ile sonucu nasıl daraltabilirim?**

Bazı listelerde kayıt sayısı çok fazla olduğu için elektronik formun
açılması zorlaşabilir. Veya listeden bir satırın seçimi pratik
olmayabilir. Hele bir de liste diğer sistemlerden (SAP, Logo, veri
tabanı gibi) alınıyor ise tamamını her seferinde almak  performans
problemine sebebiyet verebilir. Örneğin tedarikçi listesi gibi.

Bu durumlarda listenin bir PaperWork listesi ile senkronize edilmesi,
elektronik formların ise bu listeyi dinamik olarak filtrelemesi tavsiye
edilir. Aşağıdaki örnekte liste, PaperWork Listesi ile senkronize
edilmiştir. Filtreleme şu şekilde yapılır;

1.Formun üzerinde ONAY_VEREN isimli bir yazı nesnesi kullanılmıştır. 

2.Eğer arama sonucunda kayıt yok ise kullanıcıyı bilgilendirmek adına
htmlelement isimli bir HTML nesnesi kullanılmış, diğer değeri olarak
\"kayıt bulunamadı\" yazılmıştır. Yazının büyük olması için HTML Tag
özelliğine h4 yazılmıştır.

3.Yine form üzerine bir tuş nesnesi konulmuş ve özel işlem bölümüne
openDialog(); yazılmıştır. Bu aşağıda yazacağımız fonksiyonun adıdır.
Tuş nesnesi salt okunur olarak işaretlenmiştir.

4.Elektronik formun üzerinde bir açılır pencere nesnesi bulunur. Adı
pwdialog1 olarak verilmiştir.

5.Açılır pencere nesnesinin üzerinde bir veri tablosu nesnesi bulunur ve
adı pwkendogrid olarak verilmiştir.

6.Elektronik formun yükleme sonrası olayına aşağıdaki kod yazılmıştır;

``` {.javascript code-id="section-1660573261559" data-language="javascript"}
PwForm.setEvent('ONAY_VEREN', 'Change', function () {
    PwForm.enable('button', PwForm.get("ONAY_VEREN").length > 2);
});
```

Burada ONAY_VEREN isimli yazı nesnesinin değişme olayı için kod
yazılmıştır. Eğer yazı kutucuğuna girilen yazı 2 karakterden büyük ise
formun üzerindeki tuş nesnesi tıklanabilir olur.

7.pwdialog1 nesnesinin kaydetmede özelliğine afterSave(); yazılmıştır.
Bu fonksiyon aşağıdaki gibidir;

``` {.javascript code-id="section-1660574575331" data-language="javascript"}
function afterSave() {
    var selRow = PwForm.component("pwkendogrid").SelectedRow;
    PwForm.set("LOKASYON_ADI", selRow.Key1);
    PwForm.set("MALZEME_ADI", selRow.Key2);
}
```

Bu fonksiyonda seçili liste satırı alınarak değerleri LOKASYON_ADI ve
MALZEME_ADI kolonlarına atanmaktadır.

8.openDialog() fonksiyonu aşağıdaki gibi yazılmıştır;

``` {.javascript code-id="section-1660573456838" data-language="javascript"}
function openDialog() {
    PwForm.show("htmlelement", false);
    PwForm.Progress(true);
    PwForm.getPL("/Services/Lookup/GetListItems", { listName: 'MOBIL_TEST', controlName: 'TEDARIKCI_ADI', filterText: PwForm.get("ONAY_VEREN"), masterCol: '' }).then(result => {
        if (result.Values.length > 0) {
            var hdr = [
                { field: 'Key1', title: 'Type Name' },
                { field: 'Key2', title: 'Type Title' }
            ];
            PwForm.fillGrid('pwkendogrid', result.Values, hdr);
            PwForm.openDialog("pwdialog1", '', DialogData.None);
        }
        else {
            PwForm.show("htmlelement", true);
            PwForm.set("LOKASYON_ADI", "");
            PwForm.set("MALZEME_ADI", "");
        }

        PwForm.Progress(false);
    });

}
```

 Burada fonksiyon ilk çalıştığında htmlelement nesnesi görünüyor ise
görünmez olarak işaretlenir. İşlem boyunca ekran kullanılamaz hale
getirilir. Daha sonra geliştirme katmanı GetListItems metodu
kullanılarak MOBIL_TEST isimli listede TEDARIKCI_ADI kolonunda
ONAY_VEREN yazı alanındaki filtre ile listelenir. Listeleme sonucunda
eğer sonuç yok ise htmlelement nesnesi gösterilir, liste sonucunun
yazılacağı alanlar boşaltılır. 

Eğer filtre sonucunda kayıt var ise  kendogrid ayarları yapılır ve
dialog üzerinde görünmesi sağlanır. Tamam tuşuna basılır ise de
afterSave() fonksiyonu tetiklenir.

Aşağıdaki videoda tüm nesneler ve kodlar gösterilmiştir.

Form üzerinde bulunan listenin seçilen satırına ait birden fazla kolon
değerini bir tabloya yazdırmak için ise aşağıdaki örnek kod
kullanılabilir.

Örnek Kod Global Fonksiyonlarda bulunur.

``` {.javascript code-id="section-1664275850064" data-language="javascript"}
function secilenlisteChange()
{ 
var selList = PwForm.component("okunankitap2").SelectedRow;
PwForm.AddRowData('OKUNAN_KITAPLAR',{        
KITAP_ADI: selList.Key1,        
YAZAR_ADI: selList.Key2,  
YAYIN_EVI: selList.Key3,    
});
}
```

Global Fonksiyonlarda eklenen kod ise Yükleme Sorasından listenin
değişiminde çağrılır.

``` {.javascript code-id="section-1664275958148" data-language="javascript"}
PwForm.setEvent('okunankitap2','Change',function(){
       secilenlisteChange();
    });
```

Ekran görüntüleri aşağıdaki paylaşılmıştır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/GlobalFonksiyonSecilenListe.png){.fr-fil
.fr-dib .fr-draggable .fr-bordered style="height: 75%; width: 75%;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/YuklemeSonrasiSecilenListe.png){.fr-fil
.fr-dib .fr-draggable .fr-bordered style="width: 75%; height: 75%;"}

Diğer bir durum ise Veri Izgarası içerisinde bulunan bir listenin
seçilen satırının tablonun diğer kolonlarına yazdırılmasıdır.

Bu işlem içinde aşağıdaki örnek kod kullanılabilir.

Kod Global Fonksiyonlarda bulunmalıdır.

``` {.javascript code-id="section-1664276372050" data-language="javascript"}
function tablosecilenlisteChange()
{ 
var selList = PwForm.component("okunankitap1").SelectedRow;
//PwForm.Info(PwForm.Culture("Okunan Kitap Adı"),PwForm.Culture(''+ selList.Key1 +'') + "  -  Yazar Adı" + PwForm.Culture(''+ selList.Key2 +'') + "  -  Yayın Evi Adı" +PwForm.Culture(''+ selList.Key3 +''));
PwForm.set('KITAP_ADI',selList.Key1);
PwForm.set('YAZAR_ADI',selList.Key2);
PwForm.set('YAYIN_EVI',selList.Key3);

}
```

Veri Izgarasının özelliklerinde Tablo Özellikleri başlığı altındaki
Kaydetme de kısmında bu eklenen kod çağrılmalıdır.

Ekran görüntüsü aşağıda paylaşılmıştır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/GlobalFonksiyonSecilenListe(1).png){.fr-fil
.fr-dib .fr-draggable .fr-bordered style="width: 75%; height: 75%;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/TabloOzellikleriListe.png){.fr-fil
.fr-dib .fr-draggable .fr-bordered style="width: 75%; height: 75%;"}

Bu iki çalışmanın örneklendiği video eğitimini izleyebilrisiniz.

[]{.fr-video .fr-deletable .fr-fvl .fr-dvb .fr-draggable
contenteditable="false" draggable="true"}\
