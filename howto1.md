Sistemde var olan bir yetki setine aşağıdaki kod örneğiyle yeni bir
kullanıcı veya kullanıcı grubu ekleyerek yetkilendirebilirsiniz.

``` {.csharp data-language="csharp"}
a_ACLInfo acl = server.rUser.GetACLs("Yetki Seti Adı", -1).Items.FirstOrDefault();
if (acl != null)
{
    //yetki setine kullanıcı ve grup eklemek için;
    a_ACLMemberInfo m_user = new a_ACLMemberInfo()
    {
        Name = new ObjectName("Yazılım"),
        DisplayName = "Yazılım",
        MemberType = MemberTYPES.GROUP,// MemberTYPES.USER
        ObjectId = acl.ObjectId,
        BasicPerm = 0,// Yetkisiz= 0 , Tüm yetkiye sahip =31 
        ExtPerm = 0 //  Yetkisiz= 0 , Tüm yetkiye sahip =4194303 
    };
    acl.Members.Add(m_user);

    var createRes = server.rUser.UpdateACL(acl);
    if (createRes.ErrorCode != 0)
        throw new Exception($"Acl oluşturulurken hata oluştu. Hata : {createRes.Message}");
}
```
