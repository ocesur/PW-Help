#### Hata Takibini Nasıl Yaparım?

Metod tanımlama ekranında metodların hata alması durumunda elektronik
posta göndermesi istenilebilir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1644482574995.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable}

Yukarıdaki ekranda bulunan iş tanımında \"Her durumda bilgi ver\"
seçeneği ile metod her çalıştırıldığında elektronik posta ile uyarı
gönderilir. Bu seçenek işaretlenmez ise sadece hata alındığında
elektronik posta gönderilir. Elektronik posta içerisinde metodun aldığı
exception yazılır. Bunun yazılabilmesi için aşağıdaki kod örneğinde
olduğu gibi **ErrorMessage **değeri uygun şekilde doldurumlalıdır.

``` {.csharp code-id="section-1657806230992" data-language="csharp"}
try
{
   throw new Exception("Hata mesajını doldur");
   return 0;
}
catch (Exception e)
{   
   Log(e.Message);//Metod server loglarına hatanın yazılmasını sağlar
   ErrorMessage=e.Message;//elektronik postada hatanın bulunmasını sağlar
   return -1;
}
finally
{
}
```

#### Organizasyon Şeması senkronizasyonunu nasıl yaparım?

[Şu
sayfada](/tr/docs/organizasyon-semas%C4%B1-senkronizasyonu){rel="nofollow"
translate="no"} metod yardımı ile dış sistemlerden alınan organizasyon
şemasının nasıl senkroniza edilebileceği gösterilmiştir.

\

#### Metot ile bir akışı nasıl başlatırım?

Aşağıdaki örnek kod ile akış başlatmak mümkündür.

``` {.csharp code-id="section-1657806230994" data-language="csharp"}
rProcessInfo[] processes = p.rWorkflow.GetProcesses(2).Items; //Akış başlatılabilecek durumda olan process lerin listesi alınır.
            rProcessInfo prc = processes.FirstOrDefault(j =>
                                     j.ProcessName == "MUSTERI_FATURA");// Process name bilgisi verilerek başlatılacak akışın datası filtrelenir.
            if (prc == null)
                throw new Exception("Akış bulunamadı");

            rWorkflow wi = new rWorkflow(); // rWorkflow türünde yeni bir nesne üretilir.
            wi.AclId = prc.AclId; // Processin yetki seti alınarak rWorkflow türünde üretilen nesneye set edilir.
            wi.AttachmentId = string.Empty; // Eklenti yok ise boş geçilir.
            wi.ObjectId = "";// Boş geçilir. Sebebi ise daha akış başlamadığı için object id üretilmez. Başladıktan sonra bu alan otomatik dolacaktır.
            wi.ContentType = WorkItemContentTYPE.NoContent.ToString();// Content type alanı akış için 0 olarak bu şekilde tanımlanır. Not : Form = 1,Card=2
            wi.FormName = prc.FormName; // Processin form bilgisi alınarak rWorkflow türünde üretilen nesneye set edilir.
            wi.FormVersion = "1";// sabit 1 verilir.
            wi.State = WORKFLOWState.Init.ToString();// Akışın başlangıç state i 0 verilir. Bu şekilde tanımlamanız bunu ifade eder.
            wi.TypeName = prc.ObjectType;// Processin type bilgisi alınarak rWorkflow türünde üretilen nesneye set edilir.
            wi.Version = string.Empty;// Akış başladığında sistem otomatik set edecektir.
            wi.Owner = Definitions.SUPERUSER;// akışı başlatacak kullanıcının Login Name bilgisi yazılır.
            wi.ProcessId = prc.ProcessId;// Processin process id bilgisi alınarak rWorkflow türünde üretilen nesneye set edilir.
            wi.Priority = 0;// Akış önceliği set edilir. 0=>Düşük,1=>Normal,2=>yüksek,3=>Çok yüksek,-1=>Yok
            wi.WorkflowName = "KART_TANIMLAMA";//Akış adı dinamik oluşturulur.
            wi.WorkflowDesc = "Talep Başlatıldı.";//Açıklaması dinamik oluşturulur.
            wi.Tag = DateTime.Now.ToString("s");//Doldurulması zorunlu değildir. Data tutar.

            ITypes fObject = p.rDocument.getDocument(new ObjectID(string.Empty), prc.ObjectType);//Oluşturulan akış için bir akış nesnesi oluşturulur. İlk parametresi boş gönderilerek yeni bir nesne oluşturulur.İkinci parametredeki belirtilen tipe göre yeni bir nesne oluşturmuş oluruz.
            fObject.Set("SIRKET","GGSOFT");//Oluşturulan nesne için bağlı olduğu tip içindeki alanlara erişerek değerleri bu şekilde doldurulur.

            PW_SYSOBJECT sObject = fObject as PW_SYSOBJECT;//Sysobject tipinde sistem tanımlarını girmek için bir nesne oluşturulur.
            sObject.FORM_NAME = wi.FormName;// Akış için oluşturduğumuz nesne üzerinden form bilgisi girilir.
            sObject.FORM_VERSION = wi.FormVersion;// Akış için oluşturduğumuz nesne üzerinden form bilgisi girilir.
            sObject.OBJECT_NAME = wi.WorkflowName;// Akış için oluşturduğumuz nesne üzerinden akış bilgisi girilir. Bu alana isteniler herhangi bir değer girilebilir.
            sObject.ACL_ID = wi.AclId;// Akış için oluşturduğumuz nesne üzerinden yetki seti bilgisi girilir.
            sObject.OWNER = Definitions.SUPERUSER;// Login Name bilgisi girilmelidir. Mantıklı olan akışı başlatan kişinin girilmesi.
            sObject.FOLDER_ID = DefaultObjects.WorkflowDir;// Sabit olarak bu değer girilmeli. 
            sObject.OBJECT_TYPE = wi.TypeName;// Akış için oluşturduğumuz nesne üzerinden type bilgisi girilir.
            sObject.CONTENT_TYPE = Definitions.CONTENT_TYPE_FLOW;//Content type olarak FLOW değeri set edilmesi için bu ifade kullanılır.
            sObject.VIRTUAL_DOC_ID = string.Empty;//DK Eklentisi olmadığı için boş geçilmektedir.
            sObject.IS_FTS = true;//FTS e girmesi için true gönderilmeli.
            sObject.IS_VIRTUAL_DOC = false;//DK Eklentisi olmadığı için boş geçilmektedir.
            sObject.IS_LAST_VERSION = true;//Son versiyonda kullanılması için true girilmesi gerekmektedir.

            a_GenericResult gr = p.rWorkflow.CreateWorkflow(wi, fObject, "F");//Yukarıdaki nesneler kullanılarak akış başlatılır.
            if (gr.ErrorCode != 0)
                Console.WriteLine("hata : " + gr.Message);
```

#### Metodlarda Dinamik Olarak Dosya Kartı Yolu ve Dosya Kartı Oluşturma

Dosya kartını belirteceğimiz yol ile dinamik olarak oluşturmak istersek
bunu "CreateFolderByPath" ve "CreateCardByPath" fonksiyonları ile
yapabiliriz :

``` {.javascript code-id="section-1680174574257" data-language="javascript"}
public a_PathInfo CreateFolderByPath(string _path) // Verilen yoldaki klasörler yoksa belirtilen yoldaki klasörleri oluşturan fonksiyon.
    {
        ObservableCollection<LookupItem> acls = server.rLookup.GetACLs("Default ACL"); // Adı verilen yetki setini getirir.
        if (acls.Count < 0) // Yetki setinin bulunduğuna dair kontrol.
            throw new Exception("Yetkiseti bulunamadı");
        ObjectID aclId = new ObjectID(acls[0].ObjectId); // Yetki setinin Id' sini alır.
        a_PathInfo pi = server.rNavigation.CreateFolderByPath(_path, aclId, false); // Verilen yoldaki klasörler yoksa belirtilen yoldaki klasörleri oluşturur.
        
        if (pi.ErrorCode != 0) // Oluşturumasına dair hata kontrolü yapılır.
            throw new Exception(string.Format("Kabinet yolu yaratılamadı!"));
        return pi; // Oluşturulan yolun bilgisini döner.
    }
    public a_GenericResult CreateCardByPath()
    {
        ObservableCollection<LookupItem> acls = server.rLookup.GetACLs("Default ACL"); // Adı verilen yetki setini getirir.
        if (acls.Count < 0) // Yetki setinin bulunduğuna dair kontrol.
            throw new Exception("Yetkiseti bulunamadı");
        string aclId = acls[0].ObjectId; // Yetki setinin Id' sini alır.
        string path = string.Format(@"TR_CABINETS\{0}\{1}\{2}","Kullanıcılar",DateTime.Now.Year,DateTime.Now.Month); // Oluşturulacak olan yol belirlenir.
        ObservableCollection<LookupItem> Cards = server.rLookup.GetFileCards(); // Dosya kartları çekilir.
        LookupItem template = new LookupItem();
        foreach (LookupItem item in Cards)
        {
            if (item.Title == "Kullanıcı Bilgileri") // "Kullanıcı Bilgileri" olan dosya kartının  alınması sağlanır.
            {
                template = item;
                break;
            }
        }
        
        a_PathInfo pathInfo = CreateFolderByPath(path); // "CreateFolderByPath" fonksiyonu ile verilen yoldaki klasörler yoksa klasörlerin oluşturulması sağlanır. 
        string id = pathInfo.ObjectList[pathInfo.ObjectList.Count - 1]; // Son belirtilen klasörün Id' si alınır.
        if (pathInfo.ErrorCode != 0) // ErrorCode 0 ise işlem başarıyla gerçekleşmiştir.
            throw new Exception(pathInfo.Message);
        a_GenericResult retval = server.rCard.CreateCardByPath(new ObjectID(template.ObjectId), new ObjectName("Kullanıcı Dosya Kartı"), id, aclId); // Verilen dosya kartının Id'si, Dosya kartı adı, Klasör Id'si ve Yetki Seti Id' sine göre ilgili klasöre dosya kartını oluşturur.
        
        Log("Dosya kartı kaydı nesne numarası:{0}", retval.Result); // "retval.Result" oluşturulan dosya kartı kaydının nesne numarasını tutar.
        if (retval.ErrorCode != 0) // ErrorCode 0 ise işlem başarıyla gerçekleşmiştir.
            throw new Exception(retval.Message);
        else
            Log("Dosya kartı kaydedildi.");
        return retval;
    }
```

\

#### Metot ile Doküman İsmini Güncelleme

Belirli bir belgenin ismini değiştirmek için renamedocument fonksiyonunu
kullanabiliriz. Belgenin ObjectID değerini biliyorsak şu şekilde
yapabiliriz.

``` {.javascript code-id="section-1680179585600" data-language="javascript"}
public void RenameDoc(){
    string guncelDocIsmi = "Güncel Document İsmi";  //Belgenin yeni ismini string bir değer olarak alıyoruz.
    Log("Güncel İsim: " + guncelDocIsmi);
    ObjectName objectName = new ObjectName(guncelDocIsmi); // Elimizde ki string belge ismi ile bir ObjectName oluşturuyoruz.
    ObjectID oid = new ObjectID("FF000100000C20BD"); // İsmini değiştireceğimiz belgenin ObjectId değeri ile bir ObjectID oluşturuyoruz.
    /*RenameDocument fonksiyonunun 2 tane parametresi mevcut. Bunlar;
    1-objectId
        Type: ObjectID
        -Doküman nesne numarası
    1-newName
        Type: ObjectName
        -Yeni ad 
    */
    a_GenericResult renamedocument = server.rDocument.RenameDocument(oid, objectName); //Parametreleri burada fonksiyonumuza veriyoruz. 
    /*
    Return Value
        Type: a_GenericResult
        a_GenericResult nesesi içinde , ErrorCode=0 ise işlem başarılıdır. Aksi taktirde Result ve Message alanları kontrol ediniz.
    */
    if (renamedocument.ErrorCode != 0)
        throw new Exception("Belge ismi güncellenirken hata oluştu. ObjectId:" + oid + " Hata nedeni: " + renamedocument.Message);
}
```

#### Metot ile Doküman Silme

Belirli bir belgenin ObjectID değeri üzerisinden silme işlemi için
DeleteDocument fonksiyonunu kullanabiliriz. [Belgenin ObjectID değerini
biliyorsak şu şekilde
yapabiliriz.]{style="color: rgb(34, 34, 34); font-family: Nunito, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: 0.48px; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"} 

``` {.javascript code-id="section-1680180064940" data-language="javascript"}
public void DeleteDocumentExample(){
    ObjectID oid = new ObjectID("FF000100000C18E2");// Silinmek istenen belgenin ObjectId değeri ile bir ObjectID oluşturuyoruz.
    /*
    DeleteDocument fonksiyonunun zorunlu 2 tane parametresi mevcut. Bunlar;
    1-objectId
        Type: ObjectID
        Silinecek dokümanın nesne numarası. 
    2-allVersion
        Type: System.Boolean
        true : Dokümanın var ise eski versiyonları da silinir.
        false : Son versiyon silinir. Ondan önceki versiyon son versiyon olur.  
    */
    a_GenericResult retval = server.rDocument.DeleteDocument(oid, true);//Parametreleri burada fonksiyonumuza veriyoruz. 
    /*
    Return Value
        Type: a_GenericResult
        a_GenericResult nesesi içinde , ErrorCode=0 ise işlem başarılıdır. Aksi taktirde Result ve Message alanları kontrol ediniz.
    */
    if (retval.ErrorCode != 0)
        throw new Exception("Belge silinirken hata oluştu. Hata mesajı: " +  retval.Message);
}
```

#### Metot ile Nesne Taşıma

Bir nesneyi başka bir klasör altına taşınmas işlemi için MoveObject
fonksiyonu tercih edilebilir. Taşıyacağımız belgenin ve taşınmak
istenilen klasörün ObjectID değerlerini biliyorsak şu şekilde
yapabiliriz.

``` {.javascript code-id="section-1680180189050" data-language="javascript"}
public void MoveObjectExample(){
    ObjectID folderId = new ObjectID("FF000100000C227F"); // Hedef klasörün ObjectId değeri ile bir ObjectID oluşturuyoruz.
    ObjectID objectId = new ObjectID("FF000100000C20BD"); // Taşıyacağımız belgenin ObjectId değeri ile bir ObjectID oluşturuyoruz.
    int copy_type = 1; // Yapacağımız işlemi belirtiyoruz. Burada taşıma işlemi yapılacağı için 1 değerini veriyoruz.
    /*
    MoveObject fonksiyonunun zorunlu 3 tane parametresi mevcut. Bunlar;
    1-objectId
        Type: ObjectID
        Taşınacak nesnenin nesne numarası. 
    2-folderId
        Type: ObjectID
        Nesnenin taşınacağı klasör numarası. 
    3-copyType
        Type: System.Int32
        Kopyalama türü (copy=0, move=1)
    */
    a_GenericResult retval = server.rNavigation.MoveObject(objectId, folderId, copy_type);//Parametreleri burada fonksiyonumuza veriyoruz. 
    /*
    Return Value
        Type: a_GenericResult
        a_GenericResult nesesi içinde , ErrorCode=0 ise işlem başarılıdır. Aksi taktirde Result ve Message alanları kontrol ediniz.
    */
    if (retval.ErrorCode != 0)
        throw new Exception("Yetki seti değiştirilemedi. Hata mesajı: " +  retval.Message);
}
```

#### Metot ile Nesne Yetki Seti Güncelleme

Yetki setinin adını yada ObjectID değeri ile bir belgenin yetki setini
güncellemek için UpdateObjectAcl fonksiyonunu kullanabiliriz. Aşağıda
ise iki farklı kullanımı verilmiştir.

``` {.javascript code-id="section-1680180288977" data-language="javascript"}
public void UpdateObjectAclExample()
{
    ObjectID objId = new ObjectID("FF000100000C20BD"); // Yetki setini değiştireceğimiz belgenin ObjectId değeri ile bir ObjectID oluşturuyoruz.
    ObservableCollection<LookupItem> acls = server.rLookup.GetACLs("Default ACL"); // Yeni yetki setinin ismi ile filtreleme yaparak yetki setlerini alıyoruz.
    if (acls.Count < 0) //Eğer yetki seti bulunamaz ise çalışmayı durdurup hata basıyoruz.
        throw new Exception("Yetkiseti bulunamadı"); 
    
    string aclId = acls[0].ObjectId; //Yetki seti bulunduysa filtreden dönen ilk yetki setinin ObjectId değerini alıyoruz ve bir string'e atıyoruz.
    /*UpdateObjectAcl fonksiyonunun zorunlu 2 tane parametresi mevcut. Bunlar;
    1-objectId
        Type: ObjectID
        -Değiştirilecek doküman nesne numarası
    2-newAclId
        Type: System.String
        -Yeni ACL nesne numarası
    3-byName (Optional)
        Type: System.Boolean
        True ise ismiyle günceller (varsayılan : False)
    */
    a_GenericResult retval = server.rDocument.UpdateObjectAcl(objId , aclId); //Parametreleri burada fonksiyonumuza veriyoruz. 
    /*
    Return Value
        Type: a_GenericResult
        a_GenericResult nesesi içinde , ErrorCode=0 ise işlem başarılıdır. Aksi taktirde Result ve Message alanları kontrol ediniz.
    */
    if (retval.ErrorCode != 0)
        throw new Exception("Yetki seti değiştirilemedi. Hata mesajı: " +  retval.Message);
    
    /*
    Eğer yetki seti isminin başka bir yetki setinin ismini içermediğinden emin ise 3. parametreyi "true" değeri vererek yetki setinin ObjectID değerini bulmamıza gerek kalmaz.
    Bu sayede 2. Parametre yerine yetki setimizin ismini yazarak işlemimizi tamamlayabiliriz. Bunun kullanımı ise aşağıda verilmiştir.
    */
    a_GenericResult retval2 = server.rDocument.UpdateObjectAcl(objId, "Default ACL",true); 
    if (retval2.ErrorCode != 0)
        throw new Exception("Yetki seti değiştirilemedi. Hata mesajı: " +  retval2.Message);
}
```

#### Metot ile Çoklu Doküman Silme

Belirli birden fazla belgenin silinme işlemi için  DeleteDocuments
fonksiyonu tercih edilebilir. Eğer silinmesi istenen belgelerin ObjectID
değerlerini biliyorsak şu şekilde yapabiliriz.

``` {.javascript code-id="section-1680180373969" data-language="javascript"}
public void DeleteDocumentsExample(){
    ObservableCollection<KeyPairItem> ids = new ObservableCollection<KeyPairItem>(); // Silinmesi gereken belgelerin ObjectId değerlerini burada listemize ekliyoruz.
    ids.Add(new KeyPairItem() { ID = "FF000100000C2280" });
    ids.Add(new KeyPairItem() { ID = "FF000100000C2281" });
    ids.Add(new KeyPairItem() { ID = "FF000100000C2282" });
    /*
    DeleteDocuments fonksiyonunun zorunlu 2 tane parametresi mevcut. Bunlar;
    1-objectlist
        Type: System.Collections.ObjectModel.ObservableCollection<KeyPairItem>
        Silinecek dokumanların nesne numaralarını tutar.
    2-allVersion
        Type: System.Boolean
        true : Dokümanın var ise eski versiyonları da silinir.
        false : Son versiyon silinir. Ondan önceki versiyon son versiyon olur.  
    */
    a_GenericResult retval = server.rDocument.DeleteDocuments(ids , true);//Parametreleri burada fonksiyonumuza veriyoruz. 
    /*
    Return Value
        Type: a_GenericResult
        a_GenericResult nesesi içinde , ErrorCode=0 ise işlem başarılıdır. Aksi taktirde Result ve Message alanları kontrol ediniz.
    */
    if (retval.ErrorCode != 0)
        throw new Exception("Belgeler silinirken hata oluştu. Hata mesajı: " +  retval.Message);
}
```

#### Metot ile Hataya Düşen/Eksik Çalışmış Akışları Tekrar Çalıştırma

Belirli bir durum ve zaman aralığında bulunan iş akışlarını kontrol
etmek ve kriterlere uyan iş adımlarını tekrar çalıştırmak için
ReRunWorkItems fonksiyonunu kullanabiliriz. Hatalı veya eksik çalışmış
iş adımlarını yeniden tetikleme işlemini şu şekilde yapabiliriz.

``` {.csharp code-id="section-1735044477538" data-language="csharp"}
using Paperwork.Library;
using Paperwork.Methods;
using Paperwork.Connect;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data;

namespace ReRunWorkItems
{
    /// <summary>
    /// Bu metod, "ReRunWorkItems" adında, belirli bir zaman aralığında belirlenen kriterlere uyan iş akışlarını tekrar çalıştırmaktadır.
    /// Sunucu bağlantısı kurar, iş akışlarıyla ilgili SQL sorgularını çalıştırır ve sonuçlara göre iş adımlarını tetikler.
    /// </summary>
    public class ReRunWorkItems : PWMethod
    {
        public override string MethodName { get { return "PWMethod-ReRunWorkItems-V5.1"; } }

        /// <summary>
        /// Ana çalışma metodudur. Parametreleri alır, sunucu bağlantısını kurar, gerekli işlemleri yapar ve sonuçları raporlar.
        /// </summary>
        /// <param name="paramList">Metoda gönderilen parametreler</param>
        /// <returns>0 başarıyla tamamlandığını, -1 hata olduğunu belirtir.</returns>
        public override int Execute(Dictionary<string, object> paramList)
        {
Log("{0} started...", MethodName);
            var retval = base.Execute(paramList);
            string msg = string.Empty;

            try
            {
                // Sunucu bağlantısı kurulur
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);

                // İş akışlarını tekrardan tetiklemek için ana metod çağrılır
                InternalExecute();

                msg = string.Format("{0} finished... {1}", MethodName, DateTime.Now);
                Log(msg);
            }
            catch (Exception ex)
            {
                retval = -1;
                msg = string.Format("{0} Ex: {1}", MethodName, ex.Message);
                Log(msg);
            }
            finally
            {
                try
                {
                    // İşlem sonucu raporlanır ve bağlantı kesilir
                    if (server == null)
                        Log("Productivity Layer connection was fail");
                    else
                        server.rIntegration.ReportDetail(MethodName, retval == -1 ? false : true, msg);

                    DisConnectServer();
                }
                catch (Exception ex)
                {
                    Log("ReRunWorkItems Disconnect Ex :", ex);
                }
            }

            return retval;
        }

        /// <summary>
        /// İş akışlarını kontrol edip, belirtilen kriterlere uyan iş adımlarını tekrar çalıştıran metod.
        /// </summary>
        private void InternalExecute()
        {
            try
            {
                // İş akışlarını sorgulayan SQL komutu
                // Son 3 gün için bir kontrol yapılmıştır
                string sql = "SELECT WORKFLOW_ID, LAST_ACTION_DATE FROM PW_WORKFLOW(NOLOCK) WHERE STATE = 18 AND LAST_ACTION_DATE > DATEADD(day, -3, CONVERT(date, GETDATE()))";
                using (DataSet dts = server.rAdo.Query(sql, -1))
                {
                    if (dts != null && dts.Tables.Count > 0 && dts.Tables[0].Rows.Count > 0)
                    {
                        foreach (DataRow row in dts.Tables[0].Rows)
                        {
                            Log("wfId: " + row["WORKFLOW_ID"]);

                            // İş adımlarını sorgulayan SQL komutu
                            // RUNTIME_STATE değeri 3 ise başarılı, 4 ise hatalı olarak kaydedilmektedir.
                            sql = string.Format("SELECT TOP 1 WORKITEM_ID, CREATE_DATE FROM PW_WORKITEM(NOLOCK) WHERE ACT_TYPE = 'Macro' AND RUNTIME_STATE = 4 AND WORKFLOW_ID = '{0}' AND CREATE_DATE > DATEADD(day, -3, CONVERT(date, GETDATE()))", row["WORKFLOW_ID"].ToString());
                            /*
                            ACT_TYPE olarak farklı aktivite isimleri de kullanılabilir. Hata kontrolünde genelde şu aktiviteler seçilir:
                            Macro, ManualProcess, SAPModule, SendMail
                            */
                            using (DataSet dts2 = server.rAdo.Query(sql, -1))
                            {
                                if (dts2 != null && dts2.Tables.Count > 0 && dts2.Tables[0].Rows.Count > 0)
                                {
                                    string workitemId = dts2.Tables[0].Rows[0]["WORKITEM_ID"].ToString();
                                    string createDate = dts2.Tables[0].Rows[0]["CREATE_DATE"].ToString();
                                    DateTime dt = Convert.ToDateTime(createDate);
                                    createDate = dt.ToString("MM-dd-yyyy HH:mm:ss");

                                    // Kontrol sorgusu
                                    // Burada yapılan kontrolün amacı şu şekildedir; Eğer bu tetiklenen aktivite daha öncesinde 3 ya da daha fazla tetiklendiyse bir daha tetiklenmemesinin kontrolü
                                    string sqlKontrol = "SELECT WORKITEM_ID FROM PW_WORKITEM(NOLOCK) WHERE ";
                                    sqlKontrol += string.Format(" CREATE_DATE > '{0}' AND CREATE_DATE < GETDATE() ", createDate);
                                    sqlKontrol += string.Format(" AND ACTIVITY_ID = 'AA000000000FFFEC' AND WORKFLOW_ID = '{0}'", row["WORKFLOW_ID"].ToString());
                                    //Kontrol edilen ACTIVITY_ID değeri sistemde sabit tanımlı olan ve bir aktivite tekrardan çalıştığında oluşan kayıttır. 
                                    DataSet dtsKontrol = server.rAdo.Query(sqlKontrol, -1);

                                    if (dtsKontrol.Tables[0].Rows.Count < 3)
                                    {
                                        // İş adımı tekrar çalıştırılır
                                        var retval = server.rWorkflow.RerunWorkitem(workitemId);
                                        Log("res: " + retval.Result.ToString());

                                        if (retval.ErrorCode != 0)
                                            throw new Exception(retval.Message);
                                        else
                                            Log(workitemId + " Tekrardan Tetiklendi");
                                    }
                                    else
                                    {
                                        Log("Aktivite 3 kere tetiklenmiştir. WorkflowId: " + row["WORKFLOW_ID"].ToString());
                                    }
                                }
                            }
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                throw ex;
            }
        }
    }
}
```
