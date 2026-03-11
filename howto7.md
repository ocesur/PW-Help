Bir iş akışında makro adımında akış ekindeki belgeler ile birlikte
e-posta göndermek için aşağıdaki örnek kod parçacığından
yararlanabilirsiniz.

``` {.csharp data-language="csharp"}
try {
    LoadObject();
    LoadAttachment();

    a_MailTemplate template = new a_MailTemplate();
    template.To   = "abc@xyz.com.tr";
    template.From = "PaperWork";

    template.Message    = "E-posta ileti içeriği";
    template.Subject    = "E-posta konusu";
    template.IsLink     = false;
    template.TemplateId = "FFFFFFFFFFFFFFFF";

    a_Card crd = Server.productivity.rCard.GetCard(new ObjectID(AttachmentId), false);
    foreach (a_SeperatorInfo sepInfo in crd.CardSeperator.Seperators) {
        // Kullanılan dosya kartının altında istenilen belgelerin bulunduğu klasör adı yazılır
        if (sepInfo.SeperatorName.Value == "Belgeler")
        {
            foreach (a_ContentInfo item in sepInfo.Contents) {
                var detail = new a_MailDetail();
                detail.ObjectId     = item.ContentId;
                detail.ObjectName   = item.ContentName;
                detail.Format       = item.FileFormat;
                detail.InculeIndex  = false;
                detail.IsLink       = false;
                detail.IsOriginal   = true;
                detail.IsSend       = true;
                detail.IsSeperator  = false;
                detail.IsZip        = false;
                detail.Parent       = string.Empty;
                detail.Password     = string.Empty;
                detail.Rendition    = string.Empty;
                detail.TicketType   = string.Empty;
                detail.ValidCount   = 0;
                detail.ValidFrom    = DateTime.Now;
                detail.ValidTo      = DateTime.Now;
                template.MailDetail.Add(detail);
            }
        }
    }

    Paperwork.Library.a_GenericResult retval2 = Server.productivity.rCard.SendMail(ObjectID.Empty, template);
    if (retval2.ErrorCode != 0)
        Log("Mail gönderilirken hata oluştu. Hata:" + retval2.Message);
    else
        Log("Mail gönderimi tamamlandı.");
        
    SaveObject();
    SaveAttachment();
}
catch(Exception ex)
{
    throw new Exception(ex.Message);
}
```
