Makro aktivitesinde akış ekinde bulunan dosya kartı kaydına bağlı
klasörlerin ve bu klasörler içindeki belgelerin Müşteri Kodu değerine
göre belirlenen kabinet altında müşteri kodunun 2 basamaklı değerine
göre alt klasörlerin oluşturulması ve en son klasörün müşteri kodunun
tamamıyla oluşturulan bir klasör içerisinde belgelerin dosya kartında
bulundukları klasörlerle beraber taşıması işlemini gerçekleştirilecek
kod örneği aşağıda paylaşılacaktır. 

\

Senaryomuz gereği Müşteri kodumuz 0654321 olsun.

\

Dosya Kartında bu müşteri numarasına ait iki adet belge olsun. Dosya
Kartında birinci belge Resmi Belgeler isimli klasörde diğeri de
Yazışmalar isimli klasör içinde bulunsun.

\

Hedef Kabinet ismi \"Müşteri\" olarak belirlendi.

\

Makro çalıştığında belgeler Müşteri Kabineti içerisinde aşağıdaki gibi
görülecektir. 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1639396279468.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-draggable style="width: 824px;"}

[Bu işlemi gerçekleştiren kod aşağıdaki
gibidir.]{style="color: rgb(51, 51, 51); font-family: \"Helvetica Neue\", Helvetica, Arial, sans-serif; font-size: 13px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"} 

``` {.csharp code-id="section-1741696829954" data-language="csharp"}
try
{
   Log(string.Format("Belgelerin kabinetlere dağılması makrosu başladı.workflowId : {0} , attachment Id : {1} ",WorkflowId,AttachmentId));
   LoadObject();
   LoadAttachment();
   Log("Kart getiriliyor.");
   Log("object ıd : " + (string)AttachmentData.getAttribute("OBJECT_ID"));
   a_Card card2 = Server.productivity.rCard.GetCard(new ObjectID((string)AttachmentData.Get("OBJECT_ID")), true);
   Log("1");
   ObjectID obid;
   Log("object id : " + (string)AttachmentData.getAttribute("OBJECT_ID"));
   string targetPath = string.Empty;
   string customerID = string.Empty;
   Log("Kart bilgileri alınıyor.");
      
   foreach (a_SeperatorInfo item in card2.CardSeperator.Seperators)
   {
      Log("Seperatör bilgileri yükleniyor.");
      Log("İşlem yapılan seperatör:" +item.SeperatorName);
      obid = item.SeperatorId;
      Log("Kart oluştu, object Id : "+ obid.ToString());
      a_NavigationInfo getFolderFile =Server.productivity.rNavigation.GetFolderFiles(string.Empty, obid, true,2,1,
            string.Empty,string.Empty,string.Empty,string.Empty,
                  string.Empty,string.Empty);     

      foreach (PW_SYSOBJECT obj in getFolderFile.folderObjects)
      {
         ObjectID fileObjectId = new ObjectID(obj.OBJECT_ID);     
         customerID = ((string)AttachmentData.getAttribute("MUSTERI_KODU")).PadLeft(7,"0"[0]);
         Log("İşlem yapılan belge: {0}"+ obj.OBJECT_NAME);
         Log("Taşınan belgenin nesne numarası "+ fileObjectId);
         StringBuilder sb = new StringBuilder(@"Kabinetler\Müşteri");
         string strA = customerID;
         string[] split = new string[strA.Length / 2 + (strA.Length % 2 == 0 ? 0 : 1)];

         for (int i = 0; i < split.Length - 1; i++)
         {
            sb.Append("\\");
            sb.Append(strA.Substring(i * 2, i * 2 + 2 > strA.Length ? 1 : 2));
         }

         sb.Append("\\");
         sb.Append(customerID);
         string targetPath2 = string.Format(sb.ToString() + "\\Müşteri Resmi Evrakları\\{0}",item.SeperatorName);
         Log("Hedef kabinet:"+targetPath2);
         a_PathInfo pi1 = Server.productivity.rNavigation.CreateFolderByPath(targetPath2, new ObjectID((string)AttachmentData.getAttribute("ACL_ID")), false);
         if (pi1.ErrorCode != 0) throw new Exception(string.Format("Kabinet yolu yaratılamadı!"));

         ObjectID targetFolderId = new ObjectID(pi1.ObjectList[pi1.ObjectList.Count - 1]);
         ObjectID currentFolderId = new ObjectID(obj.OBJECT_ID);

         Server.productivity.rNavigation.MoveObject(fileObjectId, targetFolderId, 1);         
      }

   }
   SaveObject();
}
   catch(Exception ex)
{
   Log("Hata:"+ex.Message+ "-" + WorkflowId);
   var hata = string.Empty;
   hata=ex.Message;
   if(hata=="Object reference not set to an instance of an object."){
      FormData.Set("MAKRO_HATASI",hata + "-" + WorkflowId + " Nolu Akış Ekinde Dosya Kartı Bulunamadı!...");
      FormData.Set("MAKRO_DURUMU","Hata");
}
else
{
   FormData.Set("MAKRO_HATASI",hata);
   FormData.Set("MAKRO_DURUMU","Hata");  
}
SaveObject();
return  true;
}
```

\

\
