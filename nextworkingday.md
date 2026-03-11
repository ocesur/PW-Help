Metot içerisinde NextWorkingDay Kullanımı

Metot içerisinde NextWorkingDay fonksiyonu aşağıdaki kodlamada göründüğü
gibidir.

``` {.csharp code-id="section-1713954354261" data-language="csharp"}
using Paperwork.Methods;
using System;
using System.Collections.Generic;
using System.Text;
namespace ##ASSEMBLY_NAME##
{
  public class ##CLASS_NAME## : PWMethod {
    public override int Execute(Dictionary<string, object> _paramList) {
      this.paramList = _paramList;
      try {
        var info = base.ConnectServer();
        if (info.ErrorCode != "0")
          throw new Exception(info.LMessage);
          LoadRuleEngine();
          DateTime dateTime = DateTime.Now;
          
          // Takvim adı
          // Başlangıç tarihi
          // Eklenecek gün
          // NextWorkingDay parametreleri yukarıdaki sırada kullanılabilir.
          var hesaplama = RuleEngine.NextWorkingDay("2024 Takvim", dateTime, 1);
          Log("Sonuç" + hesaplama.ToString());
          return 0;
        }
      catch (Exception e) {
        Log(e.Message);
        ErrorMessage = e.Message;//Hata duruumunda eposta bilgilendirme hata mesajı içeriğidir.
        return -1;
      }
      finally {
      }
    }
  } 
}
```
