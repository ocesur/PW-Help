## Tip Alanları

#### Formda bir tip alanının değerini nasıl kullanırım?

Aşağıda Tip üzerindeki MUSTERI_ALANI değeri bir değişkene atanmıştır.

``` {.javascript code-id="section-1679554426657" data-language="javascript"}
var musteriAdi = PwForm.get("MUSTERI_ADI");
```

#### Formda bir tip alanının değerini nasıl güncellerim?

Aşağıda MUSTERI_ADI tip alanı verilen değer ile güncellenmiştir.

``` {.javascript code-id="section-1679554426660" data-language="javascript"}
PwForm.set("MUSTERI_ADI","Paperwork");
```

#### Form üzerindeki bir veri tablosunun bir kolonunu nasıl gizlerim?

Elektronik form üzerinde bulunan bir veri tablosu nesnesinin bir
kolonunun gizlenmesi şu şekilde yapılabilir :

[**Yeni Kullanım :** PwForm.component(\"TABLO_TİP_ADI\").grid şeklinde
kullanılmalıdır.]{teams="true"}

[**(2025 ve sonrası güncellenmiştir. Daha eski kodlarınızı
güncellemelisiniz.)**]{teams="true"}

**Eski Kullanım Örneği:** \$(\"# + Tip Adı +  \_  + Tablo Tipi Alan
Adı).data(\"kendoGrid\").hideColumn(Gizlenecek Alan Adı);  

[Not : "kendoGrid" sabit değerdir.]{style="color: rgb(209, 72, 65);"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679555130739.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Yukarıdaki tabloda, bakiye kolonunu gizlemek için aşağıdaki fonksiyonu
formun global fonksiyonlar bölümüne yazmamız gerekir. 

``` {.javascript code-id="section-1679555212035" data-language="javascript"}
function hideColumn(){
  PwForm.component("TABLO_TİP_ADI").grid;
}
```

Burada, T_EGITIM_TIPI formun bağlı olduğu tipin adı, HESAPLAR tablonun
adı, BAKIYE ise tablonun içindeki gizlenecek kolonun adıdır.

Bu fonksiyon yazıldıktan sonra, fonksiyonun aşağıdaki görselde olduğu
gibi, tuş nesnesinin özel işlemler alanında çağırılması gerekir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679555496173.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Bakiye Kolonunu Gizle tuşuna basıldığında, veri tablomuz aşağıdaki
görselde olduğu gibi görünür.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679555609417.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Aynı kolonu tekrar göstermek isterdiğimizde aynı fonksiyonu aşağıdaki
gibi hideColumn yerine showColumn ile kullanıyoruz.

``` {.javascript code-id="section-1679556550036" data-language="javascript"}
function showColumn(){
PwForm.component("TABLO_TİP_ADI").grid.showColumn("BAKIYE");
}
```

Bu fonksiyon yazıldıktan sonra da, fonksiyonun aşağıdaki görselde olduğu
gibi, tuş nesnesinin özel işlemler alanında çağırılması gerekir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679556611734.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Sonuç aşağıdaki görseldeki gibi olacaktır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1679556648471.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Veri tablosunun eklenebilir, düzenlenebilir ve silinebilir özellikleri
varsa ve bu özellikler kullanılırsa tablomuzun kolonları yeniden görünür
olacaktır. Eklenebilir, düzenlenebilir ve silinebilir olmayan koşullarda
bu şekilde kolonlarımızı gizleyebiliriz.

**[Alternatif Örnek]{style="color: rgb(41, 105, 176);"}**

Tabloda kolonu gizlemenin bir diğer yolu ise şu şekildedir :

``` {.javascript code-id="section-1679642386229" data-language="javascript"}
function hideColumn() {
    PwForm.component("HESAPLAR").component.components[0].gridShow = false;
    PwForm.component("HESAPLAR").redraw();
}
```

::::: {.section .warningBox}
::: title
Dikkat !!!
:::

::: content
Bu şekilde kullandığımızda veri tablomuzun eklenebilir, düzenlenebilir
ve silinebilir özelliklerini kullansak bile tablomuzun kolonları görünür
olmayacaktır.
:::
:::::
