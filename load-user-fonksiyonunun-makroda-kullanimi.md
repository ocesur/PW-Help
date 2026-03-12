#### Load User Fonksiyonunun Makroda Kullanımı

LoadUser fonksiyonu metot ve makrolardan çağırılabilmektedir.
Fonksiyonun amacı kullanıcıya ait LOGIN_NAME veya USER_ID bilgisini
parametre vererek kullanıcıya ait tüm bilgileri getirmektir. Bu örnekte
fonksiyonun makroda kullanımı gösterilecektir.

``` {.csharp code-id="section-1687518019882" data-language="csharp"}
try{

    LoadObject();
    //Akışı başlatan kişinin login name bilgisini elde etmek için “OWNER” tip alanından kullanacağımız parametre bilgisini getiriyoruz.
    ObjectName userName = new ObjectName((string) FormData.Get("OWNER")); 
    
    // userName olarak verdiğimiz parametreyi ilgili kullanıcıya ait kullanıcısının USER_ID bilgisini parametre olarak verdiğimizde de aynı dönüş değerlerini alabiliriz.
    a_UserInfo userInfo = Server.productivity.rUser.LoadUser(userName); 
    
    // Kullanıcıya ait ek özellik alanlarında bulunan değerleri de çekebiliyoruz.
    var departmanAdi = (string) userInfo.ExtProp2; 
    
    FormData.Set("DEPARTMAN_ADI",departmanAdi);
    FormData.Set("USER_LOGIN_NAME",userInfo.UserLogin);
    FormData.Set("USER_EMAIL",userInfo.Email);
    FormData.Set("USER_POSITION",userInfo.Position);
    FormData.Set("USER_STATE",userInfo.State);
    FormData.Set("USER_TITLE",userInfo.Title);
    FormData.Set("USER_USERINFO",userInfo.Source);
    FormData.Set("USER_USER_DOMAIN",userInfo.UserDomain);
    FormData.Set("USER_USEROSNAME",userInfo.UserOSName);
    FormData.Set("USER_DESC",userInfo.Description);

    SaveObject();
}
catch(Exception ex){
    throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
}
```

Akış üzerinde hazırladığımız makrodan bir sonra ki manuel aktiviteyi
görüntülediğimizde departman alanı ve diğer alanların tiplere atandığını
görüyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687518053770.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687518062898.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
