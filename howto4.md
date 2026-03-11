İş Akışı taslağında makro adımında ihtiyaç duyulması halinde aşağıdaki
örnek kod ile vekalet verme işlemi yaptırabilirsiniz.

``` {.csharp data-language="csharp"}
ContentServer.rAttorney info = new ContentServer.rAttorney();

info.FromUser = "ozgenozden";//vekalet veren
info.ToUser = "mehmetyılmaz";// vekalet alan
info.MasterId = prc.MasterId; // vekalet verilecek akış master ıd si
info.LastDate = DateTime.Now.AddDays(2);
info.Info = "AÇIKLAMA";
info.ToUserName = "Mehmet YILMAZ";

a_GenericResult retval = p.rUser.AddAttorney(info);
if (retval.ErrorCode != 0)
{
    throw new Exception(retval.Message);
}
```
