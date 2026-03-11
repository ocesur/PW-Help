Bu örnek, kabinet içerisindeki bir belgeye eklenmiş olan notları,
belgenin elektronik formu üzerinde bulunan veri tablosunda listeleme
örneğidir.

Bunun için öncelikle global fonksiyonlara aşağıdaki javascript kodu
eklenmelidir.

``` {.javascript code-id="section-1703509595255" data-language="javascript"}
async function getNotes()
{
    if(!PwForm.ObjectId) return;
    let a_NoteList = await PwForm.getPL("/Services/Document/GetNotes", {objectId: PwForm.ObjectId, pageIndex: -1})
    debugger;
    for(let a_Note of a_NoteList.Items)
    {
        PwForm.AddRowData("kendoGrid2", {txtNotuYazan: a_Note.Owner, txtNot: a_Note.Message, dtNoteTarihi: kendo.parseDate(a_Note.CreateDate)});
    }
    PwForm.component("kendoGrid2").redraw();
}
```

Daha sonra yükleme sonrasında yukarıda yazdığımız fonksiyonu
çağırmalıyız.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703509733669.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Veri tablosu ise şu şekilde oluşturulmalıdır :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703509758944.png){.fr-fic
.fr-fil .fr-dib .fr-shadow .fr-bordered}

Şu şekilde örnek notlar ekleyelim : 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703509784659.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Sonucunda gelişmiş veri tablosunda şu satırları görmeliyiz : 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703509806100.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
