İş akışlarımızda bazen makro aktivitelerini kullanma ihtiyacımız oluyor.
Makro aktivitelerinde çok çeşitli görevler kodlanarak yapılabiliyor. Bu
yapı içerisinde bazen öngörülemeyen yada hesaplanamayan durumlarda makro
aktivitesi hata alabiliyor ve hata kullanıcısına hatalı beklemede olarak
iş düşebiliyor. Hata kullanıcısı bazen buradaki hataların çözümünde
yeterli olamayabiliyor. Ayrıca birçok süreç için aynı kişi hata
kullanıcı olabilir. Makrolarımızda alınabilecek hatalar için hata
kullanıcısı yerine bir manuel adıma iş düşürülebilir. Biz buna hata
mekanizması diyoruz.

Bu işlemi aşağıda anlatılan şekliyle örnekleyebiliriz.

Senaryomuza göre bir makro adımı var. Bu adımda veri tabanından veya
akışın verileri üzerinden bazı alanlar kullanılarak hesaplar yapılıyor.
Bu hesaplamalar esnasında örneğin veri tabanında olması gereken veri
dönmüyor. Şu anda biz hiçbir şey yokmuş gibi ilerletiyoruz. Bu durumda
özellikle üretim ortamında akış verisi ile oynamamıza veya takla
atmamıza sebebiyet veriyor.

Tasarımımıza aşağıdaki gibi bir yapı eklersek bu sorunların daha görünür
olmasını, hata var ise düzeltilmesini ve bilinmesini sağlayabiliriz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1639396022381.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

Yukarıdaki senaryoda makro adımında veri tabanından örneğin kur bilgisi
makro adımında alınıyor ve hesaplama yapılıyor. Zaman zaman da kur
bilgisi bulunamıyor. Akışı yukarıdaki gibi değiştiriyoruz;

1.  Tip üzerinde 2 alan daha tanımlıyoruz;
    1.  HaveError: Yazı(1)
    2.  ErrorDef:Yazı(500)
2.  Makroda işlem yaparken kur bilgisi bulunamaz ise;
    1.  HaveError='T'
    2.  ErrorDef='XXX tarihli kur bilgisi bulunamadı. YYY tablosunda bu
        değerin oluşturulmasını sağlayınız ve akışınızı ilerletiniz'
    3.  Kur bilgisi bulunur ise;
    4.  HaveError='F'
    5.  ErrorDef=''
3.  Makrodan sonraki Karar adımında HaveError kontrol edilir. F ise akış
    sağ tarafa doğru devam eder. T ise manuel aktiviteye yönlenir.
4.  Manuel aktiviteye bir elektronik form tasarlanır. Sadece ErrorDef
    alanının bir Başlık alanında görüntülenmesi sağlanır. Yerine getiren
    olarak kurum içinde akışların desteğini veren veya izlemesi gereken
    kullanıcı atanır.
5.  Manuel adım sahibi Kur bilgisinin makroda alınabilmesi için gerekli
    olan çalışmayı tamamlar ve akışı tekrar makro adımına yönlendirir.

 

Bu neyi sağlar? Kur bilgisi bulunamamış ise hesapların gereksiz yapılıp
akışın devam etmesi önlenir. İzlenmesi ve hatanın giderilmesi sonucu
akışın kaldığı yerden devam etmesini sağlar.

 

[Makro adımında 1 adet ihtimal olmayabilir. Bu durumda her ihtimal için
ayrı ErrorDef tanımı yapılıp her biri için Manuel adıma gitmesi
sağlanabilir.]{style="box-sizing: border-box; font-size: 15px; font-family: Calibri, sans-serif;"}

``` {.csharp code-id="section-1671432652538" data-language="csharp"}
try{
  Log("Makro Kur alma başladı. Akış No: " + WorkflowId); //log dosyasına yazılmasını sağlar.
    var KUR = string.Empty;
    KUR = FormData.Get("KUR_BILGISI")
    if(KUR==""){
    FormData.Set("ERRORDEF","’XXX tarihli kur bilgisi bulunamadı. YYY tablosunda bu değerin oluşturulmasını sağlayınız ve akışınızı ilerletiniz");
    FormData.Set("HAVEERROR","T");
    }
    else
    {
        // bu bölümde kur bilgisi alındığındaki yapılacak işlem kodlanır.
    FormData.Set("ERRORDEF","");
    FormData.Set("HAVEERROR","F");  
    }
  SaveObject(); // Tip alanlarına kod içerisinde bir değer atama yapılıyorsa onun kaydedilmesini sağlar
}
catch(Exception ex)
{
  Log("Hata:"+ex.Message+ "-" + WorkflowId); //log dosyasına hatanın yazılmasını sağlar.
  return  true;
}
```

\

\
