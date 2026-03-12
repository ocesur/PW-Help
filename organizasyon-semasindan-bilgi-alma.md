Elektronik form üzerinde, organizasyon şemasından kullanıcıya ait
bilgilerin getirilmesi için gerekli fonksiyon şu şekildedir :

``` {.javascript code-id="section-1695638568993" data-language="javascript"}
function KisiListesi_Change() {

  // Listemizde kullanıcı bilgileri tutuluyor. Key2 anahtarı "loginName" parametresine karşılık geliyor.
  var loginName = PwForm.component("KISI_LISTESI").SelectedRow.Key2;
  
  // Kullanacağımız organizasyon şemasının ismini bu şekilde parametre olarak ekliyoruz.
  var rootId = "PAPERWORK_ORG"; 

  PwForm.getPL("/Services/Workflow/GetOrganizationPerson", { rootID: rootId, username: loginName }).then(res => {
    debugger;
    console.log(res);
    
    // Organizasyon şemasından getirdiğimiz kullanıcıya ait üst yönetici bilgisini elektronik formum uzda bir alana atama yapıyoruz.
    PwForm.set("YONETICI", res.ManagerName); 
  });
}
```
