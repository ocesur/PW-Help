#### WorkingMinutes Kullanımı

Metot içerisinde WorkingMinutes fonksiyonu kullanımı aşağıdaki örnekte
gösterildiği gibidir.

``` {.csharp code-id="section-1713954617327" data-language="csharp"}
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
          DateTime dateTime2 = DateTime.Now.AddDays(1);
          // Takvim adı
          // Başlangıç tarihi
          // Bitiş tarihi
          // WorkingMinutes parametreleri yukarıdaki sırada kullanılabilir.
          var hesaplama = RuleEngine.WorkingMinutes("2024 Takvim", dateTime, dateTime2);
          Log("Sonuç: " + hesaplama.ToString());
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
}
```
