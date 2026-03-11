Akışın eklentisine eklediğimiz belgenin aynı zamanda hedeflenen başka
bir klasörde de kısayolunun oluşturulması örneğini makro adımında
yapacağız. 

Bunun için SDK fonksiyonlarımızdan rDocument altında bulunan
ClipBoardApply() metodumuzdan faydalanacağız.

``` {.csharp code-id="section-1717411009508" data-language="csharp"}
try{
    LoadAttachment();
    var cbSet = Server.productivity.rDocument.ClipBoardSet(AttachmentId);
    if(cbSet.ErrorCode == 0){
        Log("Eklenti panoya kopyalandı.");
        List<string> attIds = new List<string>();
        attIds.Add(AttachmentId.ToString());
        //rDocument.ClipBoardApply(string action, string folderId, List<string> objectIds);
        var cbApply = Server.productivity.rDocument.ClipBoardApply("LINK", "FF51510000007DB3", attIds);
        if(cbApply.ErrorCode == 0){
            Log("Kısayol oluşturuldu.");
        }
        else{
            Log("Kısayol oluşturulamadı.");
        }
    }
}
catch(Exception ex){
    throw ex;
}
```

ClipBoardApply() metodumuza 1. parametre (action) için "LINK" değerini
kısayol oluşturacağımızdan dolayı veriyoruz, 2. Parametre (folderId)
için hedeflenen klasörün foledId değerini veriyoruz, 3. Parametre
(objectIds) burası önemli, 'List\<string\>'  tipinde olmak zorundadır ve
eklemek istediğimiz eklentilerin ID değerlerini alıp metodu çağırmadan
önce bu List için dolduruyoruz.

Kısayol için koşullara bağlı bir şekilde de kendi ihtiyaçlarınıza uygun
makro tasarımları yapabilir, dinamik şekillerde eklentilerinizin
kısayollarını oluşturabilirsiniz.

Bu yazıdaki örnekte sürecimde kullandığım 'Test' isimli klasöre
 eklediğim 'test.txt'

adındaki belge ile akışı başlatıp yukarıda örneğini vermiş olduğum makro
adımından geçtikten sonra 'Depolama Birimi' isimli klasörde kısayolunun
oluşmuş olduğunu görmüş oluyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1717411056633.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
