#### Makroda Kural Motoru Kullanımı

Makroda kural motorundaki verilere ulaşmak için öncelikle kural motorunu
çağırabilmemizi sağlayan \"LoadRuleEngine\" fonksiyonunu kullanmamız
gerekiyor. Sonrasında ulaşmak istediğimiz verinin adını
\"RuleEngine.VERI_ADI\"  şeklinde kullanarak makroda ihtiyacımıza göre
şekillendirebiliriz.

Örnek olarak gösterebilmek için basit bir süreç tasarımı oluşturup kural
motorundaki değişkenleri nasıl çağırıp forma atadığımı aşağıdaki
görsellerle sizlere açıklayacağım.

Kural motorundan tanımlı iki değişken bir tablo ve bir de fonksiyonu
kullandığım makro kodu şu şekilde;

``` {.csharp code-id="section-1684412530021" data-language="csharp"}
try{
  LoadObject();
  LoadRuleEngine();
  Log("Test makrosu başladı -ozteris");
    
  var paperWork = RuleEngine.paperwork;
  var owl = RuleEngine.owl;
  var concatStr = RuleEngine.Concat(paperWork, owl);

  Log("Kural Motoru rf değişkeni: " +RuleEngine.paperwork);
  Log("Kural Motoru a1 değişkeni: " +RuleEngine.owl);

  FormData.Set("AD_SOYAD", paperWork);
  FormData.Set("ILCE_", owl);
  FormData.Set("MAHALLE", concatStr);

  ITypes newRow = FormData.getNewRow("URUN_LISTESI");

  foreach(var row in RuleEngine.tablePaperWork.Rows){
    newRow.Set("URUN_",row["Product"].ToString());
    newRow.Set("RENK_",row["Color"].ToString());
    newRow.Set("FIYAT",row["Price"]);
  }
  FormData.AddRepRow("URUN_LISTESI", newRow);
  SaveObject();
}
catch(Exception ex){
  Log("Makro hatası - EKO : " + ex.Message);
  throw new Exception(ex.Message);
};
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684412551117.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684412562931.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684412581133.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 1063px;"}

Makro adımından önce form şu şekildedir :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684412619499.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Makro adımından geçtikten sonra ise alanlar kural motoru değerlerine
göre şu şekilde dolduruluyor :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1684412643565.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 943px;"}

\
