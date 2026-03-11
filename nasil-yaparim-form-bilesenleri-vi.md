**Bir Diyalog Nasıl Açarım?**

Aşağıdaki örnekte HTML bileşeni yardımı ile bir diyalog açılmıştır.

1.Elektronik form üzerine bir \"Açılır Pencere\" nesnesi yerleştirilir.
Adı örneğin pwdialog olsun. Açılır pencere bileşeni için [şu
sayfa](/tr/docs/p50050401003-17){rel="nofollow" translate="no"}
incelenebilir.

2.Bu dialog nesnesi üzerine bir html bileşeni koyalım. Örneğin adı
pwhtml3 olsun. HTMLbileşeni için [şu
sayfa](/tr/docs/p50050401003-11){rel="nofollow" translate="no"}
incelenebilir. Bu bileşenin özelliklerinde diğer bölümüne aşağıdaki HTML
kodunu yazalım.

``` {.markup code-id="section-1669040433403" data-language="markup"}
Merhaba,<br>
Bu bir dialog penceresidir.<br>
Bu ekranda herhangi bir nesneyi gösterebilir,
<br>açıklama yada imaj ekleyebilirsiniz.
<br>
<center><img src="/Content/archive/img/0.PNG"/>--Bu satır sunucuda bulunan bir imajı HTML içinde gösterir
</center>
```

3.Yine formun üzerine hangi tuşa basıldığını almak için bir html
bileşeni koyduğumuzu ve adının pwhtml14 olduğunu düşünelim.

4.pwdialog nesnesinin kaydetmede olayında şu kodu yazalım.

``` {.javascript code-id="section-1669040433408" data-language="javascript"}
PwForm.set("pwhtml4",'<b>Tamam</b> tuşuna basıldı');
PwForm.component("pwhtml4").redraw();
```

Aynı şekilde pwdialog nesnesinin iptalde eventinde şu kodu yazalım.

``` {.javascript code-id="section-1669040433414" data-language="javascript"}
PwForm.set("pwhtml4",'<b>Vazgeç</b> tuşuna basıldı');
PwForm.component("pwhtml4").redraw();
```

5.Ekrana bir pwbutton nesnesi koyalım ve tuşa basıldığında çalışması
için özelliklerinde özel işlem bölümüne şu kodu yazalım.

``` {.javascript code-id="section-1669040433416" data-language="javascript"}
showDialog();
```

6.Global fonksiyonlarda ise showDialog kodunu yazalım;

``` {.javascript code-id="section-1669040433418" data-language="javascript"}
function startTimer(duration) {
    myInterval(duration);
}

function myInterval(duration) {
    setTimeout(function () {
        if (--duration < 1) {
            PwForm.component("pwdialog").show(false);
        }
        else {
            seconds = duration < 10 ? "0" + duration : duration;
            $('#formio #time').text(seconds);
            if (PwForm.component("pwdialog").visible)
                myInterval(duration);
        }
    }, 1000);
}

function showDialog() {
debugger;
    PwForm.openDialog("pwdialog", '', DialogData.None);
    var delay = 30;
    startTimer(delay);
}
```

7.showDialog fonksiyonu startTimer adında bir fonksiyonu tetikler. Bu
fonksiyon da myInterval adında fonksiyonu çağırır. Örneğe göre bu
fonksiyon 1 saniyede 1 diyaloğun üzerindeki html nesnesini değiştirir ve
toplam verilen sürenin sonunda otomatik olarak kapanmasını sağlar.

Tüm bu yazılanlar ile beraber elektronik form üzerindeki dialog şu
şekilde çalışır.

**Dialog üzerinde Veri Tablosu Nasıl Gösteririm?**

1.Elektronik formun üzerine bir Açılır Pencere nesnesi yerleştirelim ve
adını pwdialog1 olarak atayalım. Bu nesnenin özelliklerini [bileşen
sayfasından](/tr/docs/p50050401003-17){rel="nofollow" translate="no"}
inceleyebilirsiniz.

2.Açılır pencere bileşeni üzerine bir Veri Tablosu yerleştirelim ve
adını pwkendogrid olarak verelim. Bu nesnenin özelliklerini [bileşen
sayfasından](/tr/docs/p50050401003-09){rel="nofollow" translate="no"}
inceleyebilirsiniz.

3.Veri tablosu için elektronik formun açılışında verileri dinamik bir
şekilde aşağıdaki gibi oluşturalım. Bunun yeriNe veri tablosu nesnesini
dilediğiniz gibi doldurabilirsiniz.

``` {.javascript code-id="section-1669040433420" data-language="javascript"}
var hs = [
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
    { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Kırtasiye 4', ORAN: '13', VADE: '12', BAKIYE: 10000 },
    { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Kırtasiye 5', ORAN: '14', VADE: '24', BAKIYE: 15000 },
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
    { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Kırtasiye 4', ORAN: '13', VADE: '12', BAKIYE: 10000 },
    { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Kırtasiye 5', ORAN: '14', VADE: '24', BAKIYE: 15000 },
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
    { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Kırtasiye 4', ORAN: '13', VADE: '12', BAKIYE: 10000 },
    { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Kırtasiye 5', ORAN: '14', VADE: '24', BAKIYE: 15000 },
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
    { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Kırtasiye 4', ORAN: '13', VADE: '12', BAKIYE: 10000 },
    { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Kırtasiye 5', ORAN: '14', VADE: '24', BAKIYE: 15000 },
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
    { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Kırtasiye 4', ORAN: '13', VADE: '12', BAKIYE: 10000 },
    { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Kırtasiye 5', ORAN: '14', VADE: '24', BAKIYE: 15000 },
    { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Kırtasiye 1', ORAN: '10', VADE: '3', BAKIYE: 1000 },
    { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Kırtasiye 2', ORAN: '11', VADE: '6', BAKIYE: 3000 },
    { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Kırtasiye 3', ORAN: '12', VADE: '9', BAKIYE: 5000 },
];

PwForm.AddRowDataFull('pwkendogrid', hs);
```

4.Dialoğu açmak için elektronik form üzerine bir tuş koyalım ve özel
işlem bölümüne aşağıdaki kodu yazalım.

``` {.javascript code-id="section-1669040433428" data-language="javascript"}
openDialog2();
```

5.Elektronik formun global fonksiyonlar bölümüne de şu kodu yazalım.

``` {.javascript code-id="section-1669040433430" data-language="javascript"}
function openDialog2() {
    PwForm.openDialog("pwdialog1", '', DialogData.None);
}
```

Bu kodlama ile beraber aşağıdaki videoda olduğu gibi Açılır Pencere
nesnesini elektronik form üzerinde gösterebiliriz.

**Dialog üzerinde bir tipin tablo verisini göstererek nasıl
değiştirebilirim?**

1.Bu örnekte tip üzerinde hesaplar isminde bir tablo bulunur.

2.Ekrana bir Açılır Pencere nesnesi yerleştirilir ve adı pwdialog3 olur.

3.Açılır Pencere nesnesinin üzerine bir veri tablosu eklenir ve adı
pwkendogrid1 olur.

4.Veri Tablosu nesnesi üzerine kolonlardan bir form oluşturulur.
hesaplar tablosundan Hesap No, Hesap tipi gibi alanlar uygun bileşenler
ile yerleştirilir.

5.Ekrana bir tuş nesnesi konur ve özel işlem bölümüne aşağıdaki gibi kod
eklenir.

``` {.javascript code-id="section-1669040433431" data-language="javascript"}
openDialog3();
```

6.Global Fonksiyonlar bölümüne openDialog3() fonksiyonu eklenir.

``` {.javascript code-id="section-1669040433433" data-language="javascript"}
function openDialog3() {
    PwForm.openDialog("pwdialog3", 'pwkendogrid1', DialogData.Data, PwForm.form.data.HESAPLAR);
}
```

7.Örnek kodu oluşturma esnasında ekrana kayıtların gelmesi açısından
aşağıdaki kod yükleme sonrası olayına eklenmiştir. Normalde tasarım
esnasında tip verisi olmayacağı için bu dialoglar boş gelir.

``` {.javascript code-id="section-1669040433434" data-language="javascript"}
PwForm.AddRowData('HESAPLAR', { HESAP_NO: 'Hesap 1', HESAP_TIPI: 'Vadeli', ORAN: '10', VADE: '3', BAKIYE: 1000 });
PwForm.AddRowData('HESAPLAR', { HESAP_NO: 'Hesap 2', HESAP_TIPI: 'Vadeli', ORAN: '11', VADE: '6', BAKIYE: 3000 });
PwForm.AddRowData('HESAPLAR', { HESAP_NO: 'Hesap 3', HESAP_TIPI: 'Vadeli', ORAN: '12', VADE: '9', BAKIYE: 5000 });
PwForm.AddRowData('HESAPLAR', { HESAP_NO: 'Hesap 4', HESAP_TIPI: 'Vadeli', ORAN: '13', VADE: '12', BAKIYE: 10000 });
PwForm.AddRowData('HESAPLAR', { HESAP_NO: 'Hesap 5', HESAP_TIPI: 'Vadeli', ORAN: '14', VADE: '24', BAKIYE: 15000 });
```

8.Yapılan çalışma ile beraber aşağıda videoda görüldüğü gibi tablo
nesnesi bir dialog ile açılır. Açılan dialoğun özelliklerine göre
dialogtaki tuşlar aktif olur.

**Bir Dialog yardımı ile nasıl belge görüntülerim?**

Bu örnek ile PaperWork Viewer kullanılarak elektronik form üzerinde bir
belge görüntülenmiştir. Bunu yapmak için aşağıdaki adımlar kullanılır.

1.Ekrana bir açılır pencere yerleştirelim ve adı pwdialog5 olsun.

2.Ekrana bir html bileşeni koyalım ve adı pwhtml8 olsun. Bu bileşenin
diğer bölümüne aşağıdaki kodu yazalım.

``` {.javascript code-id="section-1690546808285" data-language="javascript"}
<div id="objectViewer" 
 style="max-height:600px;height:600px!important;overflow-y:auto;overflow-x:hidden;margin:0px 5px;">nesne</div>
   Nesne Buraya Gelecek
 </div>
```

3.Ekrana bir yazı nesnesi koyalım be adını txObjectId koyalım.
Görüntülenecek olan belgenin nesne numarasını bu yazı nesnesinden
alacağız.

4.Ekrana bir tuş nesnesi koyalım ve Özel İşlem bölümüne aşağıdaki kodu
yazalım.

``` {.javascript code-id="section-1669040433442" data-language="javascript"}
openDoc();
```

5.Global fonksiyonlarda openDoc() fonksiyonunu aşağıdaki gibi yazalım.

``` {.javascript code-id="section-1669040433443" data-language="javascript"}
function openDoc() {
    var id = PwForm.get('txObjectId');
    PwForm.openDocument('pwdialog5', "objectViewer", id, true); //Verilen Objeyi dialog olarak açar.
}
```

6.Yazılan fonksiyonda txObjectId yazı alanında bulunan nesne numarası
alınarak diyaloğa verilmektedir. Son bölümde fonksiyona verilen true
parametresi açılacak olan görüntüleyicinin salt okunur açılmasını
sağlar. false değerinde ise kullanıcı yetkileri ile açılır. Salt okunur
durumda iken belgenin diske kaydetme fonksiyonu bulunmaz.

7.Yapılan uyarlama sonucunda belge açma ekranı aşağıdaki videoda olduğu
gibi çalışır.

**Başka bir elektronik formu nasıl açarım?**

Aşağıdaki örnek ile bir elektronik formdan tuş yardımı ile başka bir
elektronik form açılmakta, açma esnasında bir alan değeri atanmakta,
tamam ile kapatıldığı durumda da değerin çağıran elektronik forma
yazılması sağlanmaktadır.

1.Sekmeler adında bir elektronik form bulunmaktadır. Formda Müşteri No
ve Müşteri Adı alanları bulunur.

2.Formu açacak elektronik form üzerine pwdialog6 adında açılır pencere
nesnesi yerleştirilir.

3.pwdialog6 penceresi üzerine pwhtml9 isimli bir HTML nesnesi
yerleştirilir. Bu nesnenin değer bölümüne aşağıdaki kod yazılır.

``` {.javascript code-id="section-1669040433445" data-language="javascript"}
 <div id="objectViewer1" 
 style="max-height:600px;overflow-y:auto;overflow-x:hidden;margin:0px 5px;">
   Form buraya gelecek
   </div>
```

4.Açılacak formun adı bir yazı nesnesinden alınacaktır. Yazı nesnesinin
adı txObject2 olarak verilmiştir.

5.Sekmeler nesnesinden alınan MUSTERI_ADI değeri txResult adında bir
yazı alanına yazılacağı için bu nesne de forma yerleştirilir.

6.Formu açmak için ekrana bir tuş nesnesi yerleştirilir ve aşağıdaki kod
Özel İşlem bölümüne yazılır.

``` {.javascript code-id="section-1669040433446" data-language="javascript"}
openDoc2();
```

7.Kodlama bölümünde openDoc2() fonksiyonu yazılır. Yazım esnasında
yükleme öncesi ve kaydetme sonrası olaylarının fonksiyonları da yazılır.

``` {.javascript code-id="section-1669040433447" data-language="javascript"}
function afterLoad(e) {
    e.data.MUSTERI_NO = 'Must 001';
}
function afterSave(e) {
    PwForm.set("txResult", e.data.MUSTERI_ADI);  // Dialogun tamam butonuna basıldıktan sonra yapılan güncelleme
}
function openDoc2() {
    var formName = PwForm.get('txObject2'); //Açılacak Form.
    PwForm.formDialog('pwdialog6', formName, afterLoad, afterSave);
}
```

8.Yukarıda openDoc2 fonksiyonunun açılması esnasında çalışması amacı ile
afterLoad fonksiyonu yazılmıştır. Bu fonksiyonda açılacak formun
MUSTERI_NO alanına değer atanmıştır.

9.Aynı şekilde dialog kapatıldıktan sonra değişen veriyi almak amacı ile
afterSave fonksiyonu yazılmıştır. Bu fonksiyonda MUSTERI_ADI yazı
alanının değeri txResult isimli çağıran formdaki yazı alanına
atanmıştır.

10.Tüm yazılan kodlar ile beraber işleyiş aşağıdaki videoda
gösterilmiştir.

**[]{style="font-size: 18px;"}**[**Elektronik Formda pop up form nasıl
açarım ve sonucunu nasıl
kaydederim?**]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}**

Yapılan çalışmanın videosu ekteki gibidir.

Forma düzenleme araçlarından "Açılır Pencere" eklenir.  Açılır Pencere
nesnesine ise Genel başlığı altındaki HTML Nesnesi eklenir. HTML
Nesnesinin Değer kısmına aşağıdaki kod yazılır.

``` {.markup code-id="section-1669040433449" data-language="markup"}
<div id="objectViewer1" 
 style="max-height:600px;overflow-y:auto;overflow-x:hidden;margin:0px 5px;">
   Form buraya gelecek
   </div>
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644673130335.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable style="width: 932px;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1685620135310.png){.fr-fic
.fr-fil .fr-dib .fr-draggable}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644673158040.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

::::: {.section .warningBox}
::: title
Özellikler,
:::

::: content
[Özellikler alanında bulunan \"Özellik\" ve \"Değer\" kutucukları, kodun
çalışmasını etkileyen
parametrelerdir.]{style="color: rgb(127, 100, 22); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(253, 242, 206); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
Yukarıdaki örnekte Değer editörüne girilen kodun sağlıklı çalışması için
bu kutucuklarda herhangi bir veri kaydı olmamalıdır. Aksi durumda kod
hata verebilir veya beklenmeyen bir şekilde davranabilir. Bu nedenle, bu
kutucukların boş bırakılması önemlidir.
:::
:::::

\

Tuş nesnesinin Özel işlem bölümüne **openDoc2();** yazılır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644673209983.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

Formun Kodlama kısmında Global Fonksiyonlara aşağıdaki kodlar eklenir.

``` {.javascript code-id="section-1669040433451" data-language="javascript"}
//*********************FormDialog Örneği Başlangıç***********************//

function afterLoad(e) {
    //açılan formdaki alanları doldurmak için afterLoad(e) kullanılır.....................
    e.data.KITAP_ADI = 'YAŞAM 3.0';
    e.data.YAZAR_ADI = 'Max Tegmark';
    e.data.YAYIN_TARIHI = PwForm.moment().toDate();
    e.data.SAYFA_SAYISI = 464;
    e.data.YAYIN_EVI = 'Pegasus Yayınevi';
}

function afterSave(e) {
    //açılan POP-UP formdaki alanların değerlerini Tamam butonuna basıldığında ana formdaki alanlara set etmek için afterSave(e) kullanılır........
    PwForm.set("ADI_SOYADI", e.data.KITAP_ADI); 
    PwForm.set("ONAY_TARIHI", e.data.YAYIN_TARIHI); 
    PwForm.set("ONAY_DURUMU", e.data.YAYIN_EVI); 
}

function openDoc2() {
    //dialog içerisinde hangi formun açılacağı burada belirtilir. Bu function tuşun tuklama olayında yada bir nesnein değişiminde çağrılabilir....
    var formName = PwForm.get('FORM_ADI'); //Açılacak Form adı.
    PwForm.formDialog('dialog', formName, afterLoad, afterSave); //'dialog' Açılır Pencerenin adıdır.
}

//*********************FormDialog Örneği Bitiş***********************//
```

**[]{style="font-size: 18px;"}**[**Elektronik Formda Pop up form ile
tabloya satır ekleme ve seçili satırı güncelleme nasıl
yapılır?**]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}**

Forma düzenleme araçlarından "Açılır Pencere" eklenir. Açılır Pencere
nesnesine ise Genel başlığı altındaki HTML Nesnesi eklenir. HTML
Nesnesinin Değer kısmına aşağıdaki kod yazılır.

``` {.markup code-id="section-1669040433453" data-language="markup"}
<div id="objectViewer1" 
 style="max-height:600px;overflow-y:auto;overflow-x:hidden;margin:0px 5px;">
   Form buraya gelecek
   </div>
```

Tabloya Satır eklemek için kullanılan tuş nesnesinin Özel işlem bölümüne
**onClickBtnAciklamaDetayi();** yazılır. Tablodaki Seçili satırı
güncellemek için kullanılan tuş nesnesinin Özel İşlem bölüme
**onClickBtnGuncellemeDetayi();** yazılır. Formun Kodlama kısmında
Global Fonksiyonlara aşağıdaki kodlar eklenir;

``` {.javascript code-id="section-1669040433457" data-language="javascript"}
//********FormDialog örneği Tabloya Ekleme Başlangıç********************//
function onClickBtnAciklamaDetayi() {
try {
    var dialogName = "dialog";
    var formName = PwForm.get('FORM_ADI');
    PwForm.formDialog(dialogName, formName, (e) => 
    { 
        //Açılan pop-up formunun alanlarını doldurmak için yazıldı Form Boş gelmesi için kapatıldı
        /*
        e.data.KITAP_ADI = 'YAŞAM 3.0'; // 'YAŞAM 3.0' yerine PwForm.get('FORM_ADI'); şeklinde yazarak formdaki alan buraya set edilebilir.
        e.data.YAZAR_ADI = 'Max Tegmark';
        e.data.YAYIN_TARIHI = PwForm.moment().toDate(); 
        e.data.SAYFA_SAYISI = 464;
        e.data.YAYIN_EVI = 'Pegasus';
        */
    },
        (e) => {    
            //Tamam butonuna basınca formdaki tabloyu doldurmak için yazıldı. OKUNAN_KITAPLAR grup adıdır. 
        PwForm.AddRowData('OKUNAN_KITAPLAR',{
        KITAP_ADI: e.data.KITAP_ADI,
        SAYFA_SAYISI: e.data.SAYFA_SAYISI,
        YAZAR_ADI: e.data.YAZAR_ADI,
        YAYIN_EVI: e.data.YAYIN_EVI,
        YAYIN_TARIHI: e.data.YAYIN_TARIHI,
    });
});
}
catch (error) {
throw Error(`onClickBtnAciklamaDetayi error: ${error}`)
}
}
//********FormDialog örneği Tabloya Ekleme Bitiş********************//

//********FormDialog örneği Tablodaki satırı güncelleme Başlangıç********************//
function onClickBtnGuncellemeDetayi() {
try {
const selectedRow = PwForm.component("OKUNAN_KITAPLAR").SelectedRow;
if (selectedRow !== null) {
var dialogName = "dialog";
var formName = PwForm.get('FORM_ADI');
PwForm.formDialog(dialogName, formName, (e) => 
{
e.data.KITAP_ADI = selectedRow.KITAP_ADI;
e.data.YAZAR_ADI = selectedRow.YAZAR_ADI;
e.data.YAYIN_TARIHI = selectedRow.YAYIN_TARIHI;
e.data.SAYFA_SAYISI = selectedRow.SAYFA_SAYISI;
e.data.YAYIN_EVI = selectedRow.YAYIN_EVI;
},
(e) => { 
 selectedRow.KITAP_ADI=e.data.KITAP_ADI;
 selectedRow.YAZAR_ADI=e.data.YAZAR_ADI;
 selectedRow.YAYIN_TARIHI=e.data.YAYIN_TARIHI;
 selectedRow.SAYFA_SAYISI=e.data.SAYFA_SAYISI;
 selectedRow.YAYIN_EVI=e.data.YAYIN_EVI;

});
}
else
PwForm.Error("Uyarı", "Tablodan satir seçmelisiniz!");
} catch (error) {
throw Error(`onClickBtnGuncellemeDetayi error: ${error}`)
}
}
//********FormDialog örneği Tablodaki satırı güncelleme Bitiş********************//
```

**[]{style="font-size: 18px;"}**[**Elektronik Formda Pop up formun
genişliği nasıl
ayarlanır?**]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}**

[Elektronik formda bir tuş yardımı ile başka bir formu görüntülemek
ihtiyacı
olabilir. ]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}

Açılan pop -up formun genişliğini ayarlamak için, açılır pencere
nesnesinin otomatik açılır pencere genişliği seçeneği kaldırılmalı ve
hemen altında görünür olan açılır pencere genişliği değerini girerek
yapabilirsiniz.

Ayrıca pencere pozisyonu seçeneklerinden uygun olanı seçerek açılan pop
up formun konumu belirlenebilir. Seçenekler arasında Form, Pencere ve
Ekran seçimleri vardır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/A%C3%A7%C4%B1l%C4%B1r%20Pencere%20Geni%C5%9Fli%C4%9Fi.png){.fr-fil
.fr-dib .fr-bordered .fr-draggable}

Açılan Pup up formun kendisinde kolon nesnesi var ise ve bu kolon
nesnesinin sadece bir hücresine nesneler yerleştirilmiş ve diğeri boş
bırakılmışsa bu durumda açılan sayfada boş bırakılan bölüm için boş bir
alan görülmektedir. Bu boş olan alanı kaldırmak için ise açılır pencere
içerisinde çağrılan formun tasarım ekranında kolon nesnesinin
özellikleri arasında bulunan kolonları otomatik ayarla ve çocukları
gizlenmiş ise kolonu gizle seçeneklerini seçerek yapabilirsiniz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/Kolonlar%20Nesnei%20Otomatik%20Ayarla.png){.fr-fil
.fr-dib .fr-bordered .fr-draggable}

Kolonları otomatik ayarla seçeneği işaretli olmayan bir formun tasarım
ve ön izleme ekran görüntüleri aşağıdaki gibidir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/Okunan%20Kitaplar%20Popup%20Form%20Tasar%C4%B1m%C4%B1.png){.fr-fil
.fr-dib .fr-bordered .fr-draggable style="width: 800px;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/Kolonlar%20nesnesi%20otomatik%20olarak%20ayarl%C4%B1%20de%C4%9Fil.png){.fr-fil
.fr-dib .fr-bordered .fr-draggable}

Kolonları otomatik ayarla ve Çocukları gizlenmiş ise Kolonları gizle
seçenekleri aktif edildiğinde ki ekran görüntüsü aşağıdaki gibidir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/Kolonlar%20nesnesi%20otomatik%20olarak%20ayarl%C4%B1.png){.fr-fil
.fr-dib .fr-bordered .fr-draggable}

Yapılan çalışmanın videosu aşağıdaki gibidir. 

[]{.fr-video .fr-deletable .fr-fvl .fr-dvb .fr-draggable
contenteditable="false" draggable="true"}

#### Dialog Örnekleri

[**\* Dialog Type : None**]{style="color: rgb(41, 105, 176);"}

Bu tür dialog nesnesi boş veri ile kullanılmak içindir. Bu türde sadece
dialogName parametresi kullanılır. Diğer parametreler geçersizdir.

Paremetreler sırasıyla dialogName, gridName, dialogType, data, headers,
plugin şeklindedir.

dialogName : Dialog nesnesinin adı

gridName : Boş

dialogType : Dialog nesnesinin türü

data : Boş

headers : Boş

plugin : Boş

``` {.javascript code-id="section-1669040681070" data-language="javascript"}
function getNoneDialogData() {
  var headers = [];
  PwForm.openDialog('dialog', '', DialogData.None, '', '', '');
}
```

[**\* Dialog Type : SQL**]{style="color: rgb(41, 105, 176);"}

Bu tür dialog nesnesi veritabanından gelen data ile kullanılmak içindir.
Bu türde data parametresine sql sorgusu yazılır. Farklı bir veri
tabanından veri çekilecekse son parametreye plugin adı yazılır.

Paremetreler sırasıyla dialogName, gridName, dialogType, data, headers,
plugin şeklindedir.

dialogName : Dialog nesnesinin adı

gridName : Dialog nesnesinin içinde kullanılacak olan tablonun adı

dialogType : Dialog nesnesinin türü

data : SQL sorgusu

headers : Kullanılan tablo için kolon başlıkları

plugin : Boş

``` {.javascript code-id="section-1669040950487" data-language="javascript"}
function getSqlDialogData() {
  var headers = [
      { field: 'MusteriKodu', title: 'Musteri Kodu' },
      { field: 'MusteriAdı', title: 'Musteri Adi' }
  ];
  PwForm.openDialog('dialog', 'kendoGrid', DialogData.Sql, 'SELECT MusteriKodu, MusteriAdı FROM MUSTERILER(NOLOCK)', headers, '');
}
```

[**\* Dialog Type : WebServis**]{style="color: rgb(41, 105, 176);"}

Bu tür dialog nesnesi webservisten gelen veri ile kullanılmak içindir.
Bu türde veri parametresine web servisten dönen veri JSON Array olarak
gönderilir.

Paremetreler sırasıyla dialogName, gridName, dialogType, data, headers,
plugin şeklindedir.

dialogName : Dialog nesnesinin adı

gridName : Dalog nesnesinin içinde kullanılacak olan tablonun adı

dialogType : Dialog nesnesinin türü

data : JSON Array türünde data

headers : Kullanılan tablo için kolon başlıkları

plugin : Boş

``` {.javascript code-id="section-1669041186981" data-language="javascript"}
function getWebServiceDialogData() {
  var headers = [
      { field: 'types', title: 'Tip Bilgisi' }
  ];
  var serviceName  = "MYSERVICEDATA";
  var functionName = "GetDataType";
  var inputs = [];
  var obj = {paramName:'type',paramValue:''};
  inputs.push(obj);
  PwForm.webService(serviceName, functionName, inputs).then(result => {
        PwForm.openDialog('dialog', 'kendoGrid', DialogData.WebService, result, headers,"");
  });
}
```

[**\* Dialog Type : Data**]{style="color: rgb(41, 105, 176);"}

Bu tür dialog nesnesi olan bir JSON array türünde veri ile kullanılmak
içindir. 

Paremetreler sırasıyla dialogName, gridName, dialogType, data, headers,
plugin şeklindedir.

dialogName : Dialog nesnesinin adı

gridName : Dialog nesnesinin içinde kullanılacak olan tablonun adı

dialogType : Dialog nesnesinin türü

data : JSON Array türünde data

headers : Kullanılan tablo için kolon başlıkları

plugin: Boş

``` {.javascript code-id="section-1669041394097" data-language="javascript"}
function getDataDialogData() {
  var headers = [
      { field: 'DateParts', title: 'Çalışma Süresi Aralık Tipleri' }
  ];
  var  arr=['months', 'weeks', 'yearDays', 'monthDays', 'weekDays', 'hours','minutes', 'seconds'];
  PwForm.openDialog('dialog', 'kendoGrid', DialogData.Data, arr, headers,"");
}
```

\

\
