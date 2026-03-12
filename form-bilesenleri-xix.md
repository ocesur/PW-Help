#### Form Nesnesine CSS Sınıf Ataması {#form-nesnesine-css-sınıf-ataması style="text-align: justify;"}

``` {.javascript code-id="section-1687504867648" data-language="javascript"}
PwForm.component("YONETICI_KARAR").element.classList += " greenBackground"
```

Elektronik formlarda PwForm kütüphanesinde bulunan "component"
fonksiyonunu çağırdıktan sonra "element" ve "classList" bilgilerini
çağırıyoruz. Çağırdığımız "classList" fonksiyonundan gelen bilgi, diziye
(array) ekleme çıkarma işlemi şeklinde de CSS sınıfları güncellenebilir.

``` {.javascript code-id="section-1687504999532" data-language="javascript"}
// 8. CSS Class’ını kaldırıyoruz.
PwForm.component("YONETICI_KARAR").element.classList.remove[8];

// Diziyi manipüle etme yolu kullanılırsa sonrasında nesnenin yenilenmesi gerekmektedir. 
PwForm.component("YONETICI_KARAR").redraw();
```

"classList" içerisinde nesneye ait tüm HTML sınıflarının bilgisi
getirilmektedir. 

"classList" dizisine ekleme çıkarma gibi işlemler yapabiliyoruz. Bu
sayede değişim gibi tetikleme olaylarında dilediğimiz gibi CSS sınıf
değişikliği yapabiliyoruz. 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687505169672.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Yükleme sonrasında yukarıda belirttiğimiz "classList" verisini çağırıp
kullanabileceğimiz kod parçacığımızı hazırlıyoruz. Bu noktada
dilediğiniz gibi olaylar(event) içerisinde kod hazırlayabilir ve
koşullarınıza göre CSS sınıf atama işlemini gerçekleştirebilirsiniz.

 ![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687505222170.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Elektronik form önizlemesinde ilgili alanımıza yükleme sonrasında CSS
sınıf atamasını gerçekleştirdiğimizi ve kırmızı olduğunu görüyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687505251516.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

#### Başlangıç Formunda İstenen Klasöre Belge Ekleme

Akış başlatırken istenen klasöre belge eklenip eklenmediğini kontrol
etmek için şu şekilde bir kod yapısına ihtiyaç vardır : 

``` {.javascript code-id="section-1688717446093" data-language="javascript"}
var cnt = 0;
$.each($("#attc-tree-container .k-item"), function (i, chlds) {
    var itm = $(chlds);
    if (itm.find('.fa-folder').parent().length > 0) {
        if (itm.find('.fa folder').parent()[0].innerText.includes('Genel') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
    }
});
if (cnt === 0) {
    PwForm.Error("Uyarı!", "Genel isimli klasöre belge eklemek zorunludur!");
    return false;
}
else
    return true;
```

Akışı başlatıp sonraki adıma geçmeden hemen önce kontrolü
sağlayacağımızdan kodu kaydetme öncesi kısmına yazıyoruz. Örneğimizde
'Genel' isimli klasörü kontrol ediyoruz ve hiç belge eklenmemiş ise
\"Uyarı!\", \"Genel isimli klasöre belge eklemek zorunludur" uyarı
mesajını çıkarıyoruz. 

Kendi çalışmalarınızda şu kod yapısındaki \"Genel\" değerini kontol
etmek istediğiniz klasör adıyla değiştirmeniz yeterli.

``` {.javascript code-id="section-1688717555957" data-language="javascript"}
itm.find('.fa folder').parent()[0].innerText.includes('Genel') 
```

NOT: Uyarı mesajında klasör adınızı da değiştirmeyi unutmayınız.

Örneğimizde hiç belge eklenmemişse hata mesajı çıkardığımızdan söz
etmiştik. Eğer en az iki belge eklenmesi gibi kontrol sağlanacak ise şu
kod bloğunda bulunan cnt değişkenini uyarlamak yeterli olacaktır :

``` {.javascript code-id="section-1688717653752" data-language="javascript"}
if (cnt === 0) {
    PwForm.Error("Uyarı!", "Genel isimli klasöre belge eklemek zorunludur!");
    return false;
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1688717663473.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

#### Elektronik Form üzerinde veri tablolarında kolon bazlı renklendirme

Elektronik formlardaki veri tablolarında kolon bazlı renklendirme yapmak
için, kodlama bölümünde geliştirmemizi şu şekilde yapabiliriz : 

``` {.javascript code-id="section-1688717943398" data-language="javascript"}
function ColorMe() {
    setTimeout(function () { // Yapılan işlemi belirtilen saniye kadar bekletilmesini sağlar.
        var grid = $("#T_EGITIM_TIPI_HESAPLAR").data("kendoGrid"); // Belirtilen tablonun alınması sağlanır.
        var data = grid.dataSource.data(); // Tablo verilerinin alınması sağlanır.
        $.each(data, function (i, row) { // Tablodaki verileri döner.
            if (!PwForm.IsNullOrEmpty(row.HESAP_NUMARASI)) { // Eğer hesap numarası alanı boş değilse
                var cols = $('tr[data-uid="' + row.uid + '"] td'); // İlgili kolon alınır.
                cols[1].className = "color-selected"; // Yeni bir sınıf adı verilir.
                $('tr[data-uid="' + row.uid + '"] .color-selected').css("background-color", "green"); // Verilen yeni sınıf adına ilgili renk atanır.
            }
        })
    }, 1);
}
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1688717969578.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Kodlama bölümünde tanımladığımız "ColorMe" fonksiyonunu "Renklendir"
başlıklı butonun özel işlem kısmında belirtelim ve çalışmasını
sağlayalım.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1688717997016.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Ekranda görünen "Renklendir" başlıklı butona tıkladığımızda sonuç
aşağıdaki gibi olacaktır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1688718017957.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

#### Akışı sadece belgeyi akışa gönder seçeneği seçilerek başlatmaya olanak sağlamak

Akışların \"İşlerim\" ekranından başlatılmasını engeller, sadece
belgeler\'de bulunan \"Belgeyi akışa gönder\" seçeneği işe akış
başlatmaya olanak sağlar.

Bunun için elektronik formun \"Kaydetme Öncesi\" bölümüne aşağıdaki kod
eklenmelidir.

``` {.javascript code-id="section-1695986523166" data-language="javascript"}
if(!FormManager.FlowInfo.AttachmentId)
{
   MSG_ERROR = "Akış sadece belgeyi akışa gönder seçeneği ile başlatılabilir";
   return false;
}
```

#### Liste Nesnesinde Şablon Kullanımı ve Ön Ek Ekleme

Şu şekilde bir listemiz olduğunu varsayalım :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1695986765781.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 579px;"}

Bu liste dinamik bir şekilde veya örnekteki gibi sabit şekilde
doldurulmuş olabilir. Listeye ait değerlerin form içerisinde görünen Key
değerlerini dinamik değiştirmek istersek eğer aşağıda yer alan kodu
kullanmak gerekecektir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1695986800390.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 717px;"}

Yukarıdaki kodda template değerine süslü parantezler içerisinde
eklediğimiz alanlar her zaman item. şeklinde başlamalıdır. Noktadan
sonra gelen kısım ise nesne verisinde yer alan hangi keyin
görüntüleneceğidir. Süslü parantezler dışarısında kalan alanlar ise
sabit yazı değeri olarak algılanacaktır. Daha sonrasında redraw()
fonksiyonu ile nesneyi yenilemek gerekmektedir.

Kod sonucunda oluşan liste görünümü:

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1695986838649.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 718px;"}

Liste nesnesinin prefix özelliğini kullanarak da listenin başına
istediğimiz bir ön ek ekleyebiliriz yazabiliriz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1695986866379.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 717px;"}

Bundan sonra görünüm şu şekilde olacaktır :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1695986893136.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 718px;"}

#### Tekil Alanlardan Tabloya Satır Ekleme

Form üzerinde bulunan alanları bir tabloya satır olarak eklemek için
aşağıdaki fonksiyonu taslak olarak kullanılabiliriz. Burada değerini
kullanacağımız alanları değişkenlere tanımlayıp ardından
PwForm.NewRow("TABLO_ADI") ile tabloda yeni bir satır oluşturuyoruz ve
row değişkenine bu satırın atamasını yapıyoruz. Oluşturduğumuz satırın
kolonlarına değer atamak için row.KOLON = "Atanacak Değer" ile kolonları
dolduruyoruz. 

Artık elimizde içi dolu bir satır var. Bu satırı
PwForm.AddRowData("TABLO_ADI",row) kullanımıyla daha önce doldurduğumuz
satırımızı tabloya aktarmış oluyoruz.

``` {.javascript code-id="section-1696851409643" data-language="javascript"}
function addTable() {
    var urun = PwForm.get("URUN_TEKIL");
    var marka = PwForm.get("MARKA_TEKIL");
    var adet = PwForm.get("ADET_TEKIL");
    var fiyat = PwForm.get("FIYAT_TEKIL");

    var row = PwForm.NewRow("URUN_TABLOSU");
    row.URUN_KOLON = urun;
    row.MARKA_KOLON = marka;
    row.ADET_KOLON = adet;
    row.FIYAT_KOLON = fiyat;
    PwForm.AddRowData("URUN_TABLOSU", row);
}
```

Bu fonksiyonu kullanacağımız (buton, tablo butonları, nesnelerin değişim
özellikleri vb.) nesnenin "Özel İşlem" alanına ekleyerek geliştirdiğimiz
fonksiyonun çalışmasını sağlayabiliriz. Aşağıda "Özel İşlem" kısmında
fonksiyonun kullanımını görebilirsiniz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696851445397.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Aşağıdaki görselde bu kullanımı örneklendirebildiğimiz basit bir form
tasarımını görüntüleyebilirsiniz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696851507798.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

#### Veri Tablosu Nesnesinin Ekleme, Düzeltme Butonlarına Tıklandığında Ek İşlem Yapma

Veri tablosu nesnelerinde ekle ve düzenle butonuna basıldığında popup
açılmaktadır ve bu popup açıldıktan sonra veri tablosuna ait olmayan
nesnelerin verilerini PwForm.get("NESNE_ADI") şeklinde alamamaktayız. Bu
yüzden ekle ve düzenle popuplarının açılma aksiyonlarını kontrol etme
ihtiyacı doğar.

Örnek senaryoda veri tablosundaki ekle butonuna bastığımızda formda
bulunan bir alandaki değerin veri tablosu ekleme popupında gözükmesini
istiyoruz, satırı düzenlerken ise düzenle popupı açıldığında satırda
hali hazırda bulunan değeri 1 arttırarak görüntülemek istiyoruz.

``` {.javascript code-id="section-1696852342574" data-language="javascript"}
function addRow(){
    //Veri tablosu dışarısında bulunan örnek bir nesnenin değerini popup açılmadan önce alıp bir değişkende tutuyoruz
    let data = PwForm.get("VERI_TABLOSU_DISINDAKI_PARA_ALANI");
    // Veri tablosunun ekle butonuna basıldığında açılması gereken popup ı açar
    PwForm.AddRow("VERI_TABLOSU_ALAN_ADI");
    // Ver tablosu içerisinde bulunan nesneye değişkende tuttuğumuz veriyi atarız
    PwForm.set("VERI_TABLOSU_ICINDEKI_PARA_ALANI", data);
}
```

``` {.javascript code-id="section-1696852366460" data-language="javascript"}
function editRow()
{
    //Düzenle butonuna basıldığında seçili olan satırdaki değeri alır
    let rowdata = PwForm.component("VERI_TABLOSU_ALAN_ADI").SelectedRow;
    //Düzenle butonu popup ekranını açar
    PwForm.EditRow("VERI_TABLOSU_ALAN_ADI");
    //Veri tablosu içindeki nesneye nesnenin kendi değerini 1 arttırarak ekler
    PwForm.set("VERI_TABLOSU_ICINDEKI_PARA_ALANI", ++rowdata.VERI_TABLOSU_ICINDEKI_PARA_ALANI);
}
```

Dizayn sekmesi neşenin Tablo Özellikleri penceresine eklememiz gereken
fonksiyonlar: 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696852390164.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 242px;"}

Para alanına değer girdikten sonra ekleye bastığımızda girdiğimiz değer
popup içerisinde gözükmektedir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696852414846.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696852422781.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Satırı seçip düzenleye bastığımızda ise, 15 değeri popup içerisine 16
olarak gelmektedir

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696852441878.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1696852449445.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
