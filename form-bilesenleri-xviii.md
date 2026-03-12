#### Form Arkasında Kural Motoru Tablolarının Verilerine Erişim

Aşağıda, bir kural motorunda tanımlı bir tablonun kolonlarında bulunan
değerlere erişim örneği bulunmaktadır. Kural Motorunda tanımlı örnek
tablomuzun adı tablePaperWork olarak verilmiştir.

\

[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686769791189.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Kural Motorunda tanımlanan
tablo]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil
.fr-dib .fr-bordered .fr-shadow style="width: 953px;"} Bu tablonun Price
kolonu için örnek fonksiyon yazalım.

``` {.javascript code-id="section-1686770061791" data-language="javascript"}
function checkPriceRE(){
    let minPrice = ruleEngine.tablePaperWork._items[0].entries[0].value.Price;
    let maxPrice = ruleEngine.tablePaperWork._items[1].entries[0].value.Price;

    if(PwForm.get('FIYAT') < minPrice || PwForm.get('FIYAT') > maxPrice){
        PwForm.Error('Uyarı', 'Uygun aralıkta fiyat giriniz.')
        PwForm.DeleteRowAt('URUN_LISTESI', -1);
    };
}
```

\

minPrice değişkeni bu şekilde bir tanımlamada kural motorundaki
tablePaperWork tablosunun 0. indeksteki satırının Price değerini
almıştır, aynı şekilde maxPrice değişkeni de tablePaperWork tablosunun
2. indeksteki satırının Price değerini almıştır. Değerleri çekerken
kullandığımız kod yapısı
ruleEngine.(TabloAdı).\_items\[i\].entries\[0\].value bize bir
JavaScript objesi döner ve biz objenin ulaşmak istediğimiz değerlerine
yine obje.Değer şeklinde ulaşmış oluruz. İndex verirken sadece
\_items\[i\] içerisine vermemiz yeterli, 'entries\[0\].value' kısmı
sabit kalmalıdır yani indeks farketmeksizin burası böyle kalmalıdır.

#### Formlarda Eklenti Kontrolü

Süreçte yer alan manuel adım aktivitesinde kullanılan formda, aşağıda
yer alan kod ile formda eklentilere akış kullanıcıya geldiğinden
itibaren, herhangi bir belgenin eklenip eklenmediği kontrolü
yapılmaktadır.

Fonksiyon çalışırken duruma göre bilgilendirme kutucuğu çıkarak
kullanıcıyı belgenin eklenip eklenmediğine göre bilgilendirmektedir.

Not: Bu kod dağıtım işleminden sonra olan bir manuel adımda doğru
çalışmayacaktır. Bunun sebebi eklenen eklentilerin, eklendiği aktiviteye
dair herhangi bir bilgi tutumamasındandır. Eklenti direkt olarak akışa
eklenmektedir.

``` {.javascript code-id="section-1686791234052" data-language="javascript"}
//Amacı: Akışın eklentisinde belge olup olmadığının kontrolü
function belgeEklendiMi() {
    //Fonksiyonda kullanılan PwForm.Query metodu aSync olarak çalışmaktadır. Bu sebeple cevap alınana kadar kullanıcının işlem yapmasını engelliyoruz.
    PwForm.Progress(true);  //Fonksiyon çalışırken kullanıcı tarafından işlem yapılmasını engeller.
    var belgeKontrolQuery = `SELECT OBJECT_ID FROM PW_VIRTUAL_DOCS (NOLOCK) WHERE CONTENT_TYPE = 'D' AND OBJECT_ID = (SELECT ATTACHMENT_ID FROM PW_WORKFLOW (NOLOCK) WHERE WORKFLOW_ID = '${PwForm.WorkflowId}') `;
    belgeKontrolQuery += ` AND CHILD_ID IN (SELECT OBJECT_ID FROM  VW_PW_SYSOBJECT (NOLOCK) WHERE CREATED_DATE > (SELECT LAST_ACTION_DATE FROM VW_PW_WORKFLOW (NOLOCK)  WHERE WORKFLOW_ID = '${PwForm.WorkflowId}') )`;
    //Belge kontrolü için kullanılacak Query oluşturuldu.
    PwForm.Query(belgeKontrolQuery, "").then(result => {
        PwForm.Progress(false); //Boş ya da dolu bir yanıt geldiği için tekrar kullanıcıya işlem yapabilmesi için deaktif ediyoruz.
        console.log("Belge Sayısı:" + result.length); //Bu şekilde eklenen belge sayısına da ulaşabilirsiniz.
        if (result.length > 0) {
            // 0 dan fazla yanıt gelmesi belge eklendiği anlamına gelmektedir.
            PwForm.Info("Bilgi", "Dokümanlar Eklenmiştir. İşlemlerinize Devam Edebilirsiniz."); //Bilgilendirme
        }
        else {
            // Boş gelmesi belge eklenmediği anlamına gelmektedir.
            PwForm.Info("Bilgi", "İşlemlerinize Devam Edebilmek İçin Önce Ek Eklemeniz Gerekmektedir."); //Bilgilendirme
        }
    });
}
```

#### Paperwork PWForm Nesne Eventleri nelerdir ve diğer eventler nasıl kullanılabilir?

PWForm nesnesinde sadece **Change** ve **Focus **eventi** setEvent **ile
kullanılabilir. İlgili örnek [Form Bileşenleri
II](/tr/docs/nasil-yaparim-form-bilesenleri2){rel="nofollow"
translate="no"} sayfasında \"Formun kodlama kısmında getRowValue
kullanımı nasıl yapılır? \" başlığında bulunur.

Eğer bunun haricinde örneğin keypress/keyup eventleri kullanılmak
isteniyor ise ekrandaki nesnenin eventine bağlanmak gerekir.

``` {.javascript code-id="section-1686818688921" data-language="javascript"}
$("input[name='data[AD_SOYAD]']").on( "keypress", function() {
    console.log( "keypress val : " + PwForm.get("AD_SOYAD") );
} );

$("input[name='data[AD_SOYAD]']").on( "keyup", function() {
    console.log( "keyup val : " + PwForm.get("AD_SOYAD") );
} );
```

\

#### Form Tasarımı Taslak Alanında HTML Image Nesnesi Kullanımı

Form nesnelerinin veri tabloları içerisinde iken kullanabildiği taslak
özelliği, html nesnelerinin kullanılmasına olanak sağlamaktadır.

Örnek olarak kullanılabilecek bir HTML Image nesnesi tanımı:

``` {.markup code-id="section-1686791664017" data-language="markup"}
<img src=’fotoğraf-linki’ width=’150px’ height=’150px’ >
```

Aynı zamanda base64 formatında bir resim verisi kullanılarak da resim
görüntülenebilir.

Örnek base64 verisi ile image nesnesi kullanımı:

``` {.markup code-id="section-1686791793800" data-language="markup"}
<img src='data:image/png;base64, BASE64 VERİSİ'>
```

HTML Kodunun ekleneceği bölüm şu şekildedir : 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686791855931.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

#### Paperwork Form Nesnesi Taslak Bölümü

Form arayüzündeki taslak bölmesinin işlevi eğer nesne alanı bir veri
tablosu içerisinde ise KendoGrid objesinin sahip olduğu taslak
özelliğini kullanabilmemizi sağlamaktadır.

KendoGrid taslak özelliği sayesinde eklenmiş olan satır verileri farklı
biçimlerde gösterilebilir, üzerlerinde matematiksel işlem yapılabilir
veya taslak bölümü içerisinde javascript fonksiyonları direkt olarak
çağırılabilir.

Önemli noktalardan biri taslak özelliğinin sadece bir görüntüleme aracı
olduğudur.

Örn: VERI_ALANI_1'in değeri 2 ve VERI_ALANI_2'nin değeri de 2 olsun .Bu
değerlerin  toplamını taslak özelliği ile VERI_ALANI_3 üzerinde
gösterirsek 4 rakamını görebiliriz fakat. Veri tablosunun verilerini
kontrol ettiğimizde 4 rakamının verilerin içerisinde bulunmadığını
gözlemleriz.

KendoGrid'in verilere erişmek için kullandığı operatörler şu şekildedir:

\# TABLO_ALAN_ADI \#

#= JavaScript fonksiyonlarının döndüğü değerleri basabilir. \#

Örnek olarak bir veri tablosu oluşturalım ve içerisine 2 adet yazı alanı
ekleyelim.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686792679971.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Daha sonra format kontrolü nesnesinin taslak alanına aşağıdaki kodu
yerleştirelim :

``` {.markup code-id="section-1686792782842" data-language="markup"}
#if(TCKIMLIKNO.length < 11 || TCKIMLIKNO.length  > 11){#<b style='background-color:\\\#333; color:\\\#F5E1B3;'> TC Kimlik Numarası 11 Haneli olmalı Girilen: #=returnCharCount(TCKIMLIKNO)#</b># }else{#<b style='background-color:green; color:white'> Tc No formata uygundur</b># }#
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686792807494.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Taslak alanının kapasitesini gösterebilmek açısından son olarak kodlama
bölümünün Global Fonksiyonlar alanına da aşağıda yer alan kodu yazalım.

``` {.javascript code-id="section-1686792972922" data-language="javascript"}
function returnCharCount(TCKIMLIKNO){
    return TCKIMLIKNO.length;
}
```

Kodun çalışma şekli:

Eğer TCKIMLIKNO isimli alana girilen değer 11 haneden küçük veya büyük
ise Format Kontrolü alanına uyarı mesajı gelir ve uyarı mesajından sonra
Global Fonksiyonlar alanına yazdığımız fonksiyon çağrılır ve bu
fonksiyonda bize kaç haneli bir TC Kimlik Numarası girdiğimizin
bilgisini döner, bu bilgi de uyarı mesajının sonuna eklenir.

Eğer TCKIMLIKNO isimli alan 11 haneli ise, Tc No formata uygundur
şeklinde bilgilendirme Format Kontrolü alanına yazılır, 

Sonuç Görüntü: 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686793053598.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Dikkat edilmesi gerekenler:

Taslak içerisinde javascript kullandığımız için başlangıçta ve sonda \#
olmak zorundadır

Eğer taslak içerisinde \# sembolünü veri çekmek dışarısında bir amaç
için kullanacaksak bunu şu şekilde yazmalıyız:  \\\\\\#

Örnek: \<b style=\'background-color:\\\\\\#333; color:\\\\\\#F5E1B3;

Burda yer alan \# sembolü css renk koduna ait olduğundan dolayı
\\\\\\kaçış operatörünü kullanmalıyız.

#### Elektronik Formdaki Veri Tablosunu Kopyalama

Bir elektronik form üzerinde yer alan veri tablosunun tamamı veya sadece
seçili satırı clipboard üzerine alınarak kopyalanabilir. Bunun için
kullanmamız gereken fonksiyonlar ve kullanım şekilleri şu şekildedir :

[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686894250881.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Örnek Elektronik
Form]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil .fr-dib
.fr-bordered .fr-shadow style="width: 952px;"}

:::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686894283161.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Tüm tabloyu kopyalama butonu
özel işlem bölümü]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 546px;"}

::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1686894342442.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Seçili satırı kopyala butonu
özel işlem bölümü]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 551px;"}

 Kodlama bölümünde bulunan global fonksiyonlar içerisine yazılacak
kodlar şu şekildedir :

``` {.javascript code-id="section-1686894414626" data-language="javascript"}
function copyGrid() {
    //Başlıkları ile birlikte tüm veri tablosunu kopyalar
    copyGridToClipboard("TEST_VERI_GRUBU", true);
}

function copySelectedRow() {
    //Başlıkları ile birlikte seçili olan tablo verisini kopyalar
    copyGridToClipboard("TEST_VERI_GRUBU", true, true);
}

//@gridName: Form içerisindeki veri tablosu alan adı
//@isHeadersIncluded: Form içerisindeki veri tablosuna ait başlıkların kopyalanacak veriye dahil edilip edilmeyeceğini belirtir
//@isHeadersIncluded: Başlıklar tabloya dahil edilmek isteniyor ise true verilmelidir.  (hiçbir değer verilmez ise varsayılan olarak false kabul edilir).
//@returnOnlySelected: Sadece veri tablosunda seçilmiş olan değerleri kopyalaması için true verilmelidir (hiçbir değer verilmez ise varsayılan olarak false kabul edilir).
//Alınan parametrelere istinaden alan adı verilmiş veri tablosunu HTML formatında oluşturur ve döndürür
function copyGridToClipboard(gridName, isHeadersIncluded = false, returnOnlySelected = false) {
    let data = PwForm.get(gridName);
    //Sadece seçili satır kopyalanmak isteniyor ise veri dizisi düzenlenir.
    if (returnOnlySelected) {
        data = [];
        data.push(PwForm.component(gridName).SelectedRow);
    }
    let result = "";
    //Kopyalama işlemi yapabilmek için verilerin tutulacağı geçici HTML tablo nesnesi oluşturur
    let table = document.createElement("table");
    let headerContent;
    //Veri tablosu başlıkları dahil edilmek isteniyor ise 
    if (isHeadersIncluded) {
        //Başlıklar için dizi oluşturulur
        let headers = [];
        //Veri tablosu içerisindeki tüm başlıklar alınır
        Object.keys(data[0]).forEach(value => {
            //Veri tablosu başlıklarının formda görüntülenen değerleri alınır.
            headers.push($('.formio-component-' + gridName + ' [data-field="' + value + '"]').html());
        })
        headerContent = "<tr>"
        //Verilen tüm tablo başlıklarını yazdırır
        headerContent += headers.map(header => {
            return ("<td>" + header + "</td>")
        }).join('');
        headerContent += "</tr>";
        //Verilen tablo başlıklarını sonuç tablosuna ekler
        result += headerContent
    }
    //Verilen tablo verilerini yazdırır
    let tableContent = data.map(value => {
        let responseText = "<tr>";
        Object.keys(value).forEach(prop => {
            responseText += "<td>" + value[prop] + "</td>";
        })
        responseText += "</tr>";
        return responseText
    }).join('');
    //Verilen tablo içeriklerini sonuç tablosuna ekler
    result += tableContent;
    table.innerHTML = result;

    //Oluşturulan tablo sayfaya eklenir
    let body = document.getElementsByTagName("body")[0];
    body.appendChild(table);

    //Yeni oluşturulan tablo seçilir
    window.getSelection().removeAllRanges();
    let range = document.createRange();
    range.selectNode(table);
    window.getSelection().addRange(range);
    //Seçilen tablo kopyalanır
    document.execCommand('copy');
    //Kopyalama işlemi için geçici süreliğine oluşturulan HTML tablo sayfa üzerinden kaldırılır (Form üzerindeki veri tablosunu kaldırmaz).
    table.remove();
}
```
:::
::::

::: fr-img-space-wrap
 Kopyalanan veriler, başlıklar ile birlikte Word veya Excel gibi
programlara yapıştırılabilir.

 

\
:::

 

\

\
