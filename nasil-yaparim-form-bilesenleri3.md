**[Elektronik Formda veri tablosuna bir liste nasıl
eklenir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497644" data-language="javascript"}
var gridName = 'pwkendogrid';
PwForm.AddRowDataFull(gridName, [
{name:'naim',label:'Naim',age:25,birthdate:PwForm.moment().toDate()},
{name:'suleyman',label:'Süleyman',age:25,birthdate:PwForm.moment().toDate()}
]);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda veri tablonda kritere göre satır nasıl
silinir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497645" data-language="javascript"}
var gridName = 'pwkendogrid';
PwForm.deleteRows(gridName, "Key", 'Mehmet', FilterTYPES.Equal);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda veri tablodan başka bir tabloya veri kopyalanır
mı?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497646" data-language="javascript"}
var targetGrid = 'pwkendogrid1';
var destinationGrid = 'pwkendogrid2';
for (var row of PwForm.getSelectedRows(targetGrid)) {
    var newRow = PwForm.NewRow('destinationGrid');
    newRow = PwForm.copy(row, newRow, [{ ad: 'Nim', soyad: 'Slmn' }, { ad: 'Naim', soyad: 'Süleymanoğlu' }]);
    PwForm.AddRowData(destinationGrid, newRow);
}
```

**[**[]{style="box-sizing: border-box; font-size: 18px;"}** FormData
içinde yer almayan veri tablosunda satır içi düzenleme nasıl
yapılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497647" data-language="javascript"}
fManager.FormObject.data.pwkendogrid5 = usrlist.slice(); // Datanın kopyası oluşturulur.
var ds = new kendo.data.DataSource({
    transport: {
        read: function (options) { options.success(fManager.FormObject.data.pwkendogrid5); },
        update: function (options) {
            var data = options.data;
            fManager.FormObject.data.pwkendogrid5[PwForm.component('pwkendogrid5').selectedIndex - 1] = data;
            options.success([data]);
            $('#pwkendogrid5').data('kendoGrid').select('.k-grid-edit-row');
            PwForm.form.triggerRedraw();
        }
    },
    data: fManager.FormObject.data.pwkendogrid5,
    schema: {
        model: {
            id: "name",
            fields: {
                name: { type: "string", editable: true, validation: { required: true } },
                label: { type: "string", editable: true, validation: { required: false } },
                age: { type: "number", editable: true, validation: { required: false } },
                birthdate: { type: "date", editable: true, validation: { required: false } }
            }
        }
    }
});
var grd = $("#pwkendogrid5").data("kendoGrid");
grd.setDataSource(ds);
PwForm.component('pwkendogrid5').redraw();
```

**[Elektronik Formda veri tablosunda ekleme işlemi sırasında nasıl işlem
yapılır?]{style="font-size: 18px;"}\**
Bakiye toplamı girmiş olduğunuz bakiyelerin toplamıdır.\
Çeşitli yollar ile hesaplanabilir.\
Öncelikle Bakiye toplamı nesnesinin data tabındaki **Yenilendiğinde**
alanı Veri kaynağı seçilmelidir (Hesaplar)

``` {.javascript code-id="section-1660553497652" data-language="javascript"}
// Hesaplanmış Değer bölümüne;
value = _.sumBy(data.HESAPLAR, function (row) {return row.BAKIYE;}); 

// veya
value = PwForm.Sum('HESAPLAR','BAKIYE'); 

// Eğer sadece belli satırlar alınacaksa;
value = PwForm.Sum('HESAPLAR','BAKIYE','ORAN',FilterTYPES.Equal,1)
```

Eğer tabloya veri girişi için form üzerine eklenen yeni bir tuş
üzerinden işlem yapıldığı durumda global değerlere aşağıdaki örnek kod
uygulanabilir. Formun tıklama olayında da bu fonksiyon çağrılır.

``` {.javascript code-id="section-1666606818839" data-language="javascript"}
function genelToplam(){
   try{
         PwForm.set('GENEL_TOPLAM', PwForm.Sum('HESAPLAR','BAKIYE'));



   }catch(wzerror){
      PwForm.Error(PwForm.Culture("Hata"), wzerror);
   }
}
```

Formun Yükleme sonrasında ise tuşun tıklama olayında yukarıdaki
genelToplam fonksiyonu çağrılır.

``` {.javascript code-id="section-1666606941144" data-language="javascript"}
PwForm.setEvent('Satır Ekle','Click',function(){
       genelToplam();
    });
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda veri tablosunda arama nasıl
yapılır?]{style="font-size: 18px;"}**\
Tablo özellikleri kısmında
**[Aranabilir]{style="color: rgb(40, 50, 78);"} **seçimi yapılır.

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda veri tablosunda bir sütun için template nasıl
kullanlır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497654" data-language="javascript"}
// Kolon renklendirme.
{ 
    field: 'FIYAT', 
    title: 'Fiyat' ,
    format: '{0:n2}',
    template:"< span style='color:red'>#: FIYAT# < /span>"
}

// Hesaplanan alan örneği. FIYAT * MIKTAR = TUTAR elde edilir.
{ 
    field: 'TUTAR',
    title: 'Tutar',
    format: '{0:n2}',
    template:'#:FIYAT * MIKTAR #' 
}
var gridName = "pwkendogrid4";
var headers = [
    { field: 'MALZEME_ADI', title: 'Malzeme' },
    { field: 'MIKTAR', title: 'Miktar', format: '{0:n0}' },
    { field: 'FIYAT', title: 'Fiyat', format: '{0:n2}', template: '<span style="color:red">#: FIYAT# </sapn>' },
    { field: 'TUTAR', title: 'Tutar', format: '{0:n2}', template: '#:FIYAT * MIKTAR #' },
];

var rows = [
    { MALZEME_ADI: "Kalem", MIKTAR: 5, FIYAT: 2, TUTAR: 1 },
    { MALZEME_ADI: "Silgi", MIKTAR: 2, FIYAT: 1.5, TUTAR: 1 },
    { MALZEME_ADI: "Defter", MIKTAR: 4, FIYAT: 4.5, TUTAR: 1 },
];
PwForm.fillGrid(gridName, rows, headers);
```

#### Elektronik Formda Tablo üzerinde bulunan satırları renklendirme

Öncelikle renklendirme yapacağımız tablonun oluşturulması gerekmektedir.
Aşağıdaki gibi basit bir tablo ve renklendirme işlemi için bir buton
bulunan basit bir form üzerinde çalışacağız. Kod üzerinde birbirinden
farklı fiyat aralıkları için tanımlanmış renkler mevcuttur. Tabloya
ekleyeceğimiz satırların fiyat değerlerine göre satırlardaki renkler
değişecektir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1682504593127.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Örnek olarak yukarıda hazırlanan form üzerindeki tabloya farklı
değerlerde veriler girilmiştir. Renklendirme işlemini
gerçekleştireceğimiz kodlara aşağıda görebilirsiniz.

``` {.javascript code-id="section-1682504651355" data-language="javascript"}
//En yuksek fiyata sahip satirin renklendirilme ornegi

function TableColorChange() {
    var data = PwForm.component('KAYIT_TABLOSU').grid.dataSource.data();                                                 
    $.each(data, function (i, row) {
        if (row.FIYAT_KOLON <= '25000')
            $('tr[data-uid="' + row.uid + '"]').css("background-color", '#a2b9bc');
        else if ('25000' < row.FIYAT_KOLON && row.FIYAT_KOLON <= '50000')
            $('tr[data-uid="' + row.uid + '"]').css("background-color", "#b2ad7f");
        else if ('50000' < row.FIYAT_KOLON && row.FIYAT_KOLON <= '75000')
            $('tr[data-uid="' + row.uid + '"]').css("background-color", "#878f99");
        else if ('75000' < row.FIYAT_KOLON)
            $('tr[data-uid="' + row.uid + '"]').css("background-color", "#6b5b95");
    });
}
```

Bu fonksiyon içerisinde Javascript/AJAX kütüphanesini kullanarak
renklendirmek istediğimiz tablonun verilerine erişerek "grid" değişkeni
tanımlıyoruz. 

**[\$(\"# + Tip Adı +  \_  + Tablo Tipi Alan
Adı).data(\"kendoGrid\")]{style="color: rgb(41, 105, 176);"}** -\> kod
üzerinde AJAX ile veriyi şablona kendi tablomuzun değerlerini girerek
kullanabilir.

Devamında ise "grid" nesnesinin datasını çekerek data değişkeni üzerinde
tutuyoruz. Kod bloğunun devamında ise hangi şartlar altında satırların
ne renk olacağı ile ilgili tanımlamalarımızı yaparak satır renklendirme
işlemimizi tamamlayabiliriz. 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1682504771107.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Form dizayn alanımızda ise forma eklediğimiz butonun ayarlarını erişip
"Özel İşlem" alanına kodlama kısmına yazdığımız fonksiyonun
tanımlamasını yaparak "Renklendirme" butonumuz üzerinden işlemimizi
gerçekleştirebiliriz.

Aşağıdan tablonun renklendirilmiş halini görebilirsiniz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1682504808624.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

**[Elektronik Formda veri tablonda tüm satırlar nasıl
silinir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497658" data-language="javascript"}
var gridName = 'pwkendogrid';
PwForm.DeleteAll(gridName);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda logo entegrasyonu ile liste nasıl
bağlanır?]{style="font-size: 18px;"}\**

``` {.javascript code-id="section-1660553497660" data-language="javascript"}
// Yükleme Sonrası
var listName = "pwkendogrid";
var logoConnectorName = "pwlogoint";
var _pwlogoint = PwForm.component(logoConnectorName);

_pwlogoint.setParam('wsKey', '1');
_pwlogoint.setParam('LKul', 'logo');
_pwlogoint.setParam('LSif', 'logo');
_pwlogoint.callFunction(function () {
    PwForm.fillIntList(listName,'NR','ADI',logoConnectorName, 'Firmalar');
});
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda bir açılır pencere nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497661" data-language="javascript"}
var dialogName = "pwdialog";
PwForm.openDialog(dialogName, '', DialogData.None);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda bir açılır pencere için veri nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497662" data-language="javascript"}
var gridName = "pwkendogrid";
var dialogName = "pwdialog";
PwForm.openDialog(dialogName, gridName , DialogData.Data, PwForm.form.data.HESAPLAR);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda bir açılır pencerede PaperWork nesnesi nasıl
görüntülenir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497663" data-language="javascript"}
var objectId = PwForm.get('txObjectId');
var dialogName = "pwdialog";
PwForm.openDocument(dialogName, "objectViewer", objectId, true);
```

**[**[]{style="box-sizing: border-box; font-size: 18px;"}**[]{style="box-sizing: border-box; font-size: 18px;"}]{style="font-size: 18px;"}**[[]{style="box-sizing: border-box; font-size: 18px;"}[**Elektronik **]{style="box-sizing: border-box; font-size: 18px;"}** Formda
bir açılır pencerede başka bir form nasıl
görüntülenir?**]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497665" data-language="javascript"}
var dialogName = "pwdialog";
var formName = "SEKMELER"; 
PwForm.formDialog(dialogName, formName, 
        function(e){ // Form yükleme sonrası olayı
            e.data.MUSTERI_NO = 'Paperwork 34';
        },
        function(e){ // Form kaydetme sonrası olayı
            PwForm.set("txResult", e.data.MUSTERI_ADI);
        }
);
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda tarih işlemleri nasıl yapılır?]{style="font-size: 18px;"}\**
PwForm.moment() nesnesi bir dizi tarih işlemlerini yapabildiğiniz bir
kütüphanedir. [Moment JS](https://momentjs.com) adresinden detaylı bilgi
alabilirsiniz.

``` {.javascript code-id="section-1660553497667" data-language="javascript"}
PwForm.moment().toDate(); // Günün tarihini alır.
PwForm.form.moment.locale('tr'); // Tarih formatını değiştirir.
PwForm.moment().format('DD-MM-YYYY'); // Özel tarih formatı verilir.
```

:::: {.section .warningBox}
::: title
Dikkat !
:::

Tarih, TarihSaat ve Saat nesnelerinin dönüş değeri **string**\'tir
::::

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda tarih alanı nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553497669" data-language="javascript"}
PwForm.moment(PwForm.get('pwdate')).add(2, 'days').toDate()
```

[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}
Formda onay penceresi nasıl kullanılır?**]{style="font-size: 18px;"}

``` {.javascript code-id="section-1660553497670" data-language="javascript"}
PwForm.ShowConfirmPopup("Başlık", "Mesaj", 
    function(e) // Evet sonrası 
    {
        // ..Kod
    },
    function(e) // Hayır sonrası
    {
       // ..Kod
    }
);
```
