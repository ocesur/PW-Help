**[**[Elektronik ]{style="box-sizing: border-box; font-size: 18px;"}**
Formda SAP entegrasyonu ile veri tablosu nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript data-language="javascript"}
var gridName = "pwkendogrid";
var sapConnectorName = "pwsapint";
var hdr = PwForm.getIntHeader(sapConnectorName, 'VENDOR');
var _pwsapint = PwForm.component(sapConnectorName);
```

**[]{style="box-sizing: border-box; font-size: 18px;"}**[]{style="box-sizing: border-box; font-size: 18px;"}[**Elektronik **]{style="box-sizing: border-box; font-size: 18px;"}** Formda
SAP \'ye tablo içinde veri nasıl gönderebilirim?**

``` {.javascript data-language="javascript"}
function SAP_GetCustomerList() {
try {
        PwForm.Progress(true);
        //SAP nesnesi üzerinden input parametreleri doldurulur.
        var sapConnectorName = "intsap2"; 
        var _intsap2 = PwForm.component(sapConnectorName); 
        var listName = "MUSTERI" 
        //SAP table bulunarak kolonları doldurulur. 
        var tablo = _intsap2.getParam('IDRANGE');
        tablo[0].SIGN = "I";
        tablo[0].OPTION = "BT";
        tablo[0].LOW = "1";
        tablo[0].HIGH = "ZZZZZZZZZZ"; 
        //SAP tablosu ilgili alana eklenir.
        _intsap2.setParam('IDRANGE', tablo);        
        _intsap2.setParam('MAXROWS', 1000);
        _intsap2.setParam('CPDONLY', ""); 
        //Hazırnalan SAP datası SAP ye gönderilerek cevap beklenir
        _intsap2.callFunction(function () {
            PwForm.fillIntList(listName, 'NAME', 'NAME', sapConnectorName, 'ADDRESSDATA');
            PwForm.Progress(false); 
        });
    }
    catch (ex) {
        PwForm.Log("SapmaStart1/SAP_Metodunu_Calistir1 failed.", ex);
        PwForm.Error("Hata", "SapmaStart1/SAP_Metodunu_Calistir1 failed. " + ex);
    }
}
```
