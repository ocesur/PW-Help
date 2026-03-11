Akışımızın ekindeki belgeleri \"byte array\" olarak alıp bir takım
işlemler yapmak istersek, dokümanın a_File nesnesini elde etmeliyiz. 

Bunu da aşağıdaki makro kodu ile yapabiliriz. Örnek olarak istenirse,
elde ettiğimiz a_File nesnesinden dokümanı disk üzerinde bir dosya
yoluna, yine aşağıdaki gibi kaydedebiliriz.

``` {.csharp code-id="section-1681285669139" data-language="csharp"}
try
{
   Log(string.Format("Belgelerin dışarı aktarılması makrosu başladı.workflowId : {0} , attachment Id : {1} ",WorkflowId,AttachmentId));
   Log("Kart getiriliyor.");
   a_Card crd = Server.productivity.rCard.GetCard(new ObjectID(AttachmentId), true);
   Log("Kart klasörleri taranıyor.");
   int err_code = 0;
   string err_message = String.Empty;
   foreach (a_SeperatorInfo sepInfo in crd.CardSeperator.Seperators) {
        //Klasörler içerisindeki belgelerin a_File nesnelerini oluşturuyoruz.
        foreach (a_ContentInfo item in sepInfo.Contents) {
            Log("Belge id : " +  item.ContentId.Value);
            Log("Belge Adı : " +  item.ContentName.Value);
            a_File file = Server.productivity.rFile.Export(item.ContentId, string.Empty, string.Empty, out err_code, out err_message);
            if (err_code != 0)
                throw new Exception(err_message);
            else {
                //Burada file.FileData eklentinin byte array halidir.İstenir ise aşağıdaki gibi disk üzerinde bir dosya yoluna aktarımı yapılabilir.
                System.IO.File.WriteAllBytes(string.Format(@"c:\{0}.{1}", item.ContentName.Value, file.OriginalFormat), file.FileData);
            }
        }
    }
}
catch(Exception ex){
  throw new Exception(ex.Message);
}
```
