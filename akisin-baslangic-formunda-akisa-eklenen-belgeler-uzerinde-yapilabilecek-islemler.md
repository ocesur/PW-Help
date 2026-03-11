[PaperWork **V6.2 ve üzeri sürümlerde** kullanıcı deneyimini ve kontrol
mekanizmalarını güçlendirmek amacıyla yeni bir geliştirme devreye
alınmıştır. Bu geliştirme sayesinde;]{type="spanMark"}

- [Akış veya form üzerine eklenen **toplam belge
  sayısı**,]{type="spanMark"}

- [Bu belgelere ait **toplam dosya boyutu (MB
  cinsinden)**]{type="spanMark"}

[aynı anda hesaplanabilmektedir.]{type="spanMark"}

[Bu yapı özellikle **ek boyut limiti olan senaryolarda**, kullanıcıyı
önceden bilgilendirmek ve olası hataları engellemek amacıyla
kullanılabilir.]{type="spanMark"}

#### Kullanım Senaryosu {#kullanım-senaryosu block-id="mja1gvz9-ev3kri-010"}

[Kullanıcı, akışın başlangıç adımında birden fazla belge eklemektedir.
Sistem yöneticisi veya PaperWork sorumlusu, eklenen
belgelerin:]{type="spanMark"}

- [Sayısını,]{type="spanMark"}

- [Toplam boyutunu (MB)]{type="spanMark"}

[kontrol ederek belirli bir limitin aşılması durumunda kullanıcıyı
bilgilendirmek istemektedir.]{type="spanMark"}

[Örneğin:]{type="spanMark"}

- [Maksimum toplam ek boyutu: **30 MB**]{type="spanMark"}

- [Maksimum belge sayısı: **10 adet**]{type="spanMark"}

[Bu kontrol, akış başlangıç formu üzerinde taslağa kaydetme/başlatma
aşamasında yapılabilir.]{type="spanMark"}

#### [Teknik Kullanım -- Örnek Kod]{type="spanMark"} {#teknik-kullanım-örnek-kod block-id="mja1khfr-bcho3u-027"}

[Aşağıdaki örnek JavaScript kodu, form üzerindeki ekler alanında yer
alan:]{type="spanMark"}

- [Toplam belge sayısını (]{type="spanMark"}`cnt`[),]{type="spanMark"}

- [Belgelerin toplam boyutunu
  (]{type="spanMark"}`totalMb`[)]{type="spanMark"}

[hesaplar.]{type="spanMark"}

[Bu kod **V6.2 ve üzeri sürümlerde** template yapısı içerisinde
kullanılabilir.]{type="spanMark"}

``` {.language-javascript block-id="mja1lc5y-krqguw-037" language="javascript" custom-title="Custom"}
var cnt = 0;
var totalSize = 0; // byte olarak biriktirilir


$.each($("#attc-tree-container .k-treeview-item"), function (i, chlds) {
var itm = $(chlds);


if (itm.find('.fa-folder').parent().length > 0) {


var files = itm.find('.fa-file');
if (files.length > 0) {


cnt += files.length;


files.each(function () {
var sizeAttr = $(this).parent().find("span[data-file-size]").attr("data-file-size");
if (sizeAttr) {
totalSize += parseInt(sizeAttr); // byte olarak toplanır
}
});
}
}
});


var totalMb = (totalSize / (1024 * 1024)).toFixed(2);
console.log("Toplam Dosya Boyutu (MB): " + totalMb);
console.log("Toplam Belge Sayısı: " + cnt);
```

#### [Nasıl Kullanılır?]{type="spanMark"} {#nasıl-kullanılır block-id="mja1n723-5jiv8u-038"}

1.  [İlgili form tasarım ekranında **Kodlama** alanı
    açılır.]{type="spanMark"}

2.  [Yukarıdaki kod, ihtiyaca göre düzenlenerek **Global Fonksiyonlar,
    Paylaşılan Kodlar veya Tip Bazında Ortak Kodlar** sayfasından uygun
    olanın içerisine eklenir.]{type="spanMark"}

3.  [Hesaplanan ]{type="spanMark"}`totalMb`[ ve ]{type="spanMark"}`cnt`[
    değerleri;]{type="spanMark"}

    - [Bilgilendirme mesajlarında,]{type="spanMark"}

    - [Validasyon kontrollerinde,]{type="spanMark"}

    - [Kaydet / Başlat öncesi uyarılarda]{type="spanMark"}

[kullanılabilir.]{type="spanMark"}

::: {contenteditable="false"}

------------------------------------------------------------------------
:::

#### [Örnek Bilgilendirme Mesajı]{type="spanMark"} {#örnek-bilgilendirme-mesajı block-id="mja1n725-bde60b-054"}

``` {.language-javascript block-id="mja27xep-3gigj6-072" language="javascript" custom-title="Custom"}
PwForm.SetAlert("Uyarı",'Eklediğiniz belgelerin toplam boyutu '+ totalMb + ' MB olup '+ cnt + ' adet dosya içermektedir. Maksimum izin verilen ek boyutu aşıldığı için lütfen bazı belgeleri kaldırınız.');
MSG_ERROR =  "Eklediğiniz belgelerin toplam boyutu "+ totalMb + " MB olup "+ cnt + " adet dosya içermektedir. Maksimum izin verilen ek boyutu aşıldığı için lütfen bazı belgeleri kaldırınız.";
```

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-RD4ADN8S.png){.adv-wysiwyg-img
block-id="mja2kja0-bz7yc8-004" mediatype="img" width="auto"
height="auto" dataalign="left" datadisplay="flex"
data-type="media-content" fixaspectratio="false" autoaspectratio="true"
shadow="no" border="no" round="no" link="" newtab=""
style="width:auto;height:auto;"}

::: {contenteditable="false"}

------------------------------------------------------------------------
:::

#### [Notlar ve Öneriler]{type="spanMark"} {#notlar-ve-öneriler block-id="mja1n726-7lg2lg-057"}

- [Kod içerisinde hesaplama **byte** bazında yapılmakta, sonuç **MB**
  cinsine çevrilmektedir.]{type="spanMark"}

- [Limit değerleri kuruma göre özelleştirilebilir.]{type="spanMark"}

- [Kontrol mekanizmasının, mümkünse **kaydetme öncesinde**
  çalıştırılması önerilir.]{type="spanMark"}

#### [Genel Değerlendirme]{type="spanMark"} {#genel-değerlendirme block-id="mja2doh8-emzc6s-073"}

[Bu geliştirme ile birlikte PaperWork üzerinde belge eklerine yönelik
kontrol ve bilgilendirme süreçleri daha şeffaf ve yönetilebilir hale
gelmiştir. Doğru kurgulanmış senaryolar sayesinde hem sistem performansı
korunur hem de kullanıcı kaynaklı hataların önüne
geçilir.]{type="spanMark"}
