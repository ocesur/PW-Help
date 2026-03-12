#### Metotta Kabinet İçerisinde Yer Alan Elemanlara Erişme

Metot içerisinde, eğer kabinet yolu biliniyorsa, o kabinetin içerisinde
bulunan elemanları getirmek için aşağıda bulunan kod kullanılabilir.

 

``` {.csharp code-id="section-1687247526896" data-language="csharp"}
// Kabinetin yolu (TR_CABINETS -> Belgeler sayfasına işaret eder tüm kabinet yollarının başında olması gerekir)

string path = @"TR_CABINETS\Egitim";
// Verilen kabinet yoluna kadar olan tüm kabinetlerin bilgilerini liste olarak döner
a_PathInfo pi = server.rNavigation.getFolderPath(path);

// Listenin son elamanı verdiğimiz yoldaki son adıma işaret ettiğinden son elaman alınır
string str_folderId = pi.ObjectList[pi.ObjectList.Count - 1];

// Verilen nesne numarasına ait klasörün tüm elemanlarını döner
a_FolderInfo folderinfo = server.rNavigation.GetFolderInfo(str_folderId);

// Klasör içerisindeki elemanlar tek tek işlenebilir
foreach (a_FolderItemInfo item in folderinfo.Items)
{
    // Klasör elemanının türüne göre istenilen işlem yapılabilir.
    switch(item.ContentType)
    {
        case "CARD":  // Dosya kartı ise
            a_Card card = server.rCard.GetCard(new ObjectID(item.ObjectId), true, true);
            Log(item.ObjectName);
            break;
        case "DOC":  // Arşiv ise
            ITypes doc = server.rDocument.getDocument(new ObjectID(item.ObjectId));
            break;
        case "FOLDER":  // Klasör ise
            Log(item.ObjectName);
            break;
        default:
            Log(item.ObjectName);
            break;
    }
}
```

\

\
