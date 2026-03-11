#### Makro Aktivitesinde Belge Taslağı ile Doküman Nasıl Oluşturulur?

Normalde bu işlemi doküman yarat aktivitesi zaten otomatik olarak
yapmaktadır. Buradaki örneğin yapılmasının amacı, yaratılacak belgenin
sahibini değiştirebilmektir. Bu şekilde belge üzerinde yetkilendirme
işlemleri belli kullanıcılara göre yapılabilecektir. Doküman yarat
aktivitesinde istenilen bu yetkilendirmelerin yapılamamasının nedeni,
dokümanın sahibinin akış sahibi olarak atanmasıdır. Bu da kullanıcı
bazlı yetkilendirmeye olanak sağlamaz.

Örnek senaryo olarak, bir izin akışı başlattığımızı düşünelim ve bu
akışın içerisinde bir izin belgesi oluşturuyoruz. Bu izin belgesinin
yetkilendirmesini yapmak için bir takım yetki setleri oluşturduk ve
belgeye akış sahibine özel yetki vereceğiz. Oluşturulacak belgeyi de,
yine kişinin bilgilerine göre parametrik bir şekilde oluşturulacak
kabinet dosya yoluna kaydetmek istiyoruz. Bu işlemleri gerçekleştirecek
kodu aşağıda görebilirsiniz.

``` {.javascript code-id="section-1680176722268" data-language="javascript"}
try{

Log("Doküman Yarat Makrosu başladı.");

LoadObject();

//Oluşturulacak belge için yetki seti belirlenir.
string yetkiSetiName = "İzinTalepBelgeleri_"+(string)FormData.Get("OWNER");
Log("yetki seti : " + yetkiSetiName);
a_ACLInfo acll = Server.productivity.rPreset.GetAclByName(yetkiSetiName);
string aclId = string.Empty;
if (string.IsNullOrEmpty(acll.ObjectId.Value)){
    Log("Yetki seti bulunamadı");
}
else {
    Log("yetki seti bulundu.ID : "+ acll.ObjectId.Value);
    aclId = acll.ObjectId.Value;
}

//Belgenin kaydedilmesi için İzin Talep kabineti içerisinde ilgili klasör yolu oluşturulur.
string path = string.Format(@"TR_CABINETS\İzin Talep\{0}\{1}\{2}\{3}",(string)FormData.Get("SIRKETI"),(string)FormData.Get("DEPARTMANI"),(string)FormData.Get("ADI_SOYADI"),(string)FormData.Get("IZIN_TURU"));
Log("path : " + path);
var objList = string.Empty;
//İlgili klasör verilen dosya yolun varsa id’sini getirir.
    var folder = Server.productivity.rNavigation.getFolderPath(path);
    if(folder.ErrorCode != 0){
        Log(folder.Message);
        //İlgili klasör verilen dosya yolunda yoksa oluşturulur.
        folder = Server.productivity.rNavigation.CreateFolderByPath(path, new ObjectID(aclId), false);
        if (folder.ErrorCode != 0) 
            throw new Exception(string.Format("Kabinet yolu yaratılamadı! ") + folder.Message);  
    }else objList = folder.ObjectList[5];
    
//Yaratılması istenen belge için bir nesne oluşturulur ve alanları set edilir.
    ITypes fobject = Server.productivity.rDocument.getDocument(new ObjectID(string.Empty), "T_AT_IZIN_KULLANMA");
    fobject.Set("ACL_ID",           aclId);
    fobject.Set("OBJECT_TYPE", "T_AT_IZIN_KULLANMA");
    fobject.Set("FOLDER_ID", objList);
    fobject.Set("FORM_NAME", "AF_IZIN_KULLANMA");
    fobject.Set("FORM_VERSION", "1");
    fobject.Set("OBJECT_NAME", ((string)FormData.Get("IZIN_TURU"))+"-İzin Kullanım Belgesi");
    fobject.Set("IS_FTS", true);
    fobject.Set("IS_VIRTUAL_DOC", false);
    fobject.Set("VERSION_NUMBER", "1.0");
    fobject.Set("FILE_FORMAT", "DOCX");
    fobject.Set("ADI_SOYADI", (string)FormData.Get("ADI_SOYADI"));
    fobject.Set("DEPARTMANI", (string)FormData.Get("DEPARTMANI"));
    fobject.Set("E_POSTASI",(string) FormData.Get("E_POSTASI"));
    if(FormData.Get("IZIN_BASLANGIC_TARIHI") != null)
        fobject.Set("IZIN_BASLANGIC_TARIHI", (DateTime)FormData.Get("IZIN_BASLANGIC_TARIHI"));
    if(FormData.Get("IZIN_BITIS_TARIHI") != null)
        fobject.Set("IZIN_BITIS_TARIHI", (DateTime)FormData.Get("IZIN_BITIS_TARIHI"));
    
    fobject.Set("IZIN_SEBEBI", (string)FormData.Get("IZIN_SEBEBI"));
    fobject.Set("IZIN_TURU", (string)FormData.Get("IZIN_TURU"));
    fobject.Set("SIRKETI", (string)FormData.Get("SIRKETI"));
    fobject.Set("UNVANI", (string)FormData.Get("UNVANI"));
    a_GenericResult res = Server.productivity.rDocument.SetDocument(fobject);
     if(res.ErrorCode != 0)
        throw new Exception("Belge oluşturulamadı.Hata : "+ res.Message);


    //İlgili belgeye atanacak belge taslağının id'ne ulaşılır.
    string templatename="İzin Kullanım Belgesi";
    string templateId = string.Empty;

    List<a_Template> templates = server.rLookup.GetTemplates("BT Yazılım");
    if(templates.Count == 0)
                    throw new Exception("Belge taslağı bulunamadı.");

    foreach (a_Template item in templates) {
        TemplateId = item.ObjectId ;
       Log("Nesne numarası:{0}, Adı:{0} " , item.ObjectId, item.TemplateName);
    }


    //Oluşturulan nesneye bir taslak atanır.
    a_GenericResult ress = Server.productivity.rFile.setTemplateAsContent(new ObjectID(res.Result),new ObjectID(templateId));
    if(ress.ErrorCode != 0)
        throw new Exception(ress.Message);
    Log("ress.Result " +ress.Result);
          
SaveObject();
Log("Doküman Yarat Makrosu bitti.");


}catch(Exception ex){
    throw new Exception("Doküman Yarat Makrosu hatası : " + ex.Message);
}
```

\
