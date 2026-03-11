Bu örnek, elektronik form içerisinde girilmiş nesne numarasına ait
belgeyi indirmek için yapılması gerekenleri gösterir.

Öncelikle global fonksiyonlar bölümüne, aşağıdaki fonksiyonu
oluşturuyoruz :

``` {.javascript code-id="section-1703572628746" data-language="javascript"}
async function GetFile()
{
    //Yazı alanı içerisinde bulunan nesne numarası alınır
    let object_id = PwForm.get("txtObjectId");

    //Alınan Nesne Numarasına ait belgenin detayları veritabanından alınır
    let object = await PwForm.Query(String.Format("SELECT OBJECT_ID as OBJ_ID, OBJECT_NAME, FILE_FORMAT FROM PW_SYSOBJECT(NOLOCK) WHERE OBJECT_ID ='{0}'", object_id), "");
    let _obj = object[0];

    //Yeni bir AJAX isteği oluşturulur
    var request = new XMLHttpRequest();
    request.addEventListener('readystatechange', function(e) {
        switch (request.readyState) {
        case 2:
            if (request.status == = 200) {
            }
            break;
        case 3:

            break;
        case 4:
            var _OBJECT_URL = URL.createObjectURL(request.response);

            try {
                //İndirme işlemi yapılır.
                var a = document.createElement("a");
                a.style.display = "none";
                document.body.appendChild(a);
                a.href = _OBJECT_URL;
                a.setAttribute("download", _obj.OBJECT_NAME + "." + _obj.FILE_FORMAT);
                a.click();
                document.body.removeChild(a);
            }
            finally {
                window.URL.revokeObjectURL(_OBJECT_URL);
            }
            break;
        }
    });

    //Arşivden belgenin verisi alınır
    var url = "/Archive/Export?id=" + _obj.OBJ_ID + "&fileName=" + _obj.OBJECT_NAME + "&format=" + _obj.FILE_FORMAT;
    request.responseType = 'blob';
    request.open('get', url);
    request.send();
}
```

Elektronik formu aşağıdaki bilgileri içerecek şekilde düzenliyoruz (Daha
fazla alan da olabilir)

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703572678236.png){.fr-fic
.fr-fil .fr-dib .fr-bordered}

Tuş nesnesinin özel işlem alanında bu fonksiyonu çağırıyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703572726550.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow style="width: 397px;"}

Tuş tetiklenmesi sonucu belgenin inmesini bekliyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1703572757281.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
