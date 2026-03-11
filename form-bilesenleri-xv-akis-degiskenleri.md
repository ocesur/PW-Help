Akışın Elektronik formlarında akış değişkenlerine aşağıdaki gibi
ulaşabilirsiniz. **Akışın başlangıç formunda bu değerlerin henüz
oluşmadığı unutulmamalıdır.**

``` {.javascript code-id="section-1658386696390" data-language="javascript"}
function getInfo() {
    //eğer akış formu ise aşağıdaki bilgilere ulaşılabilir
    console.log("workflowId : " + PwForm.WorkflowId);//Akış numarası
    console.log("AclId : " + PwForm.AclId);//Akış yetki seti
    console.log("AttorneyId : " + PwForm.AttorneyId);//Eğer vekaleten gelen akış ise vekalet numarası 

    console.log("FolderId : " + PwForm.FolderId);//Akış klasör numarası
    console.log("FormName : " + PwForm.FormName);//O elektronik formun adı
    console.log("ObjectId : " + PwForm.ObjectId);//Akışın nesne numarası
    console.log("ProcessId : " + PwForm.ProcessId);//Akış taslağı akış numarası
    console.log("TypeName : " + PwForm.TypeName);//Akışın tip adı
    console.log("WorkitemId : " + PwForm.WorkitemId);//Akış adımının tekil numarası

    //eğer dk formu ise aşağıdaki bilgilere ulaşılabilir
    console.log("isCard : " + PwForm.isCard);//Eklenti Dosya Kartı Kaydı mı?
    console.log("CardId : " + PwForm.CardId);//Dosya kartı numarası
}
```
