#### Makroda Bir Kullanıcıyı Bir Gruba Ekleme

Hazırlanan örneklerde parametreler sabit olarak verilmiştir. Parametre
olarak verilen kullanıcı adı ve grup isimlerini farklı bir alandan
çekecek şekilde de verebilirsiniz. Her iki alanın da parametre veri tipi
string olmalıdır.

``` {.csharp code-id="section-1680243203393" data-language="csharp"}
try{
    var retval = Server.productivity.rUser.AddUserInGroup("aduz", "_PA_Ürün_Müdürleri_01");
    if(retval.ErrorCode != 0){
        Log("kullanıcı grubuna eklenemedi ");
        Log(retval.ErrorCode.ToString());
    }
    else{
        Log("kullanıcı gruba eklendi");
    }
}
catch(Exception ex){
    throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
}
```

#### Makroda Bir Kullanıcıyı Bir Gruptan Çıkarma

``` {.csharp code-id="section-1680243273815" data-language="csharp"}
try{
    var retval = Server.productivity.rUser.RemoveUserFromGoup("aduz", "_PA_Ürün_Müdürleri_01");
    if(retval.ErrorCode != 0){
        Log(retval.ErrorCode.ToString());
    }
    else{
        Log("kullanıcı gruptan çıkarıldı");
    }
}
catch(Exception ex){
    throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
}
```

\

\

\
