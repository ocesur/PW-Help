Tanımlı bir raporun metot yardımı ile e-posta eklentisi olarak
gönderilmesi mümkündür. Bu işlem aslında "Rapor Tasarım" sayfasında
tanımlı iş ekleyerek yapılabilmektedir. Ancak burada, raporun kişi bazlı
parametre alması ve bu parametre sonucu oluşan raporun gönderilecek
e-postanın eki olması örneği ele alınmıştır.

Örneğimizde kullanılan bazı parametreler şunlardır:

MAIL_TEMPLATE_NAME: Kullanılacak olan e-posta şablonu.

MAIL_SUBJECT: E-postanın konusu.

REPORT_NAME: Raporun adı.

REPORT_FORMAT: Raporun çalışması sonucunda oluşacak belgenin formatı.
(Pdf, Excel)

FILE_FORMAT: E-posta ekinde olacak belgenin formatı. REPORT_FORMAT
parametresi ile uyumlu olması gerekmektedir. (pdf, xls)

**Kodu Kullanırken Dikkat Edilmesi Gerekenler**

E-posta Şablonu: MAIL_TEMPLATE_NAME parametresi ile belirtilen şablon,
e-postanın gövdesini oluşturacaktır. Şablonun sistemde tanımlı ve
erişilebilir olduğundan emin olun.

Raporun Adı ve Formatı: REPORT_NAME ve REPORT_FORMAT parametreleri,
hangi raporun hangi formatta oluşturulacağını belirler. Bu
parametrelerin doğru şekilde ayarlandığından emin olun.

Dosya Formatı: FILE_FORMAT parametresi, e-posta ekinin formatını
belirtir. Bu formatın REPORT_FORMAT ile uyumlu olması gerekmektedir.
Örneğin, REPORT_FORMAT \'Pdf\' ise FILE_FORMAT \'pdf\' olmalıdır.

**Rapor Parametrelerinin Eklenmesi**

Raporun kendi parametrelerinin eklendiği kısmı, \"Rapor Tasarım\"
sayfasında bulunan \"kod üret\" özelliğini kullanarak, oluşan kod
parçacığı ile değiştirerek kendi raporunuza uyumlu olacak hale
getirmeniz gerekmektedir. Bu, raporun doğru parametrelerle çalışmasını
ve istenilen verileri üretmesini sağlar.

``` {.csharp code-id="section-1717768017693" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Paperwork.Methods;
using Paperwork.Library;
using System.Data;
using System.Globalization;
using System.Collections.ObjectModel;
using Paperwork.Types;
using System.IO;
using System.Net;
using System.Net.Mail;
using ContentServer;
using System.Reflection;
using System.Text.RegularExpressions;
namespace mtd_izinRaporMail
{
    public class mtd_izinRaporMail : PWMethod
    {
        public override string MethodName { get { return "PWMethod-mtd_izinRaporMail-V5.1"; } }

        // Metodun giriş noktası
        public override int Execute(Dictionary<string, object> paramList)
        {
            Log("{0} başlatıldı...", MethodName);
            var retval = base.Execute(paramList);
            var res = new a_GenericResult();

            try
            {
                // Sunucuya bağlanmayı dener
                var info = base.ConnectServer();
                if (info.ErrorCode != "0")
                    throw new Exception(info.LMessage);
                // Ana işlemi gerçekleştirir
                Bilgilendirme();
                Log("Metod çalıştırıldı. {0}", DateTime.Now);
            }
            catch (Exception ex)
            {
                retval = -1;
                var msg = ex.ToString();
                Log(msg);
                res.ErrorCode = -1;
                res.Message = msg;
                Log(ex, "Metod Hatası:");
            }
            finally
            {
                // Entegrasyon raporunu loglar ve sunucudan bağlantıyı keser
                IntgrationReport(res);
                DisConnectServer();
                Log("{0} tamamlandı...", MethodName);
            }
            return retval;
        }
        // Kullanıcı bilgilerini çekip rapor gönderen ana fonksiyon
        private void Bilgilendirme()
        {
            Log("Bilgilendirme başladı.");
            // Kullanıcı bilgilerini çeken SQL sorgusu
            var sqlQuery = " SELECT USER_NAME,LOGIN_NAME,EMAIL FROM PW_USER(NOLOCK) WHERE STATE = '1' AND IS_INTERNAL = 'F' AND EMAIL <> ''";
            using (DataSet dset = server.rAdo.Query(sqlQuery, -1))
            {
                Log("Tablo satır sayısı : " + dset.Tables[0].Rows.Count.ToString());
                if (dset.Tables[0].Rows.Count > 0)
                {
                    // Her bir kullanıcı için rapor oluşturulur ve mail gönderimi yapılır
                    foreach (DataRow row in dset.Tables[0].Rows)
                    {
                        SendMail4Report(row["LOGIN_NAME"].ToString(), DateTime.Now.AddMonths(-1).Month.ToString(), row["EMAIL"].ToString());
                    }
                }
            }
        }
        // Raporu oluşturup e-posta ile gönderir
        private void SendMail4Report(string userName, string lastMonth, string mailTo)
        {
            try
            {
                Log(string.Format("Rapor tarih alanları. Kullanıcı Adı:{0}  Son Ay:{1}", userName, lastMonth));
                var body = "";

                // E-posta şablonunu çeken sorgu
                string bodyTempQuery = string.Format("SELECT TEMPLATE_DATA FROM PW_MAIL_TEMPLATE(NOLOCK) WHERE TEMPLATE_NAME = '{0}'", getParam("MAIL_TEMPLATE_NAME"));
                using (var ds = server.rAdo.Query(bodyTempQuery, -1))
                {
                    if (ds.Tables[0].Rows.Count > 0)
                        body = (string)ds.Tables[0].Rows[0]["TEMPLATE_DATA"];
                }
                // E-posta konusunu ve diğer parametreler
                var subject = getParam("MAIL_SUBJECT");
                var to = mailTo;
                var reportName = getParam("REPORT_NAME");
                var reportType = getParam("REPORT_FORMAT"); // Pdf, Excel: Büyük/Küçük harfe dikkat edilmeli
                var prms = new List<ReportServer.rReportParam>();

                // Rapor parametrelerini ekler
                prms.Add(new ReportServer.rReportParam()
                {
                    Name = "Kullanıcı Adı",
                    Value = userName,
                    DataType = "0",
                    DisplayColumn = "",
                    FieldName = "USER_NAME",
                    IsLike = false,
                    KeyColumn = "",
                    ListName = "",
                    TableName = "IZIN_SURESI_TABLOSU"
                });
                prms.Add(new ReportServer.rReportParam()
                {
                    Name = "Son Ay",
                    Value = lastMonth,
                    DataType = "0",
                    DisplayColumn = "",
                    FieldName = "SON_RAPOR_AY",
                    IsLike = false,
                    KeyColumn = "",
                    ListName = "",
                    TableName = "IZIN_SURESI_TABLOSU"
                });

                // Raporu oluşturur
                var reportData = server.rReport.ExecuteReport(reportName, prms.ToArray(), reportType);

                // E-posta gönderir
                if (!string.IsNullOrEmpty(to) && reportData != null && reportData.Length > 0)
                    SendMailTo(
                            subject,
                            body,
                            to,
                            reportName,
                            reportType,
                            reportData);
            }
            catch (Exception ex)
            {
                Log(ex.ToString());
                throw ex;
            }
        }

        // E-postayı gönderir
        private void SendMailTo(string subject, string body, string to, string fileName, string fileExtension, byte[] fileData)
        {
            try
            {
                using (var ds = server.rAdo.Query("SELECT USERNAME,PASSWORD,SERVER,IS_SECURE FROM PW_MAIL_ACCOUNT(NOLOCK) WHERE  IS_DEFAULT='T'", -1))
                {
                    if (ds.Tables[0].Rows.Count == 0)
                        throw new Exception("Tanımlı mail konfigürasyonu bulunamadı!");

                    string Mailserver = (string)ds.Tables[0].Rows[0]["SERVER"];
                    string userName = (string)ds.Tables[0].Rows[0]["USERNAME"];
                    string isSecure = (string)ds.Tables[0].Rows[0]["IS_SECURE"];
                    var pass = Paperwork.Utils.Cryptor.Decryptor.Aes256Decrypt((string)ds.Tables[0].Rows[0]["PASSWORD"], false);

                    // Sertifika doğrulamasını geçersiz kılar
                    ServicePointManager.ServerCertificateValidationCallback = ((sender, certificate, chain, sslPolicyErrors) => true);

                    // E-posta mesajını hazırlar
                    MailMessage mail = new MailMessage(userName, to);
                    SmtpClient client = new SmtpClient();
                    client.Port = 587;
                    client.DeliveryMethod = SmtpDeliveryMethod.Network;
                    client.EnableSsl = isSecure.Equals("T");
                    client.Timeout = 600000;
                    client.Credentials = new NetworkCredential(userName, pass);
                    client.Host = Mailserver;
                    mail.Subject = subject;
                    MemoryStream st = new MemoryStream(fileData);
                    mail.Attachments.Add(new Attachment(st, fileName + "." + getParam("FILE_FORMAT"))); // xls
                    mail.IsBodyHtml = true;
                    mail.Body = body;

                    // E-postayı gönderir
                    client.Send(mail);
                    Log("E-posta başarıyla gönderildi: " + to);
                }
            }
            catch (Exception ex)
            {
                Log("E-posta gönderim hatası: " + ex.ToString());
                throw ex;
            }
        }
        // Entegrasyon raporunu loglar
        private void IntgrationReport(a_GenericResult result)
        {
            try
            {
                server.rIntegration.ReportDetail("ReportExporter", result.ErrorCode == 0, result.Message);
                Log("Entegrasyon raporu başarıyla loglandı.");
            }
            catch (Exception ex)
            {
                Log("Entegrasyon raporu hatası: " + ex.ToString());
            }
        }
    }
}
```
