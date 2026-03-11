``` {.csharp code-id="section-1681720978332" data-language="csharp"}
public static void Import()
        {
            ObservableCollection<LookupItem> acls = productivity.rLookup.GetACLs(string.Empty); // Yetki setleri listesi "acls" değişkenine atanır.
            LookupItem acl = acls.FirstOrDefault(x => x.Name == "Default Acl"); // Belgeye verilecek olan "Default Acl" yetki seti alınır.

            ObservableCollection<LookupItem> types = productivity.rLookup.GetTypes(string.Empty, string.Empty); // Tip listesi "types" değişkenine atanır.
            LookupItem type = types.FirstOrDefault(x => x.Title == "Egitim"); // Belge için kullanılacak olan "Egitim" tipi alınır.

            ObservableCollection<LookupItem> forms = productivity.rLookup.GetForms(false, string.Empty); // Form listesi "forms" değişkenine atanır.
            LookupItem form = forms.FirstOrDefault(x => x.Title == "Egitim Form"); // Belge için kullanılacak "Egitim Form" formu alınır.

            string[] files = Directory.GetFiles(@"C:\EgitimKlasör"); // "C:\EgitimKlasör" dosya yolu altındaki belgeler atanır.
            foreach (string filename in files) // "files" değişkenine atanan belgeler dönülür
            {
                string type_name = type.Name; // Tip adı atanır
                string form_name = form.Name; // Form adı atanır
                string acl_id = acl.ObjectId; // Yetki setinin numarası atanır
                string save_path = @"TR_CABINETS\PW Egitim Kabineti\PW Egitim Klasör\PW Egitim Dosya Kartı\PW Egitim Seperator"; // Belgelerin kaydedileceği kabinet yolu atanır.
                string folder_id = createFolder(save_path, acl_id); // Eğer belirtilen yolda ilgili klasör yoksa oluşturur, varsa varolan klasörün klasör numarası atanır.
                string object_name = Path.GetFileName(filename); // "C:\EgitimKlasör" dosya yolundaki belgenin adı alınır.
                string file_ext = Path.GetExtension(filename).Replace(".", "").ToUpper().Replace("İ", "I"); // "C:\EgitimKlasör" dosya yolundaki belgenin uzantısı formatlanarak atanır.

                ITypes fobject = productivity.rDocument.getDocument(ObjectID.Empty, type_name); // Verilen tip adına ait yeni bir döküman oluşturulur (Sistem tipinde belge eklenecekse "PW_SYSOBJECT" verilmelidir)
                fobject.Set("ACL_ID", acl_id); // Dökümanın yetki seti verilir.
                fobject.Set("OBJECT_TYPE", type_name); // Tip adı verilir. (Sistem tipinde belge eklenecekse "PW_SYSOBJECT" verilmelidir)
                fobject.Set("FOLDER_ID", folder_id); // Klasör numarası verilir.
                fobject.Set("FORM_NAME", form_name); // Form adı verilir. (Belge sistem tipinde verilecekse "string.Empty" verilebilir)
                fobject.Set("IS_VIRTUAL_DOC", "T"); // Belirtilen kabinet yolu bir dosya kartının içinde ise "T", değilse "F" verilir.
                fobject.Set("FORM_VERSION", "1"); // Formun versiyonu verilir.
                fobject.Set("OBJECT_NAME", object_name); // Eklenecek belgenin adı verilir.
                fobject.Set("FILE_FORMAT", file_ext); // Eklenecek belgenin uzantısı verilir.
                fobject.Set("IS_FTS", true); // Tip alanlarının aranabilir özelliği verilir.
                fobject.Set("IS_LAST_VERSION", true); // Son versiyon olup olmayacağı belirtilir.
                fobject.Set("CONTENT_TYPE", Definitions.CONTENT_TYPE_DOC); // İçerik tipi belirtilir.
                fobject.Set("VIRTUAL_DOC_ID", "FF0009000002D85D"); // Dosya Kartının Id'si verilmeli (PW Egitim Dosya Kartı)

                a_GenericResult res = productivity.rDocument.SetDocument(fobject); // Oluşturulan döküman kaydedilir.
                if (res.ErrorCode != 0) // Hata yok "ErrorCode" 0' dır.
                    throw new Exception(res.Message);
                string obj_id = res.Result; // Oluşturulan belgenin numarası atanır.
                
                a_GenericResult ires = productivity.rFile.Import(new ObjectID(obj_id), filename, file_ext); // Oluşturulan döküman adı, eklenecek belgenin adı ve belgenin uzantısı ile birlikte belgenin eklenmesi sağlanır.

                if (ires.ErrorCode != 0)
                    throw new Exception(ires.Message);

            }
        }

public static string createFolder(string path, string acl_id) 
        {
            a_PathInfo pth = productivity.rNavigation.CreateFolderByPath(path, new ObjectID(acl_id), false); // Eğer belirtilen yolda ilgili klasör yoksa oluşturur, varsa varolan klasörün klasör numarası atanır.
            return pth.ObjectList[pth.ObjectList.Count - 1]; // Son klasörü alır
        }
```
