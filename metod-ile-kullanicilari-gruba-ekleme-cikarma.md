#### Metod İle Bir Kullanıcıyı Bir Gruba Ekleme

``` {.csharp code-id="section-1680243689142" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Paperwork.Methods;
using Paperwork.Library;
namespace UserAndGroup
{
    public class UserAndGroup: PWMethod
    { 
        public override int Execute(Dictionary<string, object> _paramList)
        { 
            this.paramList = _paramList;
            try
            { 
                Log("Metod çalışmaya başladı");
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);
                
                UserForGroup();
                return 0;

            }
            catch (Exception e)
            {
                Log(e.Message);
                ErrorMessage = e.Message;//Hata durumunda eposta bilgilendirme hata mesajı içeriğidir.
                return -1;
            }
            finally
            { 
            }
        }
        public void UserForGroup(){
            try{
                a_GenericResult retval = server.rUser.AddUserInGroup("aduz", "_testGroup"); // 2 adet string tipte parametre veriyoruz.
                if(retval.ErrorCode != 0){ // sonucumuzun başarılı olup olmadığını kontrol ediyoruz. Eğer sonuç 0 ise işlem başarıyla gerçekleştiği anlamına geliyor.
                    Log("kullanıcı grubua eklenemedi ");
                    Log(retval.Message.ToString());
                }
                else{
                    Log("kullanıcı gruba eklendi");
                }
            }
            catch(Exception ex){
                throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
            }
        }
    }
}
```

#### Metod İle Bir Kullanıcıyı Bir Gruptan Çıkarma

``` {.csharp code-id="section-1680243725531" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Paperwork.Methods;
using Paperwork.Library;
namespace UserAndGroup
{
    public class UserAndGroup: PWMethod
    { 
        public override int Execute(Dictionary<string, object> _paramList)
        { 
            this.paramList = _paramList;
            try
            { 
                Log("Metod çalışmaya başladı");
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);
                
                UserForGroup();
                return 0;

            }
            catch (Exception e)
            {
                Log(e.Message);
                ErrorMessage = e.Message;//Hata durumunda eposta bilgilendirme hata mesajı içeriğidir.
                return -1;
            }
            finally
            { 
            }
        }
        public void UserForGroup(){
            try{
                a_GenericResult retval = server.rUser.RemoveUserFromGoup("aduz", "_testGroup"); // 2 adet string tipte parametre veriyoruz.
                if(retval.ErrorCode != 0){ // sonucumuzun başarılı olup olmadığını kontrol ediyoruz. Eğer sonuç 0 ise işlem başarıyla gerçekleştiği anlamına geliyor.
                    Log("kullanıcı gruptan çıkarılamadı ");
                    Log(retval.Message.ToString());
                }
                else{
                    Log("kullanıcı gruptan çıkarıldı");
                }
            }
            catch(Exception ex){
                throw new Exception("Makro Hata Aldı! Hata : " + ex.Message);
            }
        }
    }
}
```

\
