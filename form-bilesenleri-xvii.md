#### Form Alanını Tablo Kolonuna Atama

Tablo nesnesine satır ekleme yaparken ana form üzerindeki alanı pop-up
içerisine set etmek istersek veya kaydetme sırasında istenilen alana set
etmek istersek şu şekilde yapabiliriz;

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680504544300.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Ad soyad alanına veritabanından kullanıcılar geliyor ve salt okunur olan
E mail alanına o kullanıcının mail adresi atanıyor.

Şimdi bir kullanıcı seçip Atama Listesi tablosunda ekle tuşuna
tıklandığında Atanan Kişi ve Atanan Kişi E Mail alanlarına formun
üzerindeki Ad Soyad ve E Mail alanlarının değerlerinin gelmesini
istiyorum.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680504608512.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680504620612.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

``` {.javascript code-id="section-1680504652055" data-language="javascript"}
function atamaTable() {
    if (!PwForm.IsNullOrEmpty('AD_SOYAD')) {
        PwForm.AddRow('ATAMA_LISTESI');
        PwForm.set('ATANAN_KISI', PwForm.component('AD_SOYAD').SelectedRow.Key1);
        PwForm.set('ATANAN_E_MAIL', PwForm.get('E_MAIL'));
    }
}
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680504691085.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Atama Listesi tablosunun Tablo Özellikleri kısmında Ekleme Tıklandığında
bölümünde çağırdığımdan ekle tuşuna basıldığında alanlarımız atanmıştır.
Tablo Özelliklerinde 'Ekleme Tıklandığında' ve \'Düzeltme Tıklandığında'
aksiyonlarında yeni bir satır üzerinde işlem yapacağımızdan
PwForm.AddRow() fonksiyonunu kullanıyoruz. Kaydetme esnasında yapmak
istediğimizde de aynı fonksiyonu Kaydet Tıklandığında bölümünde
çağırdığımızda çalışacaktır. İsteğe göre kaydetme işlemi öncesi
kullanıcının atanacak alanlara veri girişini önlemek için alanlar salt
okunur yapılıp kaydetme esnasında atanabilir.

#### Tabloda İstenilen Kolona Göre Sıralama

Formda bir tabloda istenilen sütuna göre sıralama yapmak istersek şu
şekilde yaparız.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680505005756.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Örneğimizde 3 sütunlu bir araç tablosu bulunuyor. Tablonun ilk başta
veri tabanından gelen sırası bu şekildedir. Global fonksiyonlarda
yazdığımız fonksiyonu tuşların özel işlemlerinde istediğimiz sütuna göre
çağırıyoruz.

[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680505042508.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Plakaya Göre
Sırala]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil
.fr-dib .fr-bordered .fr-shadow
style="width: 953px;"}[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680505194298.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Modele Göre
Sırala]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil
.fr-dib .fr-bordered .fr-shadow style="width: 953px;"} 

::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680505365923.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Markaya Göre
Sırala]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil
.fr-dib .fr-bordered .fr-shadow style="width: 953px;"}

 Sıralama fonksiyonu \[0-9\], \[A-Z\] olarak çalışır. Aritmetik
sıralamayı alfabetik sıralamadan önce yapar eğer rakam yoksa alfabetik
olarak sıralar.

Global fonksiyon şu şekildedir; 

``` {.javascript code-id="section-1680505706326" data-language="javascript"}
function gridSort(grid, direction, columnName){
    var kendoGrid = $('#' + 'T_ARAC_ATAMA_' + grid).data('kendoGrid');
    var dsSort = [];
    dsSort.push({field: columnName, dir: direction});
    kendoGrid.dataSource.sort(dsSort);
}
```

Plakaya Göre Sırala tuşu için =\> gridSort(\'ARAC_LISTESI\', \'asc\',
\'PLAKA\');

Modele Göre Sırala tuşu için =\>  gridSort(\'ARAC_LISTESI\', \'asc\',
\'MODEL\');

Markaya Göre Sırala tuşu için =\>  gridSort(\'ARAC_LISTESI\', \'asc\',
'MARKA');

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680505988556.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}
:::

 

\

``` {.javascript code-id="section-1680506005154" data-language="javascript"}
function AddSortDesc(grid, direction, columnName) { // Tablodaki kayıtları eklendiği tarihsaate göre sondan ilke göre sıralama kodu
    var kendoGrid = $('#' + 'T_GECICI_KABUL_SURECI_DK' + "_" + grid).data("kendoGrid"); // var kendoGrid = $('#' + 'TIP_ADI' + "_" + 'GRID_ADI').data("kendoGrid");
    var dsSort = [];
    dsSort.push({ field: columnName, dir: direction });
    kendoGrid.dataSource.sort(dsSort);
}
```

::::: {.section .infoBox}
::: title
Sıralama
:::

::: content
gridSort fonksiyonuna verdiğmiz 'asc' parametresini 'desc' olarak
verirsek sıralama tersine dönecektik. \[9-0\]\[Z-A\]
:::
:::::

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

#### Kural Motoru NextWorkingDayWOHolidays fonksiyonu elektronik formlarda nasıl kullanılır?

İlk önce takvim tanımlaması yapıyoruz. Çalışma günlerimizi ve tatil
günlerimizi ekliyoruz.

::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680677319964.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}[Örnek Takvim
Tanımlaması]{.fr-inner}]{.fr-img-wrap}]{.fr-img-caption .fr-fic .fr-fil
.fr-dib .fr-bordered .fr-shadow style="width: 982px;"}

 

Elektronik formumuzda bulunan Global Kod alanımızda fonksiyonumuzu
hazırlıyoruz.

Kural motoruna ait herhangi bir fonksiyonu kullanabilmemiz için ilgili
fonksiyonu "ruleEngine" 'den çağırabiliyoruz. NextWorkingDayWOHolidays
fonksiyonu bizden 3 adet parametre beklemektedir, bunlar

1.  Takvim adı (string tipinde olmalıdır)
2.  Tarih bilgisi
3.  Tarihin üzerine kaç iş günü ekleneceği bilgisi

Fonksiyonumuzu yazıyoruz :

``` {.javascript code-id="section-1680677410527" data-language="javascript"}
function IsGunuHesaplama(){
    var yeniTarih = ruleEngine.NextWorkingDayWOHolidays("Genel", PwForm.moment().toDate(), 3);
    PwForm.set("IS_GUNU",yeniTarih);
}
```
:::

Daha sonra fonksiyonumuzu yükleme sonrasında çalışacak şekilde
çağırıyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680677446824.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Fonksiyonumuzun bugüne 3 iş günü ekleyip tarih verdiğini atadığımız
alanda görebiliyoruz.

04.4.2023 tarihine 3 iş günü ekledi ve elde edilen tarih herhangi bir
tatil zamanına denk gelmediği için 07.4.2023 tarih bilgisini verdi. Eğer
4 gün eklemesini isteseydik cumartesi ve pazar tatil olduğu için bu
günleri atlayıp 10.4.2023 tarihini verecekti.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680677509033.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
