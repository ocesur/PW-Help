**[Formda kural motoru nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133418" data-language="javascript"}
var endPoint = ruleEngine.ServiceEndPoint;
```

**[Formda kural motoru fonksiyonu nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133420" data-language="javascript"}
var calendarName = "Genel";
var date = new Date(PwForm.get('pwdatetime3'));
var nextDate = ruleEngine.NextWorkingDay("Genel", date, 1);
```

**[Formda sistem metodu nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133421" data-language="javascript"}
var methodName = "Metod Adı";
var prms =[{ paramName: 'prm1', paramValue: 'value1' },
{ paramName:'prm2', paramValue: 'value2' }]; PwForm.ExecuteMethod(methodName, prms).then(result => {
console.log(result);
});
```

**[Formda sistemde tanımlı WebServis çağrısı nasıl
yapılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133422" data-language="javascript"}
var serviceName  = "Servis Adı";
var functionName = "Fonsiyon Adı";
var inputs = { key: 'prm1', value: 'value1' };
PwForm.webService(serviceName, functionName, inputs).then(result => {
        console.log(result);
    });
```

**[Formun kodlama kısmında getRow kullanımı nasıl
yapılır? ]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133423" data-language="javascript"}
var row = PwForm.getRow("REFERANS_ARASTIRMASI", 0); 
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627373952785.png){.fr-fic
.fr-dii .fr-draggable border="0" width="482"
v:shapes="Picture_x0020_1579953827"}

**[Formun kodlama kısmında getRows kullanımı nasıl
yapılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133425" data-language="javascript"}
var rows = PwForm.getRows("REFERANS_ARASTIRMASI"); 
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627373952824.png){.fr-fic
.fr-dii .fr-draggable border="0" width="606"
v:shapes="Picture_x0020_969915901"}

**[ Formun kodlama kısmında getRowValue kullanımı nasıl
yapılır? ]{style="font-size: 18px;"}**

 ![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627373952858.png){.fr-fic
.fr-dii .fr-draggable border="0" width="606"
v:shapes="Picture_x0020_1661958615"}

``` {.javascript code-id="section-1660553133425" data-language="javascript"}
var gRV=PwForm.getRowValue("REFERANS_ARASTIRMASI","REFERANS_ADAY_ADI_SOYADI", 0); 
 
// İndex alanı sayı olarak girilerek. 
 
var gRV2=PwForm.getRowValue("REFERANS_ARASTIRMASI", "REFERANS_ADAY_ADI_SOYADI", PwForm.countRow("REFERANS_ARASTIRMASI") - 1);  
 
//Başka bir grid'in satır sayısı'nın sondan bir önceki index bilgisine göre. 
```

**[Dinamik verileri kullanarak listeleme nasıl
yapılır?]{style="font-size: 18px;"}**\
**![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613741078031.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow .fr-draggable}**

``` {.javascript code-id="section-1660553133427" data-language="javascript"}
// Global Fonksiyonlar
var egitimList = [
    { Key: 'Sdk', Value: '1' },
    { Key: 'Rapor', Value: '2' },
    { Key: 'Analiz', Value: '3' },
    { Key: 'Diğer', Value: '0' }
];

var seansList = [
    { Id:'1', Key: 'Sdk-1', Value: '11' },
    { Id:'1', Key: 'Sdk-2', Value: '12' },
    { Id:'2', Key: 'Veri kaynakları', Value: '21' },
    { Id:'3', Key: 'Seans1', Value: '31' },
    { Id:'0', Key: 'Seans1', Value: '01' }
];
var myList=[];

function Init() // Yükleme sonrasında çağrılır.
{
    PwForm.setEvent('EGITIM_TURU','Change',function(){setDetail();});
}

function setDetail()
{
  var id=PwForm.get("EGITIM_TURU");
  myList = seansList.filter(key => key.Id == id);
  PwForm.fillList("EGITIM_SEANSI", "Value", "Key", "myList");
}
```

**[Formda bir listeye dinamik veriler nasıl
bağlanır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133429" data-language="javascript"}
// Global Fonksiyonlar
var userList = [
    { Name:"ali", label :"Ali"   },
    { Name:"mehmet", label :"Mehmet"},
    { Name:"yunus" , label :"Yunus" }];

// Yükleme Sonrası
var  listName = "pwselect";
var  key      = "Name";
var  label    = "label"; 
PwForm.fillList(listName, key, label, "userList");
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613741306570.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow .fr-draggable
style="width: 693px;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613741366542.png){.fr-fic
.fr-dii .fr-draggable style="width: 692px;"}

**[Formda html bileşeni nasıl kullanılır?]{style="font-size: 18px;"}**

Örnek 1;

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644933851889.png){.fr-fic
.fr-fil .fr-dib .fr-draggable style="width: 947px;"}

Örnek 2;\
![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644933878488.png){.fr-fic
.fr-fil .fr-dib .fr-draggable}

Örnek 3;

``` {.javascript code-id="section-1660553133430" data-language="javascript"}
// Formda html bileşeni kullanma - Örnek 3
$.ajax({
        url: contentUrl,
        async: true,
        success: function (Data) {
            try {
                PwForm.component('pwhtml5').setContent(Data, true);
            } catch (ee) {
                PwForm.set('pwhtml5', 'Invalid Content:' + ee);
            }           
        },
        error: function (err) {
            AjaxError(err);
        }
    });
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613741853561.png){.fr-fic
.fr-dii .fr-bordered .fr-draggable style="width: 848px;"}

**[Formda bir yazı alanı için normal ifade nasıl
kullanılır? ]{style="font-size: 18px;"}**\
Sadece sayı girilmesi
için: [\^\[0-9\]{7,10}\$]{style="background-color: rgb(209, 213, 216);"}**\**
![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1613741882678.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow .fr-draggable
style="width: 840px;"}

\

**[Formda lokalizasyon nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133431" data-language="javascript"}
var msgKey = "_INVALID_MSG_";  // Localization alanıda bu key için değerler oluşturulur                                               
var msg    = PwForm.Culture(msgKey);
```

**[Formda form bileşeni için değişimi olayı nasıl
tanımlanır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133432" data-language="javascript"}
var  listName = "pwselect";
PwForm.setEvent(listName, 'Change',function(){
    // Code    
    });
```

**[Formda bir tip alanı için sayaç nasıl
tanımlanır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133432" data-language="javascript"}
// Yükleme Sonrası
var indexName = "GELEN_EVRAK";
var counterName = indexName + "_" + PwForm.moment().format('YYYY'); 
PwForm.Counter(counterName, indexName, "Gelen Evrak - {{data}}");
```

**[Formda sayaç nasıl kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133433" data-language="javascript"}
var indexName = "GELEN_EVRAK";
var counterName = indexName + PwForm.moment().format('YYYY');
PwForm.counter_sync(counterName).then(result =>{
    PwForm.set(indexName, "Gelen Evrak - " + result.Result.padStart(5,'0'));
    });
```

**[Formda veri tablosu bir listeye nasıl
tanımlanır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133435" data-language="javascript"}
// Global Fonksiyonlar
var usrlist = [
    { name:'ahmet',label:'Ahmet',age:34,birthdate: PwForm.moment().toDate() },
    { name:'mehmet',label:'Mehmet',age:35,birthdate:PwForm.moment().add(20, 'days').toDate() },
    { name: 'ali'   , label: 'Ali'   , age: 36, birthdate: PwForm.moment().add(2, 'years').toDate() },
    { name: 'yunus' , label: 'Yunus' , age: 37, birthdate: PwForm.moment().subtract(6, 'days').toDate() },];

var headers = [
    { field: 'name' , title: 'Key' },
    { field: 'label', title: 'Name' },
    { field: 'age'  , title: 'Age' },
    { field: 'birthdate', title: 'Birth Date', format: '{0:dd/MM/yyyy}' },];

// Yükleme Sonrası
var gridName = 'pwkendogrid';
PwForm.fillGrid(gridName, usrlist, headers);
```

**[Formda SQL sorgusu sonucu veri tablosu ile nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript code-id="section-1660553133437" data-language="javascript"}
var hdr = [{ field: 'LOGIN_NAME', title: 'Giriş Kodu' }, { field: 'USER_NAME', title: 'Kullanıcı Adı' }];
PwForm.Query('SELECT TOP 100 LOGIN_NAME,USER_NAME FROM PW_USER(NOLOCK)', '')
.then(result => {
    var gridName = 'pwkendogrid';
    PwForm.fillGrid(gridName, result, hdr);
    });
```
