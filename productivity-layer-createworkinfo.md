#### Productivity Layer CreateWorkInfo Kullanımı

Workitem ID\'si verilen akış adımı için, verilen kullanıcı listesindeki
kullanıcılara bir bilgilendirme manual adımı oluşturur.

Metot Adı : CreateWorkInfo

Kütüphane Adı : CreateWorkInfo

Sınıf Adı : CreateWorkInfo

Parametreler : 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1704783651523.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Metot kodumuz :

``` {.csharp code-id="section-1704783701187" data-language="csharp"}
using Paperwork.Library;
using Paperwork.Methods;
using System;
using System.Collections.Generic;
using System.Text;
using System.Data;
using System.IO;
using ContentServer;
namespace CreateWorkInfo
{
    public class CreateWorkInfo : PWMethod
    {
        //@param WORKITEM_ID, bilgilendirme adımı gönderilecek akışın workitem idsi
        //@param USER_LIST, bilgilendirme adımının kimlere gönderileceği, kullanıcıların login nameleri , ile ayrılarak girilmelidir örn. testuser,testuser2,testuser3
        public override string MethodName { get { return "PWMethod-CreateWorkInfo-V5.0"; } }
        public override int Execute(Dictionary<string, object> paramList)
        {
            Log("{0} started...", MethodName);
            var retval = base.Execute(paramList);
            string msg = string.Empty;
            try
            {
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);
                server.InitAssemblies();
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
                    if (server == null)
                        Log("Productivity Layer connection was fail");
                    else
                        server.rIntegration.ReportDetail(MethodName, retval == -1 ? false : true, msg);
                    DisConnectServer();
                }
                catch (Exception ex)
                {
                    Log("CreateWorkInfo Disconnect Ex :", ex);
                }
            }
            return retval;
        }

        private void InternalExecute()
        {
            
            
            string workitemId = getParam("WORKITEM_ID");
            string userListString = getParam("USER_LIST");

            if(string.IsNullOrEmpty(userListString)) return;

            List<rLookupItem> userList = new List<rLookupItem>();
            string[] user = userListString.Split(',');
            foreach(string userName  in user)
            {
                userList.Add(new rLookupItem() { Name = userName });//Mail gönderilecek kullanıcının giriş adı
            }
            var retVal = server.rWorkflow.CreateWorkInfo(workitemId,userList);
            if (retVal.ErrorCode != 0)
                throw new Exception(retVal.Message);
            else
                Console.WriteLine(retVal.Result);
        }
    }
}
```

Metot örnek bir akış Workitem ID\'si ile çalıştırıldığında örnek
kullanıcı üzerine aşağıdaki gibi bir bilgilendirme adımı yönlendirmiştir
:

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1704783751094.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
