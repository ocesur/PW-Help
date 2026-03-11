**[Elektronik formda DBPlugin ile diğer veri tabanlarına nasıl
erişebilirim.]{style="font-size: 18px;"}**

[Şu sayfada](/tr/docs/dbplugin){rel="nofollow" translate="no"} DBPlugin
yapısı ve örnek koduna erişebilirsiniz.[]{.token .punctuation}[]{.token
.punctuation}[]{.token .punctuation}

**[Elektronik Formda veri tabanı sorgusu  nasıl
kullanılır?]{style="font-size: 18px;"}**

``` {.javascript data-language="javascript"}
var hdr = [{ field: 'LOGIN_NAME', title: 'Giriş Kodu' }, { field: 'USER_NAME', title: 'Kullanıcı Adı' }];
   PwForm.Query('SELECT TOP 100 LOGIN_NAME,USER_NAME FROM PW_USER(NOLOCK)', '').then(result => {
        PwForm.fillGrid('pwkendogrid2', result, hdr)
```

**[Formda bir alana veri tabanından alınan değerin aktarılması nasıl
yapılır?]{style="font-size: 18px;"}**

``` {.javascript data-language="javascript"}
function position_atama(){
var hdr = [{ field: 'TITLE', title: 'Pozisyonu'}];
var query = String.Format("SELECT P.TITLE FROM PW_USER U LEFT OUTER JOIN PW_POSITION P ON U.POSITION=P.NAME WHERE P.NAME='{0}'",CurrentUser.UserPosition);
PwForm.Query(query,'').then(result => {PwForm.set('POZISYONU', result[0].TITLE);});
}
```

**DBPlugin ile başka bir veri tabanındaki veri ile dinamik liste nasıl
oluştururum?**

Senaryomuza göre LogoTiger veri tabanına plugin ile bağlantı yapılarak
Logodaki Gider Grupları listesini alacağız ve Paperwork HTML5 formda bir
liste nesnesini dolduracağız. İlk önce bir plugin tanımı yapılır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1651042686863.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

Form tasarım ekranında forma eklenen liste nesnesinin özelliklerinde
Liste tabında veri kaynağı tipi **"Değişken"** olarak seçilmelidir.
Kodlama bölümündeki işlemler yapıldıktan sonra Listenin özelliklerindeki
Kaydedilecek Alan, Özel Değer ve Liste Görünümü ayarları aşağıdaki
görselde görüldüğü gibi yapılmalıdır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1651042720541.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

Form Tasarım ekranında Kodlama tabındaki Global Fonksiyonlar altına
aşağıdaki kodlama yapılmalıdır.

``` {.javascript data-language="javascript"}
var GiderGrpList=[];

function GiderGruplariListesi() 
{
   var sql = "SELECT [KART ÖZEL KODU] AS [MASRAF_MERKEZI_KODU_FILTRE],[KART ÖZEL KOD TANIMI] AS [MASRAF_MERKEZI_ACIKLAMASI_FILTRE] FROM "+ 
      "(SELECT * FROM EV_MUH_HRK_005_06 MK5 (NOLOCK)"+
      "UNION ALL "+
      "SELECT * FROM EV_MUH_HRK_006_15 MK6 (NOLOCK) "+
      "UNION ALL "+
      "SELECT * FROM EV_MUH_HRK_011_06 MK11 (NOLOCK) "+
      "UNION ALL "+
      "SELECT * FROM EV_MUH_HRK_003_01 MK3 (NOLOCK) "+
      "UNION ALL "+
      "SELECT * FROM EV_MUH_HRK_007_01 MK7 (NOLOCK) "+
      "UNION ALL "+
      "SELECT * FROM EV_MUH_HRK_012_01 MK12 (NOLOCK) "+
      ") BUTCE "+
      "WHERE ([MASRAF MERKEZİ KODU] IS NOT NULL OR [MASRAF MERKEZİ KODU]<>'') AND  [MASRAF MERKEZİ KODU]<>'A99999'AND [MASRAF MERKEZİ KODU] LIKE '%"+
      PwForm.get("MASRAF_MERKEZI_ACIKLAMASI_FILTRE")+"' "+
      "GROUP BY [KART ÖZEL KODU],[KART ÖZEL KOD TANIMI] "+
      "ORDER BY [KART ÖZEL KOD TANIMI]";
   console.log(sql);
   PwForm.Query(sql,'LogoTiger',0).then(result => {
   try
   {
      GiderGrpList=[];
      for  (  var i=0;i<result.length;i++){
      GiderGrpList.push( {Key1 : result[i]["MASRAF_MERKEZI_ACIKLAMASI_FILTRE"],Key2: result[i]["MASRAF_MERKEZI_KODU_FILTRE"]});
      PwForm.component('MASRAF_MERKEZI_KODU_FILTRE').component.data.values=GiderGrpList;
      PwForm.component('MASRAF_MERKEZI_KODU_FILTRE').redraw();   
   }  
   }
     catch (ex)
   {
     PwForm.Error("Hata", ex);
   }
});
} 
```

Yükleme Sonrası olayına ise aşağıdaki kodlama yapılmalıdır.

``` {.javascript data-language="javascript"}
    PwForm.setEvent('textfield','Change',function(){
       MasrafMerkeziListesi();
       GiderGruplariListesi();
    });
```

Yapılan çalışmanın videosu aşağıdaki gibidir.
