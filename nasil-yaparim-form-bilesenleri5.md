**[Formda bir açılır pencere nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736020" data-language="javascript"}
var dialogName = "pwdialog";
PwForm.openDialog(dialogName, '', DialogData.None);
```

**[Formda bir açılır pencere için veri nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736022" data-language="javascript"}
var gridName = "pwkendogrid";
var dialogName = "pwdialog";
PwForm.openDialog(dialogName, gridName , DialogData.Data, PwForm.form.data.HESAPLAR);
```

**[Formda bir açılır pencerede PaperWork nesnesi nasıl
görüntülenir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736023" data-language="javascript"}
var objectId = PwForm.get('txObjectId');
var dialogName = "pwdialog";
PwForm.openDocument(dialogName, "objectViewer", objectId, true);
```

**[Formda bir açılır pencerede başka bir form nasıl
görüntülenir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736024" data-language="javascript"}
var dialogName = "pwdialog";
var formName = "SEKMELER"; 
PwForm.formDialog(dialogName, formName, 
        function(e) // Form yükleme sonrası olayı
        {
            e.data.MUSTERI_NO = 'Paperwork 34';
        },
        function(e) // Form kaydetme sonrası olayı
        {
            PwForm.set("txResult", e.data.MUSTERI_ADI);
        }
);
```

**[Formda günün tarihi nasıl alınır?]{style="font-size: 18px;"}**

Örnek: PwForm.moment() nesnesi bir dizi tarih işlemlerini yapabildiğiniz
bir kütüphanedir. <https://momentjs.com> adresinden detaylı bilgi
alabilirsiniz

``` {.javascript code-id="section-1658482736025" data-language="javascript"}
PwForm.moment().toDate();
```

**[Formda tarih formatı nasıl değiştirilir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736025" data-language="javascript"}
PwForm.form.moment.locale('tr');
```

**[Formda tarih formatı nasıl verilir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736026" data-language="javascript"}
PwForm.moment().format('DD-MM-YYYY');
```

Not: Tarih,TarihSaat ve Saat nesnelerinin dönüş değeri string\'tir.

**[Formda tarih alanı nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736027" data-language="javascript"}
PwForm.moment(PwForm.get('pwdate')).add(2, 'days').toDate()
```

**[Tip üzerindeki Tarih alanını nasıl
alırım?]{style="font-size: 18px;"}**

**[]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660025129382" data-language="javascript"}
DateTime? islemtarihi = FormData.Get("ISLEM_TARIHI") as DateTime?;
```

**[]{style="font-size: 18px;"}**

**[Formda onay penceresi nasıl kullanılır? ]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482736028" data-language="javascript"}
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

**Formda tabloya kod ile kayıt ekleme, güncelleme ve silme işlemlerini
nasıl yaparım?**

Kod örnekleri aşağıdaki gibidir. Formun kodlama sayfasındaki Global
Fonksiyonlar kısmına yazılır.

Elektronik Form üzerinde bulunan tuşların tıklama olayında fonksiyonlar
çağrılır.

``` {.javascript code-id="section-1678218827170" data-language="javascript"}
function satirEkle() {
    try {
        if (PwForm.equals(PwForm.get('ADI_SOYADI'), '')
            && PwForm.equals(PwForm.get('DOGUM_TARIHI'), '')
            && PwForm.equals(PwForm.get('DOGUM_YERI'), '')
            && PwForm.equals(PwForm.get('OGRENIM_DURUMU'), '')) {
            PwForm.Info(PwForm.Culture('Alan Hatası'), PwForm.Culture('Lütfen öncelikle tablo alanlardan bir tanesini doldurunuz!'));
        }
        else
            PwForm.AddRowData('KATILIMCILAR', {
                K_ADI_SOYADI: PwForm.get('ADI_SOYADI'),
                K_DOGUM_TARIHI: PwForm.get('DOGUM_TARIHI'),
                K_DOGUM_YERI: PwForm.get('DOGUM_YERI'),
                K_OGRENIM_DURUMU: PwForm.get('OGRENIM_DURUMU'),
            });
        PwForm.set('ADI_SOYADI', '');
        PwForm.set('DOGUM_TARIHI', '');
        PwForm.set('DOGUM_YERI', '');
        PwForm.set('OGRENIM_DURUMU', '');

    } catch (wzerror) {
        PwForm.Error(PwForm.Culture("Hata"), wzerror);
    }
}

function satirGuncelle() {
    try {
        var gridName = 'KATILIMCILAR';
        var row = PwForm.component(gridName).SelectedRow;
        if (row) {
            if (PwForm.equals(PwForm.get('ADI_SOYADI'), '')
                && PwForm.equals(PwForm.get('DOGUM_TARIHI'), '')
                && PwForm.equals(PwForm.get('DOGUM_YERI'), '')
                && PwForm.equals(PwForm.get('OGRENIM_DURUMU'), '')) {
                PwForm.Info(PwForm.Culture('Alan Hatası'), PwForm.Culture('Lütfen öncelikle güncellenecek alanlardan bir tanesini doldurunuz!'));
            }
            if (!PwForm.equals(PwForm.get('ADI_SOYADI'), '')) {
                row.K_ADI_SOYADI = PwForm.get('ADI_SOYADI');
            }
            if (!PwForm.equals(PwForm.get('DOGUM_TARIHI'), '')) {
                row.K_DOGUM_TARIHI = PwForm.get('DOGUM_TARIHI');
            }
            if (!PwForm.equals(PwForm.get('DOGUM_YERI'), '')) {
                row.K_DOGUM_YERI = PwForm.get('DOGUM_YERI');
            }
            if (!PwForm.equals(PwForm.get('OGRENIM_DURUMU'), '')) {
                row.K_OGRENIM_DURUMU = PwForm.get('OGRENIM_DURUMU');
            }

            PwForm.component(gridName).updateGrid();
            PwForm.set('ADI_SOYADI', '');
            PwForm.set('DOGUM_TARIHI', '');
            PwForm.set('DOGUM_YERI', '');
            PwForm.set('OGRENIM_DURUMU', '');
        }

        else
            PwForm.Info(PwForm.Culture('Seçim Hatası'), PwForm.Culture('Lütfen öncelikle satır seçiniz!'));
    } catch (wzerror) {
        PwForm.Error(PwForm.Culture("Hata"), wzerror);
    }
}

function seciliSatirSil() {
    try {
        var gridName = 'KATILIMCILAR';
        var row = PwForm.component(gridName).SelectedRow;
        if (row) {
        PwForm.DeleteRow('KATILIMCILAR');
        }
        else
        PwForm.Info(PwForm.Culture('Seçim Hatası'), PwForm.Culture('Lütfen öncelikle satır seçiniz!'));

    } catch (wzerror) {
        PwForm.Error(PwForm.Culture("Hata"), wzerror);
    }
}

function tumTabloSil() {
    try {
        PwForm.DeleteAll('KATILIMCILAR');

    } catch (wzerror) {
        PwForm.Error(PwForm.Culture("Hata"), wzerror);
    }
}
```

::::: {.section .warningBox}
:::: title
::: content
**[]{style="box-sizing: border-box; font-size: 18px;"}**Form kodlama
ekranında açılır pencere kodlamalarınızı, form sihirbazı kodlamalarının
sonunda yer alan \"Endregion\" satırından sonra kullanmanız gerekir.
:::
::::
:::::

**Anket Formu Nasıl Oluştururum?**

Aşağıdaki örnekte bir tablo nesnesi yardımı ile anket formu
oluşturulmuştur. Anket formunun soruları dinamik olarak alınabilir.
Tasarım ekranında veri olmadığı için sorular da dinamik oluşturulmuştur.

1.Formun üzerine Veri Tablosu bileşeni yerleştirilmiş ve ismi
pwkendogrid8 olarak atanmıştır.

2.Veri Tablosu üzerine bir yazı nesnesi yerleştirilmiş ve adı QUESTION
olarak belirlenmiştir.

3.Veri Tablosuna Seçim Düğmesi nesnesi yerleştirilmiş ve 5 seçenek
oluşturulmuş, her seçeneğin değeri belirlenmiştir. Taslak bölümünde
aşağıdaki kodlama yapılmış ve her seçenek değişik renkle boyanmıştır.

``` {.javascript code-id="section-1658482736028" data-language="javascript"}
      <div style='position:relative;font-size:10px;float:right'>  
      <input type='radio' class='rClass' value='CI' name='group#: QUESTION#' data-bind='checked: ANSWER'><span class='green'>Çok iyi</span>  
      <input type='radio' class='rClass' value='I' name='group#: QUESTION#' data-bind='checked: ANSWER'><span class='purple'>Iyi</span>          
      <input type='radio' class='rClass' value='N' name='group#: QUESTION#' data-bind='checked: ANSWER'><span class='blue'>Normal</span>            
      <input type='radio' class='rClass' value='K' name='group#: QUESTION#' data-bind='checked: ANSWER'><span class='orange'>Kötü</span>            
      <input type='radio' class='rClass' value='CK' name='group#: QUESTION#' data-bind='checked: ANSWER'><span class='red'>Çok Kötü</span>          
      </div>
```

4.Global fonksiyonlarda veri oluşturulmuş, ön değerler atanmış ve veri
tablosuna bağlanmıştır.

``` {.javascript code-id="section-1658482736030" data-language="javascript"}
var questions = [
    { QUESTION: 'Verilen örnekler yeterli mi?', ANSWER:'CI' },
    { QUESTION: 'Eğitmenin bilgi seviyesi Nasıl?',  ANSWER:'I' },
    { QUESTION: 'Eğitim süresi yeterli mi',  ANSWER:'I' },
    { QUESTION: 'Genel olarak Eğitimi nasıl değerlendirirsiniz?',  ANSWER:'CK' },
];
 
 function survey() {
    PwForm.fillGrid('pwkendogrid8', questions, null);
}
```

5.Tüm bu yapılan ayarlar ile beraber ara yüzde formun çalışması
aşağıdaki videoda gösterilmiştir.

#### Veri Tablosu içerisinde bulunan alanlara OnChange fonksiyonu atama

 [[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1671023632338.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Şekil
1.1]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil .fr-dib
.fr-bordered .fr-shadow style="width: 1117px;"} 

\"COFFEES\" isimli veri tabanı örneği üzerinde
PwForm.component(\"COFFEES\").component.components  kodu bize her bir
satırda ki nesneleri getiriyor.

\

::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1671023687948.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Şekil
1.2]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil .fr-dib
.fr-bordered .fr-shadow style="width: 983px;"}

 

Şekil 1.1 de görüldüğü üzere tabloda kolon nesnesi kullanılmış. Eğer
tablomuzda kolon bulunuyor ise kodumuz değişiklik gösteriyor. Şekil 1.2
de ise tabloda her bir satır nesnesi görülmektedir. İlk değer kolon
değeri gösteriyor. 1 ve 2 değerleri ise kolon içerisinde olmadığı için
direkt olarak tip alanına bağlı.

Eğer kolon bulunmuyor ise kodumuz;

PwForm.component(\"COFFEES\").component.components\[1\].onCustomChange =
aksiyon1;

Bu kod \"COFFEE_PRICE\" nesnesi her değiştiğinde \"aksiyon1\"
fonksiyonunu çalıştıracaktır. Bu kod yükleme sonrasına yazılması
gerekiyor.

Eğer tip kolon içerisinde ise;

PwForm.component(\"COFFEES\").component.components\[0\].columns\[0\]

Kodu ile hangi kolon da olduğunu seçiyoruz. Örneğimizde 1 adet kolon
içerisinde ilk tarafta \"COFFEE_NAME\", ikinci tarafta ise
\"COFFEE_COUNT\" nesneleri bulunuyor.

Burada \"columns\[0\]\" diyerek kolon nesnesinin sütun sırasına göre o
sütunda bulunan nesnelere ulaşıyoruz. Burada ki örnekte kolonda bir tane
nesne olduğu için kodumuz şu şekilde ;

PwForm.component(\"COFFEES\").component.components\[0\].columns\[0\].components\[0\].onCustomChange
= aksiyon1;

Eğer ikinci sütunda olan nesne için event eklemek istersek;

PwForm.component(\"COFFEES\").component.components\[0\].columns\[1\].components\[0\].onCustomChange
= aksiyon1;  şeklinde düzenlemeliyiz.

Eğer kolon içerisindeki sütunlarda birden fazla nesne olur ise yine
sırasına göre 

PwForm.component(\"COFFEES\").component.components\[0\].columns\[1\].components\[sırasıSayısı\];
şeklinde değiştirmeliyiz.
:::

#### Bir veri tablosu satırının sürecin bir sonraki adımında bir listeye set edilmesi

Başlangıç formunda bulunan tablomuzdaki verileri alabilmemiz için aynı şekilde tablo ve tablo içerisindeki alanları bitiş formunda da tasarıma eklememiz gerekiyor. Listeye veri ekleme işlemi başarılı
/
başarısız olsada tabloyu fonksiyonun sonunda gizleyerek kullanıcının görmemesini sağlıyoruz.

``` {.javascript code-id="section-1676034861070" data-language="javascript"}
/* 
Fill List yapılacak olan array'i global değişkenlerde tanımlıyoruz.  
Bu array'in fonksiyon dışarısında ve global değişkenlerde tanımlı olması gerekiyor. 
*/ 

var adayBilgi = []; 

function adayTabloVerileri() { 
    /* 2. Forma gelen tabloda veri varsa işlem yapıyoruz. */
    if (PwForm.rowCount('GORUSME_LISTESI_TABLOSU') > 0) { 
        /* Tablo verilerinin hepsini bir değişkene atıyoruz. */
        var rows = PwForm.getRows('GORUSME_LISTESI_TABLOSU'); 

        /* Tablo değişkenlerini bir array'e keylerini belirtelerek ekliyoruz. */
        for (row of rows) { 
            /*
            Sadece Key1 alanını yani Aday Adı Soyadının görünür olmasını istersek 18. satırda ki gibi kod yazılması gerekmektedir. 
            adayBilgi.push({ Key1: row.ADAY_ADI_SOYADI, Key2: row.ADAY_MESLEGI }); 
            Tüm bilgileri tek satırda göstermek istersek satır 21 deki gibi kod yazılması gerekmektedir. 
            */
            adayBilgi.push({ Key1 : "Adı Soyadı: " + row.ADAY_ADI_SOYADI + " Mesleği : " + row.ADAY_MESLEGI }); 
        } 

        /*
        For bloğu içerisinde veri ile doldurduğumuz adayBilgi array'ini "GORUSME_LISTESI"
        içerisinde göstermek için fill list fonksiyonunu kullanıyoruz. 
        */ 

        PwForm.fillList('GORUSME_LISTESI', 'Key1', 'Key1', 'adayBilgi'); 
    } 

    /* Tablo en başta görünür olmalıdır. Tüm işlemler bittikten sonra görünmez olarak isteğe bağlı olarak set edilebilir. */

    PwForm.show("GORUSME_LISTESI_TABLOSU",false); 
} 
```
