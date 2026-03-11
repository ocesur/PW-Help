Aşağıda örnek olarak paylaşılan kod akışın eklentisinin olması durumunda
eklentiye ait tip alanlarının güncellenmesinde kullanılabilir.

``` {.csharp data-language="csharp"}
try
{
    Log("İzin Talep Arşiv Dosya kartı güncelleme makrosu başladı.");
    LoadAttachment();
    LoadObject();
    
    if(string.IsNullOrEmpty(AttachmentId))
        throw new Exception("İzin Talep Onayı Akış ekinde dosya kartı kaydı bulunmamaktadır.");
    AttachmentData.Copy(FormData);
    //NOT: Bir üst satırdaki kod akış tipi alanları ile Eklentideki tip alan adları , uzunlukları ve veri tipleri aynı olan alanların güncellemesini yapar.
    //     akış tip alanı ile eklentinin tip alan adları farklı ise aşağıdaki örnek ile alanlar eşleştirilmeldir.
    //     AttachmentData.Set(FormData, "DEGISIKLIK_TALEP_TARIHI", "TALEP_TARIHI"); DEGISIKLIK_TALEP_TARIHI akış tip alan adı, TALEP_TARIHI Eklentinin tip alan adıdır.
    
    // Akış Tipindeki bir grup içindeki tüm veriyi akış ekindeki tipin grubuna kopyalamak için örnek aşağıdaki gibidir. 
    // Örnek kodda BAKIM_ANLASMALARI grup adıdır. Her iki tipde de aynı isimle grup oluşturulmuştur. Grup alan isimleride aynıdır. 
    // Bu durmda yukarıda paylaşılan AttachmentData.Copy(FormData); kodu grupları alanlarınıda kapsar. 
    // Grup adları ve alanları tiplerde farklı ise aşağıdaki örnek kod ile alanlar eşleştirilebilir.
       List<MappingClass> mappingBAKIM_ANLASMALARI= new List <MappingClass>();
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="ADAM_AY_UCRETI",Source="ADAM_AY_UCRETI" });
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="ADAMGUN_UCRETI",Source="ADAMGUN_UCRETI" });
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="BAKIM_AKTIF_PASIF",Source="BAKIM_AKTIF_PASIF" });
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="BAKIM_TUTAR",Source="BAKIM_TUTAR" });
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="BASLANGIC_TARIHI",Source="BASLANGIC_TARIHI" });
       mappingBAKIM_ANLASMALARI.Add(new MappingClass(){Destination="BITIS_TARIHI",Source="BITIS_TARIHI" });
       AttachmentData.CopyRep(FormData, "BAKIM_ANLASMALARI", "BAKIM_ANLASMALARI",mappingBAKIM_ANLASMALARI, RepCopyType.All, true); 
       // true parametresi hedef tabloyu temizliyor sonra insert ediyor. false ise tabloyu temizlemeden üzerine yeni satır olarak ekliyor.
        
    SaveAttachment();
    Log("İzin Talep Arşiv Dosya Kartı Güncelleme makrosu başarıyla sonlandı.");
}
catch(Exception ex)
{
    throw new Exception("İzin Talep Arşiv Dosya kartı güncelleme makrosu çalışırken hata oluştu. Hata: " + ex.Message);
}
```
