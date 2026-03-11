**Akışı başlatırken belirli bir klasörde ekli belge sayısını nasıl
kontrol ederim?**

Not: Aşağıdaki kodlar 5.0 ve 5.1 versiyonlarında çalışmaktadır.

Akışın ekinde bir dosya kartı kaydı olduğunda akışı başlatırken Ruhsat
Fotokopisi isimli klasördeki belge adedi kontrol edilmiş, 3 den fazla
olmaması durumunda hata vererek akışın başlaması engellenmiştir.

``` {.javascript code-id="section-1658482809793" data-language="javascript"}
var cnt = 0;
$.each($("#attc-tree-container .k-item"), function (i, chlds) {
   var itm = $(chlds);
    if (itm.find('.fa-folder').parent().length > 0) {
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Ruhsat Fotokopisi') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
    }
});
if (cnt < 3) {
    PwForm.Error("Uyarı", "Ruhsat Fotokopisi isimli klasöre en az 3 adet belge eklemek zorunludur! Eki belge sayısı : " +cnt );
    return false;
}
else
    return true;
```

**Akış başlatma ekranında belirli klasöre belge ekleme zorunluluğu
kontrolünü nasıl yaparım?**

Aşağıdaki örnekte akışın ekinde dosya kartı kaydı bulunmaktadır. Dosya
kartının belirtilen klasöründe belge olup olmadığı kontrol edilmiştir.

``` {.javascript code-id="section-1658482809798" data-language="javascript"}
var cnt = 0;
$.each($("#attc-tree-container .k-item"), function (i, chlds) {
     var itm = $(chlds);
    if (itm.find('.fa-folder').parent().length > 0) {
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Ruhsat Fotokopisi') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length        
    }
});
if (cnt === 0) {
    PwForm.Error("Uyarı", "Ruhsat Fotokopisi isimli klasöre belge eklemek zorunludur!");
    return false;
}
else
    return true;
```

**Akış başlatılırken belge sayısı kontrolünü nasıl yaparım?**

Aşağıdaki örnekte dosya kartının tüm klasörlerindeki belge sayılarının
toplamı kontrol edilmiştir.

``` {.javascript code-id="section-1658482809801" data-language="javascript"}
var cnt = 0;
$.each($("#attc-tree-container .k-item"), function (i, chlds) {
    var itm = $(chlds);
    if (itm.find('.fa-folder').parent().length > 0) {
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Ruhsat Fotokopisi') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Police Fotokopisi') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Ehliyet Fotokopisi') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Police Pirim Makbuzu') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
        if (itm.find('.fa-folder').parent()[0].innerText.includes('Alkol Raporu') && itm.find('.fa-file').length !== 0)
            cnt = cnt + itm.find('.fa-file').length;
    }
});
if (cnt !== 2) {
    PwForm.Error("Uyarı", "Dosya kartı kaydına sadece 2 adet belge eklemek zorunludur! Ekli belge sayısı : " + cnt);
    return false;
}
else
    return true;
```

**Akış adımını bitirirken belge sayısını nasıl kontrol ederim?**

İş Akışı Eklenti Tanımı Dosya Kartı olan bir sürecimizde belirlediğimiz
bir manuel adım aktivitesinde dosya kartına belge ekleme yapılıp
yapılmadığının kontrol edilebilmesi için akışın ekinde dosya kartı
eklentisi olmalıdır.

Senaryomuz gereği akışı başlatırken en az bir adet belge ile
başlatılması zorunlu tutulmuştur. Sonraki adımda ise yeni belge ekleme
kontrolü istenmektedir.

Belge kontrolü yapılacak manuel aktivitede tanımlı olan elektronik form
üzerinde aşağıdaki kodlama yapılır. Elektronik Formun Kodlama kısmında
Global Fonksiyonlarda bulunacak kod şu şekildedir;

``` {.javascript code-id="section-1658482755725" data-language="javascript"}
function ilerlet()
{
   try {
      var ID= PwForm.ObjectId; //PwForm.Error(PwForm.Culture('Object Id Bilgisi'), PwForm.Culture(PwForm.ObjectId));
      debugger;
      var sql = "SELECT CHILD_ID FROM PW_WORKFLOW W(NOLOCK), PW_VIRTUAL_DOCS V(NOLOCK), PW_SYSOBJECT S(NOLOCK)  WHERE W.ATTACHMENT_ID=V.OBJECT_ID AND V.CHILD_ID=S.OBJECT_ID AND V.CONTENT_TYPE='D' AND S.IS_DELETED=0 AND W.OBJECT_ID='" + ID + "'";
      //PwForm.Error(PwForm.Culture('SQL Sorgusu'),PwForm.Culture(sql));
      PwForm.Query(sql,'').then(result => {
         if ((result.length <2) && (PwForm.get('ADI_SOYADI') == "Onur Cesur")) {
         PwForm.Error(PwForm.Culture('Belge Eklemek Zorunlu'), PwForm.Culture('Belge Eklemek zorunludur! En az 1 adet belge ekleyiniz.'));   
         return false;
         }
         else{
            PwForm.Complete();
         }
        });
}
catch(wzerror){
   PwForm.Error(PwForm.Culture("Hata"), wzerror);
}        
}
```

** **Formun üzerinde bir Tuş olmalı. Tuş Nesnesinin özelliklerinde
Aksiyon başlığında "**Özel**" seçeneği seçilmelidir. Özel İşlem başlığı
altında da **ilerlet();** kodu eklenmelidir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1651126222754.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable style="width: 400px;"}

Örneğin videosu aşağıdaki gibidir.

\
