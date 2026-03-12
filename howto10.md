Aşağıdaki kod örneği akış eklentisinin adını değiştirmek için
kullanılabilir. Çoğunlukla akış eklentisinin dosya kartı olması
durumunda dosya kartı kayıtlarının nesne adları dosya kartı taslağının
adıyla oluşmaktadır. Son kullanıcılar da bu dosya kartı kayıtlarına
gitmek istediklerinde Belgelerim ekranında hep aynı isimde kayıtları
görürler. Hangi kayıt üzerinde işlem yapacağını belirlemek adına kaydın
nesne adını güncellemek gerekir. Bu işlemi aşağıda paylaşılan kod ile
makro aktivitesinde yapabilirisiniz.

``` {.csharp code-id="section-1669097983829" data-language="csharp"}
try {
    LoadObject();
    LoadAttachment();
    Log("İzin Talep Arşiv Listesi nesne adı güncelleme makrosu başladı. Dosya Kartı Nesne Numarası : " + AttachmentId);
    ObjectID oid = new ObjectID(AttachmentId);
      
        DateTime baTarihi = (DateTime) FormData.Get("BASLANGIC_TARIHI");
        
        a_Card card = Server.productivity.rCard.GetCard(oid, true);
        card.CardData.Set("OBJECT_NAME","İzin Talep Arşiv - " +FormData.Get("AD_SOYAD")+" - "+baTarihi.Year.ToString()+"-"+baTarihi.Month.ToString().PadLeft(2,'0')+"-"+baTarihi.Day.ToString().PadLeft(2,'0'));
        a_GenericResult retval = Server.productivity.rCard.SaveCard(card);
        Log("İzin Talep Onay Akış ekinde dosya kartı nesne adı güncellendi.");
        if (retval.ErrorCode != 0)
        throw new Exception(retval.Message);

}
catch (Exception ex) {
    throw new Exception("İzin Talep Arşiv Listesi nesne adı bilgileri güncelleme makrosu çalışırken hata oluştu. Hata: " + ex.Message);
}
```
