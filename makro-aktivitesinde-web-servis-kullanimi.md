``` {.csharp code-id="section-1763374265022" data-language="csharp"}
   // Makro içerisinde  Web servis kullanımı

    Log("Başladı...");
    List<Param> webInputs= new  List<Param>();

    var tList = new List<object>();

    tList.Add(new { Adi="test", Uzantisi ="PNG" , Data = "dGVzdA==" });

    dynamic destek = new
    {
        DestekTalepEden = "skul",
        DestekTalepKonu = "Test",
        DestekTalepAciklama = "test ediliyor",
        DestekTalepEposta = "skul@paperwork.com.tr",
        Ekler = tList.ToArray()
    };

    var ser = JsonConvert.SerializeObject(destek);

    Log("Nesne : " + ser);

    webInputs.Add(new Param(){ParamName="destek",ParamValue= ser});

    dynamic ServiceResult = JsonConvert.DeserializeObject(CallMvc("HARS_CONNECT", "ReservationCars", webInputs, ref Message));

    Log("Message :" + Message);

    if(ServiceResult==null)
        throw new Exception(Message);

    Log("Res :" + JsonConvert.SerializeObject(ServiceResult));

    if(ServiceResult.ErrorCode == 0)
        FormData.Set("CODE",ServiceResult.Result);
    else
        FormData.Set("MESSAGE",ServiceResult.Message);
```
