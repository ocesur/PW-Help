Makroda Sistemde Tanımlı Rapor Kaynağı Kullanımı

Bu örneğin amacı sistemde tanımlı rapor kaynaklarını çalıştırıp dönen
sonuç verisini Excel veya Pdf formatında bir belgeye dönüştürüp dışarıya
almaktır.

Sistemde akışın nesne numarası (OBJECT_ID) verisini alarak o akışa ait
tip verisini getiren bir raporumuz olduğunu düşünelim ve akış bitmeden
önceki makroda akışa ait tip verisini dosyalayarak diske yazalım. Bunu
aşağıda yazılan makro kodu ile gerçekleştirebiliriz.

``` {.csharp code-id="section-1698837439077" data-language="csharp"}
try
{
    LoadObject();
    //Sistemde kayıtlı rapor tanımının ismi
    var reportName = "Test Report Source";
    // Oluşturulacak dosyanın formatı
    //Pdf veya Excel olabilir: Büyük/Küçük harfe dikkat edilmeli
    var reportType = "Pdf"; 
    var prms = new List<ReportServer.rReportParam>(); //Parametre Listesi

    // Rapor için tanımlanmış her bir parametre aşağıdaki gibi prms listesine eklenmelidir. Value alanı parametre değeri olarak gönderilecek değer olmalıdır
    // Test için kullandığımız raporda OBJECT_ID isimli bir parametre alanı vardır bu yüzden FieldName ve Name alanlarını OBJECT_ID olarak giriyoruz
    prms.Add(new ReportServer.rReportParam()
    {                                                           
            Name = "OBJECT_ID",                                    
            Value = ObjectId,                                  
            DataType = "0",                            
            DisplayColumn = "",                  
            FieldName = "OBJECT_ID",                          
            IsLike = false,                                  
            KeyColumn = "",                          
            ListName = "",                            
            TableName = ""                           
    });
    //ExecuteReport sdk metotu oluşan dosyanın datasını döndürür (byte array | byte[])
    var reportData = Server.productivity.rReport.ExecuteReport(reportName, prms.ToArray(), reportType);
    //Rapor datasını diske yazıyoruz. reportData değişkeni byte[] olduğundan paperwork içerisindeki herhangi bir kabinete de kolaylıkla alınabilir.
    File.WriteAllBytes(@"C:\Paperwork\Report.pdf", reportData);

}
catch(Exception ex)
{
    throw ex;
}
```
