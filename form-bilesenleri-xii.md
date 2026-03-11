#### Tabloda İstenen Kolona Göre Sıralama

Elektronik form üzerinde bulunan bir veri tablosunun içinde bulunan
verileri, istenilen sütuna göre sıralama işlemi şu şekilde yapılır:

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684129658077.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Örneğimizde marka, model ve plaka olmak üzere üç sütunlu bir araç
tablosu bulunuyor. Tablonun ilk başta veri tabanından gelen sırası
şekilde görüldüğü gibidir. Global fonksiyonlarda yazdığımız fonksiyonu
tuşların özel işlemlerinde istediğimiz sütuna göre çağırıyoruz. Sıralama
fonksiyonu \[0-9\], \[A-Z\] olarak çalışır. Aritmetik sıralamayı
alfabetik sıralamadan önce yapar eğer rakam yoksa alfabetik olarak
sıralar.

Global fonksiyon şu şekildedir; 

``` {.javascript code-id="section-1684129849473" data-language="javascript"}
function gridSort(grid, direction, columnName){
    var kendoGrid = $('#' + 'T_ARAC_ATAMA_' + grid).data('kendoGrid');
    var dsSort = [];
    dsSort.push({field: columnName, dir: direction});
    kendoGrid.dataSource.sort(dsSort);
}
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684129863783.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

Plakaya Göre Sırala tuşu için; 

``` {.javascript code-id="section-1684130009207" data-language="javascript"}
gridSort('ARAC_LISTESI', 'asc', 'PLAKA');
```

Modele Göre Sırala tuşu için;

``` {.javascript code-id="section-1684130036833" data-language="javascript"}
gridSort('ARAC_LISTESI', 'asc', 'MODEL');
```

Markaya Göre Sırala tuşu için;

``` {.javascript code-id="section-1684130047965" data-language="javascript"}
gridSort('ARAC_LISTESI', 'asc', ‘MARKA’);
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684130697268.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Sıralama fonksiyonunu kendi ihtiyacınıza göre düzenlemek isterseniz
alttaki örneği isteğinize göre değiştirebilirsiniz.

``` {.javascript code-id="section-1684130756457" data-language="javascript"}
function AddSortDesc(grid, direction, columnName) { // Tablodaki kayıtları eklendiği tarihsaate göre sondan ilke göre sıralama kodu
    var kendoGrid = $('#' + 'T_GECICI_KABUL_SURECI_DK' + "_" + grid).data("kendoGrid"); // var kendoGrid = $('#' + 'TIP_ADI' + "_" + 'GRID_ADI').data("kendoGrid");
    var dsSort = [];
    dsSort.push({ field: columnName, dir: direction });
    kendoGrid.dataSource.sort(dsSort);
}
```

**Not :** gridSort fonksiyonuna verdiğimiz 'asc' parametresini 'desc'
olarak verirsek sıralama
[\[9-0\]\[Z-A\]]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}
şeklinde tersine dönecektir.

:::::: {.section .warningBox}
::: title
Uyarı
:::

:::: content
::: {style="text-align: justify;"}
Sıralama yapıldıktan sonra tabloya ekleme, silme ya da düzenleme
yapılırsa sıralama en baştaki haline dönecektir. Bu yüzden fonksiyonu
kullanacağınız yer önemlidir. Tabloda herhangi bir aksiyon sonrası
fonksiyonu çağırırsanız güncel satırlarla sıralama yapabilir.
:::
::::
::::::

#### Formdaki Alanı Tablo Kolonuna Atama

Elektronik form üzerinde bir veri tablosu nesnesine satır ekleme
yaparken, elektronik form üzerindeki alanı pop-up içerisine atama
istersek veya kaydetme sırasında istenilen alana atama istersek şu
şekilde yapabiliriz;

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684131746989.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Ad soyad alanına veritabanından kullanıcılar geliyor ve salt okunur olan
E mail alanına o kullanıcının mail adresi atanıyor. Şimdi bir kullanıcı
seçip Atama Listesi tablosunda ekle tuşuna tıklandığında Atanan Kişi ve
Atanan Kişi E-Mail alanlarına formun üzerindeki Ad Soyad ve E-Mail
alanlarının değerlerinin gelmesini sağlayalım.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684137315986.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684132580919.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 1071px;"}

``` {.javascript code-id="section-1684132610630" data-language="javascript"}
function atamaTable() {
    if (!PwForm.IsNullOrEmpty('AD_SOYAD')) {
        PwForm.AddRow('ATAMA_LISTESI');
        PwForm.set('ATANAN_KISI', PwForm.component('AD_SOYAD').SelectedRow.Key1);
        PwForm.set('ATANAN_E_MAIL', PwForm.get('E_MAIL'));
    }
}
```

Atama Listesi tablosunun Tablo Özellikleri kısmında \'Ekleme
Tıklandığında\' bölümünde çağırdığımdan ekle tuşuna basıldığında
alanlarımız atanmıştır. Tablo Özelliklerinde 'Ekleme Tıklandığında' ve
\'Düzeltme Tıklandığında' aksiyonlarında yeni bir satır üzerinde işlem
yapacağımızdan PwForm.AddRow() fonksiyonunu kullanıyoruz. Kaydetme
esnasında yapmak istediğimizde de aynı fonksiyonu Kaydet Tıklandığında
bölümünde çağırdığımızda çalışacaktır. İsteğe göre kaydetme işlemi
öncesi kullanıcının atanacak alanlara veri girişini önlemek için alanlar
salt okunur yapılıp kaydetme esnasında atanabilir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684132654471.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
