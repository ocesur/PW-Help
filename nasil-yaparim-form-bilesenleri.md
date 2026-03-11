---
title: "Nasıl Yaparım Form Bileşenleri"
---

**Elektronik Formda yazı alanına format(regular expression) nasıl
verilir?**

Örneğin sadece sayı girişine izin vermek için şu ifade kullanılır:Sadece sayı girilmesi için: ^[0-9]7,10\$

Bunun için yazı bileşeninin doğrulama bölümünde "Düzenli ifade kalıbı"bölümüne bu ifade yazılır;

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627388659795.png)

:::::::: titleRegEx:::

::: contentRegEx için daha fazla bilgiye şu adresten erişebilirsiniz:[RegEx](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)::::::::

**Elektronik Formda bir bileşenin değerini nasıl
kullanırım?**

Aşağıda txtMusteriAdi isimli yazı alanının değeri bir değişkeneatanmıştır.

```{.javascript data-language="javascript"}
var componentName =  "txtMusteriAdi";
var musteriAdi  =   PwForm.get(componentName);
```

**Elektronik Formda bir bileşenin değerini nasıl
güncellerim?**

Aşağıda txtMusteriAdi isimli bileşenin değerigüncellenmiştir.

```{.javascript data-language="javascript"}
var componentName =  "txtMusteriAdi";
PwForm.set(componentName, "Paperwork");
```

**Elektronik Formda bir bileşenin görünürlüğünü nasıl
değiştiririm?**

Aşağıda txtMusteriAdi isimli bileşenin görünürlüğükapatılmıştır.

```{.javascript data-language="javascript"}
var componentName =  "txtMusteriAdi";
PwForm.show(componentName, false);
```

**Elektronik Formda bir bileşenin aktifliğini nasıl
değiştiririm?**

Aşağıda txtMusteriAdi isimli bileşenin aktifliğikapatılmıştır.

```{.javascript data-language="javascript"}
var componentName =  "txtMusteriAdi";
PwForm.enable(componentName, false);
```

**Elektronik Formda bir bileşenin zorunluluğunu nasıl
değiştiririm?**

Aşağıda txtMusteriAdi isimli bileşenin zorunluluğukaldırılmıştır.

```{.javascript data-language="javascript"}
var componentName =  "txtMusteriAdi";
PwForm.required(componentName, false);
```

\*\*Elektronik Formda [html](/tr/docs/a5x140217000)\*\*[**[]**](/tr/docs/p50050401003-11)**bileşeni nasıl
kullanılır?**

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627387184028.png)

Yukarıdaki şekilde görüldüğü gibi HTML bileşeninin değer bölümüne HTMLkodu yazılarak görünüm oluşturulmuştur. Yazılan HTML kodu aşağıdakigibidir;

```{.markup data-language="markup"}
<div class="row">
     <ul class=" col-sm-12 col-md-12 col-lg-9 public">
         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 col-xs-6 font-blue-dark nowrap">Giriş Adı</div>
             <div class="p-col col-sm-7 col-md-7 col-xs-6 font-grey-mint nowrap">goksel</div>
         </li>
         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 col-xs-6 font-blue-dark nowrap">Son Giriş</div>
             <div class="p-col col-sm-7 col-md-7 col-xs-6 font-grey-mint nowrap">27 Ocak 2021 09:27</div>
         </li>
         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 col-xs-6 font-blue-dark nowrap">Elektronik Posta</div>
             <div class="p-col col-sm-7 col-md-7 col-xs-6 font-grey-mint nowrap">goksel@g-gsoft.com</div>
         </li>
         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 col-xs-6 font-blue-dark nowrap">Ünvanı</div>
             <div class="p-col col-sm-7 col-md-7 col-xs-6 font-grey-mint nowrap">Yazılım Direktörü</div>
         </li>
         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 col-xs-6 font-blue-dark nowrap">Varsayılan Dil</div>
             <div class="p-col col-sm-7 col-md-7 col-xs-6 font-grey-mint nowrap"> 
                 <span title="" class="k-widget k-dropdown" unselectable="on" role="listbox" aria-haspopup="true" aria-expanded="false" tabindex="0" aria-owns="lang_listbox" aria-live="polite" aria-disabled="false" style="vertical-align: middle;" aria-busy="false" aria-activedescendant="3860ea3f-5530-4fd6-9020-f46028d9a604"><span unselectable="on" class="k-dropdown-wrap k-state-default"><span unselectable="on" class="k-input">Türkçe</span><span unselectable="on" class="k-select" aria-label="select"><span class="k-icon k-i-arrow-60-down"></span></span></span><input css="langSel input-small" id="lang" name="lang" style="vertical-align: middle; display: none;" type="text" data-role="dropdownlist"></span> 

                 <a href="#" id="btnLangSel" class="btn red-sunglo btn-sm btn-lang-save hidden">Kaydet</a>
             </div>
         </li>

         <li class="row left">
             <div class="p-col col-sm-3 col-md-3 font-blue-dark nowrap"> </div>
             <div class="p-col col-sm-7 col-md-7 font-grey-mint nowrap">
                 <a href="#" id="btnRemDelete" class="btn red-sunglo btn-sm btn-rem-save hidden">Beni hatırla</a> 
             </div> 
         </li>  
     </ul> 
 </div>
```

**Elektronik Formda HTML nesnesini kullanarak bir logo nasıl
gösterebilirim?**

Aşağıda örnek kod ile HTML nesnesi üzerinde şirketinizin logosunugösterebilirsiniz.

```{.markup data-language="markup"}
<br>
   <image
   <img src="https://www.paperwork.com.tr/assets/img/logo.png"  type="image/jpg">
   </image> 
<br>
```

**Elektronik Formda HTML Bileşeni ile imaj nasıl
gösteririm.**

 Aşağıdaki örnekte, sunucu üzerinde bulunan bir imaj HTML nesnesiüzerinde gösterilmiştir;

```{.markup data-language="markup"}
<center>
<img src="/Content/archive/img/0.PNG"/>
</center>
```

### CrossDomain

Eğer imaj adresi site dışında ise, sitenin Crossdomain ayarlarında\
erişimin açılması gerekir. Normal şartlarda sitelerin başka siteler ya\
da adresler'den content alımı engellenir.

**Elektronik Formda HTML Bileşeninde tooltip nasıl
kullanılır**

Aşağıdaki örnek yardımı ile HTML TAG leri kullanılarak ekrana yazıyazılır. Bu yazının bir bölümü de tooltip yardımı ile gösterilir;

```{.markup data-language="markup"}
Bir HTML nesnasinde yazıya tooltip vermek için 
<div class="tooltip">buradaki gibi
<span class="tooltiptext">Kodlama-->CSS bölümüne bakınız</span>
</div>
işlem yapılır
```

 Bu tooltip belirlenirken CSS bölümünde de renk gibi değerlerbelirlenir;

```{.css data-language="css"}
.tooltip {
position: relative;
display: inline-block;
border-bottom: 1px dotted black;
}
.tooltip .tooltiptext {
visibility: hidden;
width: 120px;
background-color: black;
color: #fff;
text-align: center;
border-radius: 6px;
padding: 5px 0;

position: absolute;
z-index: 1;
bottom: 100%;
left: 50%;
margin-left: -60px;
}
.tooltip:hover .tooltiptext {
visibility: visible;
}
```

Bu tanımlamalar ile beraber HTML nesnesi aşağıdaki gibi görüntülenir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627387824712.png)

**Elektronik Formda HTML nesnesi kullanarak YouTube videosunu nasıl
gösterebilirim?**

Aşağıdaki HTML kodu kullanılarak HTML bileşeni ile video form üzerindegösterilmiştir. iframe ile başlayan bölüm YouTube üzerindeki videodankısa yol oluşturma yöntemi ile alınmıştır.

```{.markup data-language="markup"}
<p></p>YouTube Örnek Videosu;</p>
<center>
<iframe width="560" height="315" src="{{data.yazi2}}" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
```

Aşağıdaki örnek yardımı ile herhangi bir sitedeki video gösterilmiştir;

```{.markup data-language="markup"}
<center>
<iframe width=600 height=340 
frameborder="0" 
scrolling="no" 
src="https://screencast-o-matic.com/player/cYfnXL4kkF?ff=1&title=0&controls=1" 
allowfullscreen="true"></iframe>
</center>
```

**Elektronik Formda HTML Bileşeni ile ses dosyası nasıl
çalabilirim?**

Aşağıdaki örnek aracılığı ile elektronik forma bir mp3 kaydı eklenmiş veçalınabilir olması sağlanmıştır.

```{.markup data-language="markup"}
<audio controls="controls" src="https://www.w3schools.com/tags/horse.mp3">
        Your browser does not support the HTML5 audio element.
    </audio>
```

Yukarıdaki kod ile aşağıdaki nesne elektronik form üzerinde gösterilir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1627388305846.png)

**Elektronik Formda CSS kod alanı nasıl
kullanılır?**

Elektronik formların kodlama bölümünde CSS bölümü bulunur. Bu bölümeihtiyaç duyulan tüm CSS ler yazılabilir.

Örnek: Bir yazı alanını css ile aşağıdaki gibi büyük harf olmasısağlanır.

```{.css data-language="css"}
.formio-component-MUSTERI_NO .form-control{
    text-transform: uppercase;
}
```

**Elektronik Formda lokalizasyon nasıl
kullanılır?**

Elektronik formların ara yüzlerindeki nesnelerde lokalizasyon yapmakiçin formların kodlama bölümündeki lokalizasyon bölümü kullanılabilir.Burada ekle ile yeni başlıklar oluşturmak ve eklemek mümkündür. Dahasonra kod içinde bu değerler aşağıdaki gibi kullanılabilir.

```{.javascript data-language="javascript"}
var msgKey = "_INVALID_MSG_";    // Localization alanıda bu key için değerler                                                
var msg    = PwForm.Culture(msgKey); // oluşturulur.
```

 **Elektronik Formda  Paperwork geliştirme katmanı metodları  nasıl
kullanılır?**

```{.javascript data-language="javascript"}
var hdr = [
        { field: 'Name', title: 'Type Name' },
        { field: 'Title', title: 'Type Title' },
        { field: 'ObjectId', title: 'Type Id' }
    ];
  PwForm.getPL("/Services/Lookup/GetTypes", { usageType: 'FLOW', objectId: '', checkPerms: false }).then(result => {
        PwForm.fillGrid('pwkendogrid', result, hdr);
class="token punctuation">;
    });
```

**Elektronik Formda form bileşeni için değişimi olayı nasıl
tanımlanır?**

```{.javascript data-language="javascript"}
//------------ Yükleme Sonrası----------------------------
var  listName = "pwselect";
PwForm.setEvent(listName, 'Change',function(){
        //---- Code    
   });
```