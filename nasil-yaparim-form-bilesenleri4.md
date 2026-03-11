**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formun kodlama kısmında getRow & getRows kullanımı nasıl
yapılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482755718" data-language="javascript"}
var row = PwForm.getRow("REFERANS_ARASTIRMASI", 0);
var rows = PwForm.getRows("REFERANS_ARASTIRMASI"); 
var rows = PwForm.getRows('AVANS_TALEP','SEHIR','TEST2',FilterTYPES.Equal);
var rows = PwForm.getRows('AVANS_TALEP','SEHIR','TEST2',FilterTYPES.Contains);
```

**![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613745160550.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}**

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda getRowValue kullanımı nasıl yapılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482755720" data-language="javascript"}
var gRV=PwForm.getRowValue("REFERANS_ARASTIRMASI","REFERANS_ADAY_ADI_SOYADI", 0); 
 
// İndex alanı sayı olarak girilerek. 
 
var gRV2=PwForm.getRowValue("REFERANS_ARASTIRMASI", "REFERANS_ADAY_ADI_SOYADI", PwForm.countRow("REFERANS_ARASTIRMASI") - 1);  
 
//Başka bir grid'in satır sayısı'nın sondan bir önceki index bilgisine göre. 
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda bir tip alanı için sayaç nasıl
tanımlanır?]{style="font-size: 18px;"}**

Aşağıdaki örnek yükleme sonrasında çalışması için tasarlanmıştır. Bazı
durumlarda herhangi bir aksiyonda kodun çalışması gerekebilir. Bu
durumda kod ilgili aksiyonda yazılabilir. Bu yapı için form sihirbazı
incelenmelidir.

``` {.javascript code-id="section-1658482755721" data-language="javascript"}
//------------ Yükleme Sonrası-------------------------------------
var indexName = "GELEN_EVRAK";
var counterName = indexName + "_" + PwForm.moment().format('YYYY'); 
PwForm.Counter(counterName, indexName, "Gelen Evrak - {{data}}");
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda sayaç nasıl tanımlanır?]{style="font-size: 18px;"}**

Aşağıdaki örnekte \"GELEN_EVRAK2022\" (2022 yılı için) bir sayaç
oluşturulmuştur. Sayaç ilk oluşturulduğunda 0 değerini hazırlar ve ilk
alındığında 1 değerini verir. Eğer o isimde sistemde bir sayaç var ise
numara sıfırlanmaz, kaldığı yerden devam eder.

PadStart komutu yardımı ile yazı tipinde [GELEN_EVRAK2022-00001 gibi bir
numara
oluşturulur.]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"} 

``` {.javascript code-id="section-1658482755722" data-language="javascript"}
var indexName = "GELEN_EVRAK";
var counterName = indexName + PwForm.moment().format('YYYY');
PwForm.counter_sync(counterName).then(result =>{
    PwForm.set(indexName, "Gelen Evrak - " + result.Result.padStart(5,'0'));
});
```

**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda veri tablosuna bir liste nasıl
eklenir?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1658482755723" data-language="javascript"}
var gridName = 'pwkendogrid';
PwForm.AddRowDataFull(gridName, [
{ name:'naim',label:'Naim',age:25,birthdate:PwForm.moment().toDate()},
{ name:'suleyman',label:'Süleyman',age:25,birthdate:PwForm.moment().toDate()}
]);
```

**[Formda veri tablosu seçilen satır
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133439" data-language="javascript"}
var gridName = 'pwkendogrid';
var row = PwForm.component(gridName).SelectedRow;
    if (row)
        alert(row.name);
    else
        PwForm.SetAlert('warning', 'Satır Seçiniz!');
```

**[]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}[**Formda
veri tablosuna satır nasıl
eklenir?**]{style="font-size: 18px;"}[]{style="font-size: 18px;"}**[]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133440" data-language="javascript"}
var gridName = 'pwkendogrid';
PwForm.AddRowData(gridName, { name: 'suleyman', label: 'Süleyman', age: 25, birthdate: PwForm.moment().toDate() });
```

**Formda tablolar arası satır kopyalama nasıl yapılır?**

Elektronik formlarda bulunan 2 tablo arasında seçilen satırlar aşağıdaki
örnek kod yardımı ile kopyalanabilir.

``` {.javascript code-id="section-1660553218191" data-language="javascript"}
function satirekle(){     
   try{
   var targetGrid = 'ANA_TABLO';
   var destinationGrid = 'ALT_TABLO';
   for (var row of PwForm.getSelectedRows(targetGrid)) 
   {  
      PwForm.AddRowData(destinationGrid,{ ALT_SAHIP:row.SAHIBI, ALT_SAHIP_OLUNAN:row.SAHIP_OLUNAN});
   }     
   }catch(wzerror){      
   PwForm.Error(PwForm.Culture("Hata"), wzerror);   }
}
```

Aşağıdaki videoda ise hem kodun nereye nasıl yazılacağı hem de çalışma
şekli gösterilmiştir.

**Elektronik Formlarda HTML nesnesinde lokalizasyon nasıl yapılır?**

İlk önce HTML nesnasinin başlık adı lokalizasyona girecek şekilde
planlanır. Örneğin başlığımız \_HTMLNesne\_ olsun. Lokalizasyon
bölümünde bunun için uygun içerik tanımlanır;

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1659949616833.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

Daha sonra HTML nesnesinin değer bölümüne HTML kodu örneğin aşağıdaki
gibi yazılır;

``` {.markup code-id="section-1659950118388" data-language="markup"}
<center><h2 id='custom_form_header'>{{PwForm.Culture("_HTMLNesne_")}}</h2></center>
<div style="border:1px solid powderblue"></div>
```
