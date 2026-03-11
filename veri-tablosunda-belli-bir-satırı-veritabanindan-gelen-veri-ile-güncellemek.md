#### Veri Tablosunda Belli Bir Satırı Veritabanından Gelen Veri ile Güncellemek

Bir form üzerinde basit bir veri tablosu oluşturuyoruz. Veritabanında
kullanıcı tablosu üzerinden belirli bir kullanıcı için sorgu yaparak
kayıt getirip bu kaydın kullanıcı adı bilgisini tablomuzun ikinci
kolonuna yazdırmayı hedefliyoruz. Formumuz aşağıda görüldüğü gibidir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1753884399570.png){.fr-fic
.fr-fil .fr-dib .fr-draggable .fr-bordered .fr-shadow
style="width: 900px;"}

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1753884661497.png){.fr-fic
.fr-fil .fr-dib .fr-draggable .fr-shadow .fr-bordered
style="width: 900px;"}

Güncelle butonunun arkasında bulunan kod bloğu aşağıdaki gibidir.

``` {.javascript code-id="section-1720013210228" data-language="javascript"}
async function updateRow() {
    try {
        // Veri tablosunun tüm satırlarını getirir.
        var veriTablosu = PwForm.getRows("VERI_TABLOSU"); 
        // Kullanıcı adını sorgulayan SQL ifadesi.
        let result = await PwForm.Query("SELECT LOGIN_NAME, USER_NAME FROM PW_USER(NOLOCK) WHERE LOGIN_NAME='asaygili'", '');
        
        if (result.length > 0) {
            let user = result[0];
            // Veri tablosundaki her satırı kontrol eder.
            veriTablosu.forEach((veriTablosuRow, index) => {
                // Eşleşen satırı bulur.
                if (veriTablosuRow.TABLO_ALAN1 === user.LOGIN_NAME) {
                    // Eşleşen satırın ikinci kolonunu günceller.
                    PwForm.setRowValue("VERI_TABLOSU", "TABLO_ALAN2", index, user.USER_NAME);
                }
            });
            // Tabloda yapılan güncelleme sonrasında tablo yenilenerek verilerin form üzerine yansıması sağlanır.
            PwForm.component("VERI_TABLOSU").redraw();
        }
    } catch (error) {
        console.error("Error updating row:", error);
    }
}
```

Yukarıdaki kod bloğu, güncelle butonuna tıklandığında tablomuzda bulunan
satırları kontrol ederek gerekli eşleşmenin sağlandığı satır için
güncelleme yapmaktadır.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1753884791240.png){.fr-fic
.fr-fil .fr-dib .fr-draggable .fr-shadow .fr-bordered
style="width: 900px;"}

Yukarıdaki görselde görüldüğü üzere, tabloda bulunan üç satırdan
yalnızca birinde güncelleme gerçekleşmiştir.

\
