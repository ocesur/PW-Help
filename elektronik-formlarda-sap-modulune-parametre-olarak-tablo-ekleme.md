#### Elektronik Formlarda SAP modülüne Parametre Olarak Tablo Ekleme

SAP'e tablo tipinde veri ekleme fonksiyonumuzu hazırladığımızda
fonksiyonumuzu butondan çağıracak şekilde düzenliyoruz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1680245638780.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

``` {.javascript code-id="section-1680245668680" data-language="javascript"}
function aktar() {
    try {
        var _intsap = PwForm.component('intsap'); // elektronik forma dizayn kısmından eklenen SAP modülümüzün alan adını alacak şekilde değişkene atıyoruz.
        _intsap.setParam('I_AD_SOYAD', PwForm.get('KULLANICI_ADI'));  //parametrelerimizi veriyoruz.
        _intsap.setParam('I_EMAIL', PwForm.get('KULLANICI_MAIL'));
        _intsap.setParam('I_MASRAF_KODU', PwForm.get('MASRAF_KODU'));
        _intsap.setParam('I_DEPO_YERI', PwForm.get('DEPO_YERI_KODU'));
        var rows = PwForm.getRows('SATINALMA_TABLOSU'); // elektronik formumuzda bulunan tabloyu bir değişkene atıyoruz.
        _intsap.removeAllRow('NOTESDATA'); // sap modülünde tutulan ilgili tablomuzun tüm satırlarını siliyoruz.
        //debugger;
        for (var i = 0; i < rows.length; i++) {

            //her döngü işleminde elektronik formumuzda bulunan tablo verilerimizi SAP 'de ki tablomuza aktarıyoruz.
            var itm = _intsap.getNewRow('NOTESDATA');
            itm.DOC_TYPE = rows[i].SAT_BELGE_TURU_NO;
            itm.SHORT_TEXT = rows[i].TMALZEME_ADI;
            itm.QUANTITY = rows[i].SAT_MIKTAR;
            itm.UNIT = rows[i].SAT_OLCU_BIRIMI;
            itm.ACCTASSCAT = rows[i].SAT_HESAP_TAYIN_TIPI;
            itm.PURCH_ORG = rows[i].SAT_ORGANIZASYON_NO;
            itm.PREQ_NAME = PwForm.WorkflowId;
            itm.MAT_GRP = rows[i].SAT_MALZEME_KODU;
            itm.DELIV_DATE = PwForm.moment(rows[i].SAT_TESLIM_TARIHI).format().replaceAll('-', '');
            isUndTable1(itm);
            _intsap.addRow('NOTESDATA', itm); //oluşturulan satır SAP tablosuna ekleniyor.
        }
    }
    catch (wzerror) {
        PwForm.Error(PwForm.Culture("Hata"), wzerror);
    }
}
```
