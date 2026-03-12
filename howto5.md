Tasarlayacağımız süreçlerin bazılarında sayaç kavramını kullanmak
gerebilir. Sayaç kullanmak için öncelikle veri tabanında sayaç tanımı
yapılması gerekmektedir. Sonrasında ise iş akışı taslağında makro
aktivitesinde kodlama yapılması gerekmektedir. Aşağıda veri tabanında
sayaç tanımlama için gereken sql komutu vardır. Öncesinde aynı isimde
sayaç tanımlanmış mı kontrol edilmelidir. Aynı isimde birden fazla sayaç
tanımlanamaz.

``` {.plsql code-id="section-1657806000294" data-language="plsql"}
SELECT * FROM PW_COUNTER (NOLOCK) WHERE COUNTER='İzinTalep'
```

İzin sayaç isimli sayaç PW_COUNTER tablosunda bulunmadığı durumda
aşağıdaki insert komutunu çalıştırarak sayaç tanımın yapılmasını
sağlayabilirsiniz. Value değeri sayacın hangi numaradan başlamasını
istiyorsanız o değeri vermelisiniz. Örneğin sayaç 1001 den başlamasını
istiyorsanız value değeri olarak 1000 vermelisiniz. USE
\[ArgusTest_PAPERWORK\] ifadesini sizin ortamınızda ki veri tabanı ismi
ile değiştirmelisiniz. Aşağıdaki kod sayacın 1 ile başlamasını
sağlayacaktır.

``` {.plsql code-id="section-1657806000296" data-language="plsql"}
USE [ArgusTest_PAPERWORK]
GO

INSERT INTO [dbo].[PW_COUNTER]
           ([COUNTER]
           ,[VALUE])
     VALUES
           ('İzinTalep',
           0)
GO
```

Aynı isimde sayaç adı olduğunda ve yukarıdaki kod çalıştırıldığında
aşağıdaki mesajı alırsınız. Bu durumda sayaç adını değiştirmeniz
gerekecektir.

``` {.plsql code-id="section-1657806000297" data-language="plsql"}
Msg 2627, Level 14, State 1, Line 2
Violation of PRIMARY KEY constraint 'PK_PW_COUNTER'. Cannot insert duplicate key in object 'dbo.PW_COUNTER'. The duplicate key value is (İzinTalep).
The statement has been terminated.
```

İş akışı taslağında makro aktivitesinde ise aşağıdaki kod örneği
kullanılabilir. İhtiyacınıza göre de düzenleme yapabilirsiniz.

Aşağıdaki örnek kod çalıştığında 20191200001 sayacını verecektir. 2019
Yılı, 12 Ayı ve 00001 de sayaç numarasını ifade eder.

``` {.csharp code-id="section-1657806000298" data-language="csharp"}
try {
  LoadObject();
  Log("izin talep no sayaç işlemi başladı. Akış No : " + WorkflowId); // Workflow log dosyasına yazılır.
  int count1 = 0;
  int yil = DateTime.Now.Year;
  int ay = DateTime.Now.Month;
  string counter1 = string.Empty;
  string ay1 = string.Empty;
  count1 = Server.productivity.rAdo.getCounter("IzinTalep");
  counter1 = count1.ToString().PadLeft(5, '0'); //sayaç 5 basamaklı olacak ve 0 ile doldurulacak anlamına gelir.
  ay1 = ay.ToString().PadLeft(2, '0'); //Ay 2 basamaklı olacak ve 0 ile doldurulacak.
  FormData.Set("IZIN_TALEP_NO", yil.ToString() + ay1 + "-" + counter1);
  Log("IzinTalepNo: " + yil.ToString() + ay1 + counter1); // Workflow log dosyasına yazılır.
  Log("izin talep no sayaç işlemi bitti. Akış No : " + WorkflowId); // Workflow log dosyasına yazılır.
  SaveObject();
}
  catch (Exception ex) 
{
  Log("IzinTalep hata aldı. Hata Mesajı: " + ex.Message);
  return false;
}
```
