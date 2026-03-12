Aşağıdaki yazılan metod, makro aktivitesinin bir bölümünde
çağrılmaktadır. Belgenin Orijinali XML formatındaki Elektronik
Faturadır. Elektronik faturanın ara yüzlerde gösterimi için sistem
otomatik olarak belgenin TIF kopyasını oluşturur. Aşağıdaki kod ile bu
TIF belgesi PDF belgesine dönüştürülmüştür.

``` {.csharp code-id="section-1759996945705" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Paperwork.Methods;
using Paperwork.Library;
using Paperwork.Types;
using System.Collections.ObjectModel;

namespace XMLToPdf
{
    public class XMLToPdf : PWRuntimeMethod
    {
        public override string MethodName { get { return "PWMethod-XMLToPdf-V5.0"; } }
        public ObservableCollection<LookupItem> acls = new ObservableCollection<LookupItem>();
        public ObservableCollection<LookupItem> types = new ObservableCollection<LookupItem>();
        public ObservableCollection<LookupItem> forms = new ObservableCollection<LookupItem>();
        public override string Execute(Dictionary<string, object> paramList)
        {
            var retval = base.Execute(paramList);
            try
            {
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);
                Log("Initializing...");
                getDocs();            
            }
            catch (Exception ex)
            {
                retval = ex.Message;
                Log(ex, "Method çalışması sırasında hata oluştu");
            }
            finally
            {
                DisConnectServer();
            }          
            return retval;
        }
   
        public a_GenericResult importNewFile(Stream stream,string file_ext)
        {
            //Eklenecek belgenin nesnesi oluşturulur. Tip bilgisi, Form bilgisi gibi alanlar parametrik olarak alınmıştır.
            //GetDocument metodu ile belirtilen tipten bir nesne oluşturulur ve alanlar doldurularak SetDocument metodu ile kaydedilir.
            acls = server.rLookup.GetACLs(string.Empty);
            types = server.rLookup.GetTypes(string.Empty, string.Empty);
            forms = server.rLookup.GetForms(false, string.Empty);
            string attId = getParam("ATTACHMENT_ID");
            string folderName = getParam("FOLDER_NAME");
            string filename = getParam("FILE_NAME");
            string typeName = getParam("TYPE_NAME");
            string formName = getParam("FORM_NAME");
            string aclName = getParam("ACL_NAME");
            string ext = getParam("EXT");
            string acl_id = getACLByName(aclName).ObjectId;
            string folder_id = getFolderID(attId, folderName);           
            string object_name = Path.GetFileName(filename);
            ITypes fobject = server.rDocument.getDocument(ObjectID.Empty, typeName);
            fobject.Set("ACL_ID", acl_id);
            fobject.Set("OBJECT_TYPE", typeName);
            fobject.Set("FOLDER_ID", folder_id);
            fobject.Set("FORM_NAME", formName);
            fobject.Set("FORM_VERSION", "1");
            fobject.Set("OBJECT_NAME", object_name);
            fobject.Set("FILE_FORMAT", file_ext);
            fobject.Set("IS_FTS", true);
            fobject.Set("IS_VIRTUAL_DOC", true);
            Log("attId " +attId);
            fobject.Set("VIRTUAL_DOC_ID", attId);      
            fobject.Set("VERSION_NUMBER", "1.0");          
            a_GenericResult res = server.rDocument.SetDocument(fobject);
            if (res.ErrorCode != 0)
                throw new Exception(res.Message);       
            //Oluşturulan nesne üzerine belgenin içeriği Import metodu ile eklenir. 
            string obj_id = res.Result;          
            a_GenericResult ires = server.rFile.Import(new ObjectID(obj_id), stream, file_ext, filename + "." + file_ext);
            if (ires.ErrorCode != 0){
                throw new Exception(ires.Message);            
            }
            return res;
        }
        public string getFolderID(string attId, string folderName)
        {
            //ID'si verilen dosya kartı kaydındaki yine adı verilen klasör bulunarak klasörün ID'si alınır. Eklenecek olan yeni belge bu klasörün altına eklenecektir.
            a_Card card = server.rCard.GetCard(new ObjectID(attId), false);
            a_CardSeperator sp = card.CardSeperator;
            return sp.Seperators.Where(x => x.SeperatorName.Value == folderName).FirstOrDefault().SeperatorId.Value;
        }

        public LookupItem getACLByName(string name)
        {
            foreach (LookupItem acl in acls)
                if (acl.Name == name)
                    return acl;
            return null;
        }
       
        public void getDocs()
        {
            try
            {
                //ID'si verilen dosya kartı kaydının klasörüleri dönülerek içinde bulunan XML belgenin PDF kopyası oluşturulur. Burada yapılan işlemler sırası ile şöyledir;
                //1- XML belgenin ön izlemesi olan TIF formatında belge EXPORT edilir.
                //2- TIF formatında export edilen memory stream importNewFile metoduna gönderilerek dosya kartı kaydına TIF dosyasının eklenmesi sağlanır. Bu işlemin amacı
                //GetPdfFile metodunun kullanılması için bizen ObjectID istemesidir.
                //3- Eklenen TIF belgesinin objectId'si GetPdfFile metoduna gönderilerek tekrar mermory stream dönmesini sağlar. Bu MS biz PDF belgesinin contentini verir.
                //4- importNewFile metoduna bu content ile birlikte format bilgisi PDF olarak verilir ve artık PDF belge istenilen klaösre eklenmiş olur.
                //5- Son olarak çevrim yapmak için kullandığımız TIF belgesi silinir. Tercihe bağlıdır istenildiği durumda silinmeyebilir.
                List<string> files = new List<string>();
                a_Card cardData = server.rCard.GetCard(new ObjectID(getParam("ATTACHMENT_ID")), false);
                foreach (a_SeperatorInfo item in cardData.CardSeperator.Seperators)
                {
                    foreach (a_ContentInfo content in item.Contents)
                    {   
                        int err_code=0;
                        string err_msg= "";
                        a_File file = server.rFile.Export(content.ContentId,"T","TIF",out err_code, out err_msg);
                        if (err_code != 0)
                            throw new Exception(err_msg);   
                        MemoryStream stream = new MemoryStream(file.FileData);
                        a_GenericResult res = importNewFile(stream,"TIF");
                        if (res.ErrorCode != 0)
                            throw new Exception(res.Message);   
                        MemoryStream ms = server.rTransfer.GetPdfFile(res.Result);                       
                        importNewFile(ms,"PDF");
                        a_GenericResult rtval = server.rDocument.DeleteDocument(new ObjectID(res.Result), true);
                        if (rtval.ErrorCode != 0)
                            throw new Exception(rtval.Message);                          
                        else
                            Log("CoverSheet dökümanı silindi");                     
                    }
                }
            }
            catch (Exception e)
            {
                throw new Exception(e.Message);
            }
        }
    }
}
```
