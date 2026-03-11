#### Elektronik Formda Takvimde Bulunan Tatil Günleri Nasıl Listelenir?

Amacımız, sistemde tanımlı olan takvim tanımına eklenen tatil günlerinin
isimlerini, başlangıç ve bitiş tarihlerini forma eklenen bir veri
tablosu nesnesinde göstermek.

Örnek bir form tasarımı yapalım :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1753885903283.png){.fr-fic
.fr-fil .fr-dib .fr-draggable .fr-bordered .fr-shadow
style="width: 900px;"}

Form arkasında global fonksiyonlar alanına aşağıdaki kod parçasını
ekleyelim :

``` {.javascript code-id="section-1704783250871" data-language="javascript"}
async function GetHolidays()
{
    //Takvim Adı
    let calendarName = "2023 Takvim";
    //Veritabanından takvim id si alınır
    let calendar = await PwForm.Query(String.Format("SELECT CALENDAR_ID as OBJECT_ID FROM PW_CALENDAR(NOLOCK) WHERE CALENDAR_NAME = '{0}' ", calendarName),"");
    
    // Productivityden takvime ait detaylar alınır
    let a_Calendar = await PwForm.getPL("/Services/Admin/GetCalendar", {calId : calendar[0].OBJECT_ID});

    //Takvim detayındaki her bir tatil günü için işlem yapılır
    for(let tatil of a_Calendar.Details)
    {
        //Başlangıç tarihi ve başlangıç saati birleştirilerek Tarih/Saat tipine dönüştürülür.
        let baslangicTarihi = PwForm.moment(kendo.parseDate(tatil.StartDate)).add(tatil.StartTime.TotalSeconds, 'second').toDate();
        
        //Bitiş tarihi ve bitiş saati birleştirilerek Tarih/Saat tipine dönüştürülür.
        let bitisTarihi = PwForm.moment(kendo.parseDate(tatil.EndDate)).add(tatil.EndTime.TotalSeconds, 'second').toDate();

        // tatilGünleri adıyla oluşturulmuş veri tablosuna txtTatilAdi,dtBaslangicTarihi,dtBitisTarihi neslerine değer atayıp, yeni satır atar.
        PwForm.AddRowData("tatilGunleri", {txtTatilAdi: tatil.Name, dtBaslangicTarihi: baslangicTarihi, dtBitisTarihi: bitisTarihi});
    }
    //Tablo tekrardan çizilir.
    PwForm.component("tatilGunleri").redraw();
}
```

Yükleme sonrasında yazdığımız fonksiyonu çağıralım (İstenirse buton gibi
bir işlevle de çağırılabilir) :

[GetHolidays]{style="font-size:14px;font-family:Consolas;color:teal;"}[();]{style="font-size:14px;font-family:Consolas;color:black;"}

\

Alacağımız sonuç şu şekilde olacaktır : 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1753885864246.png){.fr-fic
.fr-fil .fr-dib .fr-draggable .fr-shadow .fr-bordered
style="width: 900px;"}

\
