#### Connection Pool Kullanım Örneği

Bu uygulama, Paperwork SDK katmanı üzerinde yapılması istenen işlemler
için daha güvenli ve verimli bir erişim sağlanması için oluşturulmuştur.
Singleton tasarım kalıbı kullanılarak oluşturulan bu örnekte, locklar
kullanılarak aynı anda birden fazla thread tarafından session
oluşturulması engellenmiş, sistemde aktif olan sessionlar kullanılarak,
connection pool üzerinden kaynak kullanımının optimizasyonu ve yönetimi
sağlanmıştır. Esneklik sağlanması amaçlı konfigürasyon bilgileri config
dosyasından alınmış, kullanıcı sessionları uygulama içerisindeki Login
ve Logout fonksiyonları ile yönetilmiştir. 

Coonection pool kapasitesinin dolması ve sunucu erişiminin kaybolması
gibi senaryoların engellenmesi amaçlanmıştır. Uygulama üzerinde SDK
katmanı kullanılarak dosya kartı bilgilerinin getirilmesi ile ilgili
örnekler geliştirilmiştir. İhtiyaca göre sdk katmanı üzerinden farkı
senaryolarda geliştirmeler yapılabilir.

``` {.csharp code-id="section-1730457007977" data-language="csharp"}

using Paperwork.Library;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using static System.Runtime.InteropServices.JavaScript.JSType;
namespace CPExample.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }
        public string GetCard(string cardId)
        {
            PWConnector.Instance.CheckAlive(); //Session kontrolü yapılır ve aktif olan session yoksa yeni session üzerinden login işlemi yapar.
            var card = PWConnector.Instance.Get().rCard.GetCard(new ObjectID(cardId),true); //Aktif sessionın productivity nesnesi üzerinden SDK'ya erişir ve id'si verilen kart bilgilerini döndürür.
            var json = Newtonsoft.Json.JsonConvert.SerializeObject(card); // Kart bilgilerini json data olarak verir.
            return json;
        }
        public string GetCardData(string cardId)
        {
            PWConnector.Instance.CheckAlive(); //Session kontrolü yapılır ve aktif olan session yoksa yeni session üzerinden login işlemi yapar.
            var card = PWConnector.Instance.Get().rCard.GetCard(new ObjectID(cardId),true); //Aktif sessionın productivity nesnesi üzerinden SDK'ya erişir ve id'si verilen kart bilgilerini döndürür.
            var json = Newtonsoft.Json.JsonConvert.SerializeObject(card.CardData,
            Newtonsoft.Json.Formatting.Indented); // Kart index alan bilgilerini json data olarak verir.
            return $"<pre>{json}</pre>";
        }
        public string GetCardSeperators(string cardId)
        {
            PWConnector.Instance.CheckAlive(); //Session kontrolü yapılır ve aktif olan session yoksa yeni session üzerinden login işlemi yapar.
            var card = PWConnector.Instance.Get().rCard.GetCard(new ObjectID(cardId),true); //Aktif sessionın productivity nesnesi üzerinden SDK'ya erişir ve id'si verilen kart bilgilerini döndürür.
            var json = Newtonsoft.Json.JsonConvert.SerializeObject(card.CardSeperator, Newtonsoft.Json.Formatting.Indented); // Kart alt klasör bilgilerini json data olarak verir.
            return $"<pre>{json}</pre>";
        }
        public string Logout()
        {
            PWConnector.Instance.Logout(); //Aktif session'ı sonlandırır.
            return string.Empty;
        }
    }
}
```

``` {.csharp code-id="section-1730457495075" data-language="csharp"}

using Paperwork.Connect;
using Paperwork.Library;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Web.Services.Description;
namespace CPExample
{
    public class PWConnector
    {
        private string AppName = "Demo";
        private string SessionId;
        public bool SessionAvailable = false;
        public string ServerInfo;
        private string UserName;
        private string Password;
        static readonly object instanceLock = new object(); //Aynı anda birden fazla PWConnector nesnesi oluşturulmaması için kullanılacak lock nesnesi oluşturulur.
        private static PWConnector instance; //Uygulama üzerinde yapılacak her işlemi zaten hali hazırda aktif olan bir sessionda yapılması için oluşturulan PWConnector tipinde singleton instance'dır.
        public static PWConnector Instance
        {
            //Singleton private instance'a erişim sağlayacak public bir instance'dır.
            //Private instance daha önce yaratılmamış ise (null ise), lock nesnesi (instanceLock) yardımıyla aynı andan birden fazla oluşturulamayacak şekilde singleton instance nesnesini oluşturur.
            get
            {
                if (instance == null)
                {
                    lock (instanceLock)
                    {
                        if (instance == null)
                            instance = new PWConnector();
                    }
                }
                return instance;
            }
        }
        public PWConnector()
        {
            //Content sunucusuna bağlantı için Web.config ya da App.config üzerinden host, user, password gibi gerekli bilgileri çeker. Ayrıca session yönetimi için maxpoolsize, minpoolsize, timeout gibi bilgiler de alınır.
            //Bu constructor ile nesne oluşturulduğunda, constructor içerisindeki Login metodu ile de verilen kullanıcı bilgileri ile ortama login işlemi yapar.
            var pwSettings = new
            {
                Port = "8099",
                host = ConfigurationManager.AppSettings["PwHost"],
                user = ConfigurationManager.AppSettings["PwUser"],
                pass = ConfigurationManager.AppSettings["PwPass"],
                minPoolSize = 2,
                maxPoolSize =
            Int32.Parse(ConfigurationManager.AppSettings["PwMaxPoolSize"]),
                isSecure = ConfigurationManager.AppSettings["PwSecure"] == "1",
                loggingEnabled = ConfigurationManager.AppSettings["PwLoggingEnabled"] == "1",
                timeout = 10,
                language = "tr",
                customerId = "",
                tempFolder = @"c:\Temp\"
            };
            ConnectionPool.TempFolder = pwSettings.tempFolder;
            ConnectionPool.InitializeServers(pwSettings.host, pwSettings.Port,
            string.Empty, string.Empty, pwSettings.isSecure, "", pwSettings.minPoolSize,
            pwSettings.maxPoolSize, pwSettings.timeout);
            ConnectionPool.ConnectionType = ClientTypes.ProductivityLayer;
            ConnectionPool.DefaultLang = pwSettings.language;
            ConnectionPool.CustomerId = pwSettings.customerId;
            ConnectionPool.PoolLog = pwSettings.loggingEnabled;
            ConnectionPool.onSessionEnd = onSessionEnd;
            this.UserName = pwSettings.user;
            this.Password = pwSettings.pass;
            Login();
        }
        private void onSessionEnd(object sender, EventArgs e)
        {
            //Aktif olan session süresi sona erdiğinde neler yapılacağını belirtir. Bu hali ile generic bir exception oluşturur.
            throw new Exception("");
        }
        public Productivity Get()
        {
            //Paperwork SDK'sına erişim için verilen session id'ye ait productivity nesnesini döndürür.
            return ConnectionPool.GetServer(SessionId).productivity;
        }
        public bool CheckAlive()
        {
            //İlgili sessionın hala aktif olup olmadığını kontrol eder. Aktif değil ise tekrar login işlemi yapılır ve yeni session oluşturulur. Aktif sessionı döndürür.
            if (!SessionAvailable)
                Login();
            else
            {
                Ping();
                if (!SessionAvailable)
                    Login();
            }
            return SessionAvailable;
        }
        private bool Login()
        {
            try
            {
                //Verilen kullanıcı bilgileri ile ilgili kullanıcıya ait yeni bir session oluşturur. Login işlemi yapar.
                var info = ConnectionPool.GetServer(UserName, Password,
                ClientTypes.ProductivityLayer, AppName);
                if (info.ErrorCode == "0")
                {
                    SessionId = info.SessionId;
                    SessionAvailable = true;
                    ServerInfo = info.ServerInfo;
                }
                else
                {
                    //logger.Error("Login failed:" + info.LMessage);
                    SessionAvailable = false;
                }
            }
            catch (Exception ex)
            {
                //logger.Error("Login failed::" + ex.Message);
                SessionAvailable = false;
            }
            return SessionAvailable;
        }
        private bool Ping()
        {
            try
            {
                //Aktif session bilgisini çeker. Hata almaz ise aktif session vardır. var gr = Get().rUser.GetSessionId();
                SessionAvailable = gr.ErrorCode == 0;
            }
            catch
            {
                SessionAvailable = false;
            }
            return SessionAvailable;
        }

        internal void Logout()
        {
            //Aktif session varsa, ilgili session id kullanılarak logout işlemi yapılır.
            if (!string.IsNullOrEmpty(SessionId) && SessionAvailable)
            {
                try
                {
                    Get().rLogin.Logout(SessionId);
                }
                catch (Exception ex)
                {
                    //logger.Error("Logout failed::" + ex.Message);
                }
                SessionAvailable = false;
                SessionId = string.Empty;
            }
        }
    }
}
```
