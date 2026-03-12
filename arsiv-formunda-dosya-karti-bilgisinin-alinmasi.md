#### Arşiv Formunda Dosya Kartı bilgisinin alınması

[]{style="white-space:pre;"}Dosya kartı içinde bulunan arşiv
belgelerinin formlarında, belgelerin bulundukları dosya kartlarına ait
bilgilere erişebilmekteyiz. Bu sayede arşiv formunda bulunan alanların
güncellenmesi gibi işlemler yapılabilmektedir.  

Aşağıda bulunan JavaScript kod örneği arşiv tipinde bir belgenin
formunda, global fonksiyonlarda kullanılabilir. Bu kodun çalışabilmesi
için bu arşiv tipinin bir dosya kartı tanımının altında olması
gerekmektedir.

``` {.javascript code-id="section-1699861200015" data-language="javascript"}
function dKGetVal() {
    //PwForm.MasterData  nesnesi ile birlikte arşiv belgenin içerisinde bulunduğu dosya kartı bilgilerine erişebilmekteyiz.
    //Eriştiğimiz bilgilere örnek olarak; Dosya kartının ObjectId değeri, Yetkiseti ismi, yetkiseti no, Dosya kartının bulunduğu konum
    //Dosya kartının ObjectId değerini burada Arşiv belgenin formunda ki "ANA_KAYIT_ID_NO" alanına atanıyor.
    PwForm.set("ANA_KAYIT_ID_NO", PwForm.MasterData.OBJECT_ID);
    //pwSysObject fonksiyonu bize boş bir sabit paperwork nesnesi dönüyor.  
    var pwo = pwSysObject();
    //Ardından load komutu ile bu boş nesneye yüklemek istediğimiz nesnenin ObjectId değerini veriyoruz. Bu şekilde yüklediğimiz bu kaydın bilgilerine erişebiliyoruz.
    pwo.load(PwForm.MasterData.OBJECT_ID).then(function() {
        //Burada Dosya kartının objectId değerini verdik ve Dosya kartının alanlarından olan "BELGE_ADI" alanının değerine ulaşıyoruz.
        var belgeAdi = pwo.get("BELGE_ADI");
        //Ulaştığımız Dosya kartı alanının değerini Arşiv kaydının alanlarından olan "FORM_ADI" alanına atayabiliyoruz.
        PwForm.set("FORM_ADI", belgeAdi);
    }).catch (function() { console.log("hata") })
}
```
