Bu rehber, [Kural
Motoru](/tr/docs/a5x070404000#kural-motorunun-hazır-fonksiyonları){target="_self"
translate="no"}'nda tanımlanan değerlerin iş süreçlerinde ve formlarda
nasıl kullanılacağını standart kod bloklarıyla açıklar.

------------------------------------------------------------------------

## 1. Değişkenler (Variables) - Sistem Parametreleri {#değişkenler-variables---sistem-parametreleri block-id="mjn7174f-j95i0g-016" path-to-node="6"}

**Senaryo:** Uygulamanın bağlandığı bir dış servis adresi (ERP veya
Müşteri Servisi) ve uygulamanın \"Bakım Modu\" bilgisinin merkezi olarak
yönetilmesi.

### **C# (İş Akışı / Makro)** {#c-iş-akışı-makro block-id="mjn7174g-72freq-018" path-to-node="8"}

``` {.language-csharp block-id="mjn6x2jg-49v9e9-007" language="csharp" custom-title="Custom"}
try {
    LoadRuleEngine(); // Kural motorunu yükle
    
    // Değişkenler sekmesinden "BakimModu" değerini oku
    string isMaintenance = RuleEngine.BakimModu; 

    if (isMaintenance == "EVET") {
        Log("Sistem bakım modunda. Akış durduruluyor.");
        // Gerekli yönlendirme mantığı...
    }
} catch(Exception ex) {
    Log("HATA! Değişken Okuma: " + ex.Message);
    throw;
}
```

### **JS (Form / Web SDK)** {#js-form-web-sdk block-id="mjn70iwg-k5avan-014" path-to-node="15"}

``` {.language-javascript block-id="mjn6ytrc-v27bd3-010" language="javascript" custom-title="Custom"}
function checkServiceUrl() {
    // Kural motorundaki "MusteriSorguURL" değişkenine doğrudan erişim
    var apiUrl = ruleEngine.MusteriSorguURL;

    if (!apiUrl) {
        PwForm.Error("Hata", "API bağlantı adresi tanımlı değil!");
        return;
    }
    // API çağrısı işlemleri...
}
```

## 2. Listeler (Lists) - Seçim ve UI Mantığı {#listeler-lists---seçim-ve-ui-mantığı block-id="mjn708so-url99e-011" path-to-node="13"}

**Senaryo:** Formdaki bir \"Ödeme Tipi\" listesine göre, ek belgelerin
yüklenmesinin zorunlu kılınması.

### **JS (Form / Web SDK)** {#js-form-web-sdk-1 block-id="mjn708sp-4uidth-013" path-to-node="15"}

``` {.language-javascript block-id="mjn71jdz-kdm29v-019" language="javascript" custom-title="Custom"}
function onOdemeTipiChange() {
    var secilenTip = PwForm.get("ODEME_TIPI");

    // Listeler sekmesindeki "KrediKarti" değerine göre kontrol
    if (secilenTip === "Kredi Kartı") {
        PwForm.setRequired("PROVIZYON_KODU", true);
        PwForm.Info("Bilgi", "Kredi kartı seçildiği için provizyon kodu zorunludur.");
    } else {
        PwForm.setRequired("PROVIZYON_KODU", false);
    }
}
```

## 3. Fonksiyonlar (Functions) - Hesaplama ve Doğrulama {#fonksiyonlar-functions---hesaplama-ve-doğrulama block-id="mjn74fp1-26uqyc-020" path-to-node="18"}

**Senaryo:** Verilen bir tarihin üzerine, sistem takvimindeki tatilleri
atlayarak 3 iş günü ekleyen bir SLA hesaplama fonksiyonu.

### **C# (İş Akışı / Makro)** {#c-iş-akışı-makro-1 block-id="mjn74fp3-f2e8vn-022" path-to-node="20"}

``` {.language-csharp block-id="mjn74j7y-pizhgz-023" language="csharp" custom-title="Custom"}
try {
    LoadRuleEngine();
    DateTime baslangic = (DateTime)PwForm.get("TALEP_TARIHI");

    // Fonksiyonlar sekmesinde tanımlı 'IsGunuEkle' metodunu çağır
    // Parametreler: TakvimAdı, Tarih, GünSayısı
    DateTime termin = RuleEngine.IsGunuEkle("Merkez_Takvim", baslangic, 3);

    PwForm.set("TERMIN_TARIHI", termin);
    Log("Termin hesaplandı: " + termin.ToShortDateString());
} catch(Exception ex) {
    Log("HATA! Termin Hesaplama: " + ex.Message);
}
```

## Notlar {#notlar block-id="mjn7hi8i-xbov3p-024" path-to-node="28"}

1.  **Bakım Kolaylığı:** Statik değerleri (Mail adresleri, URL\'ler,
    Limitler) asla kodun içine yazmayın. Bunları her zaman
    **Değişkenler** sekmesinde tanımlayın.

2.  **Merkezi Yönetim:** Aynı hesaplama mantığı birden fazla akışta
    kullanılıyorsa, bunu **Fonksiyonlar** sekmesine taşıyarak tek bir
    yerden güncelleyin.

3.  **Performans:** Tablo sorgularında `SELECT *`{path-to-node="29,2,0"
    index-in-node="31"} yerine sadece ihtiyacınız olan
    `SELECT ONAYCI_EPOSTA`{path-to-node="29,2,0" index-in-node="71"}
    gibi sütunları çağırın.

4.  **Güvenlik:** JS tarafında `debugger;`{path-to-node="29,3,0"
    index-in-node="23"} komutunu geliştirme bittikten sonra canlıya
    alırken mutlaka kaldırın.
