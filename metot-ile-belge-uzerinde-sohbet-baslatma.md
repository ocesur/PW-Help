#### Metot ile Belge Üzerinde Sohbet Başlatma

Aşağıda bulunan kod parçacığı ile belirlenen kullanıcıların dahil olduğu
bir sohbet belge üzerinde başlatılabilir.

``` {.csharp code-id="section-1711959757858" data-language="csharp"}
public void InternalExecute()
{
  //Sohbet Oluşturulacak belgenin nesne numarası
  string object_id = "FF000100000C3407";
  
  //Sohbet Katılımcılarının giriş adı değerleri bu listeye atanmalı
  List<string> chatUsers = new List<string>{"cpece", "aduz", "obelkeci", "doge", "asaygili", "eozteris"};

  //Sohbet Konusu
  string subject = "Portal Örnek";
  var result = server.rInbox.ChatCreate(object_id, 1, subject, chatUsers);
  if(result.ErrorCode != 0)
  {
    throw new Exception(result.Message);
  }
}
```

Sonuç ekranı şu şekilde olacaktır :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1711959825723.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1711959832923.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
