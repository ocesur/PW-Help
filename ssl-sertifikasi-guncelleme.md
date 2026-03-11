PaperWork Uygulama sunucusu (Content Server) ile IIS arasındaki
haberleşme SSL sertifikası ile şifrelenebilir. Aynı zamanda geliştirme
katmanı ile Uygulama Sunucusuna yapılan her türlü erişim bu sertifika
ile şifreli çalışır.

Sertifika süresi dolduğunda aşağıdaki adımlar gerçekleştirilerek
sertifika güncellenebilir.

1.  Tanımlamalar bölümünde parametre tanımları ekranı açılır.
2.  CERTIFICATE_FILE isimli parametrede sertifikanın Content Server
    üzerindeki yolu bulunur. Yeni sertifika bu adrese eskisinin üzerine
    yazılacak şekilde kopyalanır.
3.  [CLIENT_CERTIFICATE_FILE Bu sertifika dosyası, content servisi
    aracılığıyla Productivity Layer\'a bağlanmak için kullanılır.Yeni
    sertifika bu adrese eskisinin üzerine yazılacak şekilde
    kopyalanır.]{teams="true"}
4.  CERTIFICATE_PASSWORD parametresinde sertifika şifresi bulunur.
    Normal şartlarda bu veri veri tabanı üzerinde şifreli tutulur. Bu
    ekranda şifreli şifre açık yazılır ve değiştirmenize izin verir.
    Eğer sertifika şifreniz değişti ise bu bölümden yeni şifre girilerek
    kaydedilir.
5.  Content Server tekrar başlatılır ve sertifikanın geçerli olması
    sağlanır.

::::: {.section .infoBox}
::: title
Content Server Tekrar Başlatma
:::

::: content
Uygulama sunucusunu tekrar başlatılması [Servis
Yönetimi](/tr/docs/admin-servis-yonetimi){rel="nofollow" translate="no"}
sayfasında açıklanmıştır.
:::
:::::

::::: {.section .infoBox}
::: title
SSL Sertifika Kullanımını Aktif Etme
:::

::: content
Eğer daha önce SSL sertifikası aktif değil ise SSLENABLE parametresi F
olarak yer alır. Sertifika ilk defa kurulacak ise bu parametrenin T
olarak değiştirilmesi gerekir. Bu işlem
[parametre ](/tr/docs/p50050511001){rel="nofollow"
translate="no"}tanımları ekranından yapılabilir.
:::
:::::

::::: {.section .infoBox}
::: title
IIS SSL Sertifikası
:::

::: content
Yukarıda anlatılanların IIS Sertifikası kurulumu ile alakası yoktur. IIS
üzerindeki sertifika için ilgili ürünün kılavuzları incelenebilir.
:::
:::::

::::: {.section .errorBox}
::: title
SSL Sertifikası
:::

::: content
SSL sertifikası güvenlik yeterliliği ve IIS güvenlik ayarları kurum
sorumluluğundadır.
:::
:::::
