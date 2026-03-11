Makroda grup yaratma örneği, grup oluştuktan sonra "CreateGroup"
fonksiyonundan çalışma işlemi başarılı ise yaratılan gruba ait nesne
numara bilgisi gelmektedir. Bu nesne numarasını kullanarak daha
sonrasında kullanıcı grubuna kullanıcı ekleme/çıkarma işlemleri
yapılabilmektedir.

Not : Aynı isime sahip iki kullanıcı grubu olamaz ve oluşturulamaz. Aynı
isimde bir kullanıcı grubu var ise fonksiyon hata verecektir.

``` {.csharp code-id="section-1695639685509" data-language="csharp"}
try
{
    Log("Grup oluşturma makrosu çalışmaya başladı! ");
    var group = new a_GroupInfo(); //a_GroupInfo tipinde yeni bir değişken oluşturuyoruz.
    group.ObjectId    = ObjectID.Empty;
    group.GroupName   = new ObjectName("Test Anil11"); //grup ismi özeldir ve aynı grup ismine sahip farklı bir grup varsa hata alacaktır.
    group.Email       = "testuser@mycorp.net"; 
    group.Description = "test group"; //grup açıklama alanı
    group.IsPrivate   = false;
    group.Owner       = string.Empty;
    group.Domain      = string.Empty;
    group.Source      = string.Empty;
    group.Members     = new List<a_UserGroup>();
    var retval = Server.productivity.rUser.CreateGroup(group); //CreateGroup fonksiyonuna "group" nesnesini parametre vererek çağırıyoruz.
    if (retval.ErrorCode != 0)
        throw new Exception(retval.Message);
    else{
        string group_id = retval.Result.ToString(); //yaratılan grubun nesne numarası "result" içerisinde bilgi olarak bize geliyor.
        
        Log(string.Format("Grup nesne numarası :{0}", group_id));
    }

    Log("Grup oluşturma makrosu çalışmayı başarıyla sonlandırdı! ");
}
catch(Exception ex)
{
    throw new Exception(string.Format("makro çalışırken hata oluştu. Hata: {1} ", ex.Message));
}
```
