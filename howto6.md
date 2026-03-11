Aşağıdaki örnek kod ile makro adımında akış adı oluşturulmuş ve
değiştirilmiştir.

``` {.csharp data-language="csharp"}
try
{
    LoadObject();
    Log("Akış adı belirle makro adımı başladı.");   
    string day        = DateTime.Now.Day.ToString();
    string month      = DateTime.Now.Month.ToString();
    string year       = DateTime.Now.Date.Year.ToString().Substring(2,2); //Buraya kadar olan bölüm günün tarihi alıyor.
    string talep      = (string)FormData.Get("YAZIM"); // Tipteki alan
    //string talepNo    = talep.Length>=4 ? talep.Substring(talep.Length-4) : string.Empty;
     string day2   = day.Length==1 ? "0" + day : day;
    string month2 = month.Length==1 ? "0" + month : month;
    // Bu bölümde de akış adını update ediyor. Dikkat etmeniz gereken akış adı maksimum 255 karakter olabilir. Tek satır olmalı. Çoklu satırı desteklemez.
    string akisAdi = string.Format("{0}{1}{2}-{3}", day2,month2,year,talep);    
    Log("Akış Adı :"+akisAdi);
    string sql=string.Format("UPDATE PW_WORKFLOW SET WORKFLOW_NAME ='{0}' WHERE WORKFLOW_ID='{1}'",akisAdi,WorkflowId);
    a_GenericResult retval = Server.productivity.rAdo.Execute(sql);
    if(retval.ErrorCode != 0)
        Log("WorkflowName güncellenirken hata oluştu");
    else
        Log("WorkflowName başarı ile güncellendi.");

    SaveObject();
}
catch(Exception ex)
{
    Log(string.Format("Hata oluştu:", ex.Message));
    return false;
}
```
