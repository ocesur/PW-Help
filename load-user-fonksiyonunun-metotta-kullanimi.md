#### Load User Fonksiyonunun Metotta Kullanımı

LoadUser fonksiyonu metot ve makrolardan çağırılabilmektedir.
Fonksiyonun amacı kullanıcıya ait LOGIN_NAME veya USER_ID bilgisini
parametre vererek kullanıcıya ait tüm bilgileri getirmektir. Buradaki
örnekte fonksiyonun metot içerisinde kullanımı gösterilecektir.

``` {.csharp code-id="section-1687517740163" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Paperwork.Methods;
using Paperwork.Library;
namespace mtdLoadUser
{
    public class mtdLoadUser: PWMethod
    { 
        public override int Execute(Dictionary<string, object> _paramList)
        { 
            this.paramList = _paramList;
            try
            {   
                base.ConnectServer();
                LoadUser();
                return 0;
            }
            catch (Exception e)
            {
                Log(e.Message);
                ErrorMessage = e.Message;//Hata duruumunda eposta bilgilendirme hata mesajı içeriğidir.
                return -1;
            }
            finally
            { 
                return 0;
            }
        }
        public void LoadUser()
        {
            a_UserInfo user = server.rUser.LoadUser(new ObjectID("6000010000000CD8")); //LoadUser fonksiyonu a_UserInfo tipinde veri dönmektedir.

            Log("Kullanıcı Detayı");
            Log("Nesne no :{0}", user.ObjectId);
            Log("Adı      :{0}", user.UserName);
            Log("Login    :{0}", user.UserLogin);
            Log("Mail     :{0}", user.Email);
            Log("Position :{0}", user.Position);
            Log("Yetkisi  :{0}", user.Previleges);
            Log("Durumu   :{0}", user.State);
            Log("Pozisyon :{0}", user.Title);
            Log("Kaynak   :{0}", user.Source);
            Log("Domain   :{0}", user.UserDomain);
            Log("OS Name  :{0}", user.UserOSName);
            Log("Son giriş:{0}", user.LastLogin);
            Log("Açıklama :{0}", user.Description);
        }
    }
}
```

Metotu çalıştırıp logları görüntülediğimizde ilgili kullanıcıya ait
bilgileri görebilmekteyiz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687517851394.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
