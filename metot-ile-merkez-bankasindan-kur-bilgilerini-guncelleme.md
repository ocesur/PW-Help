#### Metot ile Merkez Bankasından Kur Bilgilerini Güncelleme

Bir metot tanımı içerisinde iletilen C# kod örneğinin ana class
tarafından çağrılması ile birlikte kullanımı yapılabilir. Ancak
öncesinde kod içerisinde de belirtildiği üzere, ilk olarak verilerin
ekleneceği database tablosunun oluşturulması gerekmektedir.

Kod örneğimiz şu şekildedir :

``` {.csharp code-id="section-1699860376768" data-language="csharp"}
public void KurBilgiInsert()
{
    const string bugun = "https://www.tcmb.gov.tr/kurlar/today.xml"; //Merkez bankasının günlük güncellediği xml
    const string tableName = "TCMB_KUR"; //Database üzerisinde güncelleyeceğimiz tablo

    //XmlDocument nesnemizi oluşturuyoruz.
    var cxml = new XmlDocument();
    cxml.Load(bugun); //xml linkimizi nesneye yüklüyoruz.

    string usd_satis = cxml.SelectSingleNode("Tarih_Date/Currency [@Kod ='USD'] / ForexSelling").InnerXml; //Dolar Döviz Satış değeri
    Log("usd_satis: " + usd_satis);
        
    string eur_satis = cxml.SelectSingleNode("Tarih_Date/Currency [@Kod ='EUR'] / ForexSelling").InnerXml; //Euro Döviz Satış değeri
    Log("eur_satis: " + eur_satis);

    //Database Insert query için stringBuilgder tanımlıyoruz.
    StringBuilder insertQuery = new StringBuilder();
    insertQuery.Append("INSERT INTO ");
    insertQuery.Append(tableName);
    insertQuery.Append(" (USD, EUR, KUR_TARIHI) "); //Örnek tablomuzda 3 adet kolon bulunuyor.Bunlar USD, EUR, KUR_TARIHI
    insertQuery.AppendFormat(" VALUES ({0}, {1}, GETDATE()) ", usd_satis, eur_satis); //Değerler sırası ile atanıyor
    Log("Insert Q: " + insertQuery); //Çalıştırılacak insert query log basarak takibimizi yapıyoruz.

    //rAdo altında insert, update gibi sorguları çalıştırmamız için Execute sdk fonksiyonunu kullanıyoruz.
    a_GenericResult updRes = server.rAdo.Execute(insertQuery);
    if (updRes.ErrorCode != 0)
        throw new Exception("Update sırasında Hata " + updRes.Message); //Sorgu çalıştırılırken hata alındığında hata uyarısı vermesi için
    else
        Log("Kurlar güncellendi."); //Başarılı şekilde çalıştırıldığında log dosyalarında kayıt için
}
```
