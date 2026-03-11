#### Makroda SAP modülüne Parametre Olarak Tablo Ekleme

Fonksiyonumuzu süreç taslaklarında oluşturduğumuz makro içerisinde
oluşturup daha sonrasında kaydediyoruz. Bu alana gelmeden önce SAP'de
kullanılacak olan fonksiyon bilgini almış olmamız gerekiyor.

``` {.csharp code-id="section-1680245945289" data-language="csharp"}
try{
   SapFields _field = null; // SapFields tipinde bir değişken oluşturuyoruz.
            var fnc1 = Current.Instance.productivity.rIntegration.GetSapFunction("SAP_CUSTOMER_LIST","SAP"); // SAP_CUSTOMER_LIST Sap fonksiyonumuzu çağırıyoruz.
            fnc1.GetElement("IDRANGE").Tables.Clear(); //SAP tablosuna veri eklmeden önce tabloda ki değerleri temizliyoruz.
            _row = new SapTables(); 
            _field = fnc1.GetElement("IDRANGE").GetDetail("SIGN"); // SIGN alanımıza veri ekleyebilmek için çağırıyoruz.
            _field.SetValue("E"); // SIGN alanına verimizi ekliyoruz.
            _row.Detail.Add(new SapTableFields(1, _field)); // indexi 1 olan satırın SIGN verisini ekliyoruz.
            _field = fnc1.GetElement("IDRANGE").GetDetail("OPTION"); // OPTION alanımıza veri ekleyebilmek için çağırıyoruz.
            _field.SetValue("EQ"); // OPTION alanına verimizi ekliyoruz.
            _row.Detail.Add(new SapTableFields(1, _field));  // indexi 1 olan satırın OPTION verisini ekliyoruz.
            _field = fnc1.GetElement("IDRANGE").GetDetail("LOW"); // LOW alanımıza veri ekleyebilmek için çağırıyoruz.
            _field.SetValue("1"); // LOW alanına verimizi ekliyoruz.
            _row.Detail.Add(new SapTableFields(1, _field)); // indexi 1 olan satırın LOW verisini ekliyoruz.
            fnc1.GetElement("IDRANGE").Tables.Add(_row); // SAP'de bulunan IDRANGE alanına tablomuzu ekliyoruz.


            SapFunction sp2 = Current.Instance.productivity.rIntegration.CallSapFunction(fnc1); 
        //SAP tablomuzu eklemek için düzenlemiş olduğumuz fnc1 'i parametre vererek SAP'e istek gönderiyoruz.

            Log("Response xmL : " + sp2.ToXml()); // sonucu XML 'e dönüştürüyoruz.
            SapElements seq = (SapElements)sp2.Elements.Where(x => x.Name.Equals("SONUC")).FirstOrDefault(); // SAP'den gelen SONUC tablosunu değişkenimize tanımlıyoruz.
            row.Set("DURUM_LG",seq.GetDetail("Durum").GetValue().ToString()); // Yaptığımız import işleme ait durum verisini formumuzda bulunan "DURUM_LG" alanına tanımlıyoruz.
            row.Set("MESAH_LG",seq.GetDetail("Mesaj").GetValue().ToString()); // Yaptığımız import işleme ait mesaj verisini formumuzda bulunan "MESAJ_LG" alanına tanımlıyoruz.
}
catch(Exception ex){
    throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
}
```

\
