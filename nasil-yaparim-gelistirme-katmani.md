#### Formda aktif kullanıcı bilgilerini nasıl kullanırım?

 CurrentUser nesnesi aktif kullanıcı bilgilerini içerir.

``` {.csharp code-id="section-1658999617492" data-language="csharp"}
{
    "UserName": "Serdar Kul",
    "UserLogin": "skul",
    "ServerInfo": "T|T|T|T|T|F|T|T|T|T|T|T|T|T|T|T|T|T|T|T|T|F|T",
    "Platform": "DEVELOPMENT",
    "CustomerName": "",
    "UserEmail": "skul@paperwork.com.tr",
    "UserPosition": "MUDUR",
    "UserTitle": "Kıdemli Yazılım Geliştirme Uzmanı",
    "Culture": "TR",
    "CurrentApp": "Mvc",
    "ExtProp1": "32843915",
    "ExtProp2": "YAZILIM",
    "ExtProp3": "32843915",
    "ExtProp4": "",
    "ExtProp5": "",
    "ExtProp6": "",
    "ExtProp7": "",
    "ExtProp8": "Müdür",
    "ExtProp9": "",
    "ExtProp10": "",
    "ExtProp11": "",
    "ExtProp12": "",
    "ExtProp13": "",
    "ExtProp14": "",
    "ExtProp15": ""
}
```

#### Formda form nesnesini nasıl kullanırım?

[PwForm ]{.underline}nesnesi ile ulaşılır. PwForm.form web form
nesnesidir.  Aşağıdaki metodları içerir.

1.  AclId: (\...) : Nesne numarası oluşmuş akış, kabinet kaydı veya
    dosya kartı kaydının yetki setini verir
2.  AddRow: ƒ (compName) : Veri kaynağına satır eklenmesi için popup
    ekranını açar.
3.  AddRowData: ƒ (compName, data) : Veri kaynağına verilen JSON Array
    türündeki datayı ekler
4.  AddRowDataFull: ƒ (compName, data): Veri kaynağının datası temizler,
    verilen JSON Array türündeki datayı ekler
5.  AttorneyId: (\...) : Vekealet verilen akışın vekalet numarasını
    verir
6.  CardId: (\...) : Dosya kartı formunda kaydın nesne numarasını verir
7.  Complete: ƒ () : Akışın mmanuel adımının tamamlanmasığı sağlar
8.  CopyClipBoard: ƒ CopyClipBoard(text) : Verilen yazıyı panoya
    kopyalar
9.  Counter: ƒ (counterName, attribute, regex) : Verilen sayaç adı ile
    belirtilen alana sayaç numarasını set eder
10. DeleteAll: ƒ (compName) : Veri kaynağındaki tüm satırları temizler
11. DeleteRow: ƒ (compName) :  Veri kaynağındaki seçili satırı siler
12. DeleteRowAt: ƒ (compName, index) :  Veri kaynağındaki satır numarası
    verilen satırı siler
13. EditRow: ƒ (compName) : Veri kaynağında satır düzenlemesi için popup
    ekranını açar.
14. EditRowAt: ƒ (compName, index) :  Veri kaynağındaki satır numarası
    verilen satırı düzenler
15. Error: ƒ (title, message): Başlık ve içeriği verilen hata mesajını
    popup olarak açar
16. ExecSql: async ƒ (aSql, aPlugin): SQL sorgusunu çalıştırmak için
    kullanılır
17. ExecuteMethod: async ƒ (aMethod, aParamList): Tanımlı metodu
    tetikletmek için kullanılır
18. FormId: (\...) : Formun nesne numarasını verir
19. FormName: (\...) : Formun nesne adını verir
20. GetComboSelectedRow: ƒ (comp) : Belirtilen liste nesnesinin seçili
    satırının datasını verir
21. GetComponent: ƒ (root, key) : Id si verilen nesneyi döner
22. IsNullOrEmpty: ƒ (value) : Bir değerin boş veya null olmasını
    kontrol eder
23. LoadForm: async ƒ (index, formName, parent, isForm) : Nesne adı
    verilen formun yüklenmesini sağlar
24. LoadRuleEngine: ƒ () : Kural motorunun yüklenmesini sağlar
25. Log: ƒ (msg,msg2) : Paperwork.Log dosyasına log basmasını sağlar
26. MasterData: (\...) : Akış eklentisinin sistemde kayıtlı bilgisini
    döner
27. MoveDown: ƒ (compName) : Veri kaynağında seçili satırı bir alt
    satıra kaydırır
28. MoveUp: ƒ (compName): Veri kaynağında seçili satırı bir üst satıra
    kaydırır
29. NewRow: ƒ (compName) : Veri kaynağında JSON Array türünde yeni boş
    bir satır kaydı oluşturur
30. ObjectId: (\...) : Kaydın nesne numarasını verir
31. ObjectName: (\...): Kaydın nesne adını verir
32. ProcessId: (\...) : Akışın süreç numarasını (ProcessId) verir
33. Progress: ƒ (isVisible) : Bekleme durumlarında Hourglass çıkmasını
    ve kaybolmasını sağlar
34. Query: async ƒ (aSql, aPlugin, TableId) : SQL sorgusunu çalıştırmak
    için kullanılır
35. SetAlert: ƒ (type, message) : Uyarı mesajı çıkartır. (Hata, Uyarı,
    Bilgi türünde)
36. ShowConfirmPopup: ƒ (title, message, onSuccess, onError) : Onay
    popup ekranını açar
37. ShowPromptPopup: ƒ (title, message, defaultValue, dataType,
    onSuccess, onError)
38. Sum: ƒ (groupName, columnName, filterColumn, filterValue,
    filterType) : Veri kaynağında belirtilen kolonda filtreye bağlı yada
    filtresiz toplamının alınmasını sağlar
39. TypeName: (\...) : Tip bilgisini döner
40. WorkflowId: (\...) : Manuel adım formu ise akış numarasını döner
41. WorkitemId: (\...) : Manuel adım formu ise adım numarasını döner
42. closeDialog: ƒ (gridName) : Açılan dialog nesnesini kapatır
43. component: ƒ (compName) : Adı verilen nesneyi verir
44. copy: ƒ (source, destination, map) : Eşelştirmesi yapılmış alanların
    datalarının kopyalanmasını sağlar
45. countRow: ƒ (groupName) : Veri kaynağındaki satır sayısını verir
46. counter_sync: async ƒ (counterName) : Adı verilen sayaçın değerini
    döner
47. deleteRows: ƒ (groupName, filterColumn, filterValue, filterType) :
    Veri kaynağında belirtilen kolonda filtreli yada filtresiz bulunan
    satırları siler
48. disableTab: ƒ (compName, index,isDisable) : Sekme nesnesinin
    görünürlüğünü ayarlar
49. enable: ƒ (compName, isEnable) : Adı verilen nesneyi salt okunur
    olmasını yada olmamasını sağlar
50. fillComboJson: ƒ (component, data, valueKey, displayKey) :
    Belirtilen liste nesnesini verilen JSON türündeki data ile doldurur
51. fillComboWithPL: ƒ (aMethod, component, valueKey, displayKey,
    isJson)  : Belirtilen liste nesnesini tetiklenen metod ve metoddan
    dönen data ile doldurur
52. fillComboWithSql: ƒ (aSql, component, aPlugin, valueKey, displayKey,
    isJson) : Belirtilen liste nesnesini sql sorgusundan dönen data ile
    doldurur
53. fillGrid: ƒ (gridName, data, headers) : Veri kaynağını verilen data
    ile doldurur
54. fillIntGrid: ƒ (gridName, intCompName, resultElementName, headers) :
    Veri kaynağını entegrasyon datası ile doldurur
55. fillIntList: ƒ (compName, key, label, intCompName,
    resultElementName) : Listeyi entegrasyon datası ile doldurur
56. fillList: ƒ (listName, key, label, arrayName) : Listeyi verilen data
    ile doldurur
57. fillTypeFields: ƒ (aTypeName) : Tip adı verilen tipin alanlarını
    döner
58. focus: ƒ (compName): Belirtilen nesneye odak yapılır
59. formDialog: ƒ (dialogName, formName, afterLoad, afterSave) : Form
    adı verilen formu dialog nesnesinde açar
60. get: ƒ (compName) : Belirtilen nesnenin datasını döner
61. getComboLabel4Grid: ƒ (gridName, columnName, key) : Veri kaynağı
    içindeki listenin başlığını döner
62. getIntData: ƒ getIntData(compName) : Form üzerinde tanımlı
    entegrasyon nesnesinin datasını döner
63. getIntHeader: ƒ getIntHeader(compName, elementName) : : Form
    üzerinde tanımlı entegrasyon nesnesinin başlık bilgisini döner
64. getRow: ƒ (groupName, index) : Veri kaynağında Index bilgisi verilen
    satırı döner
65. getRowValue: ƒ (groupName, columnName, index) : Veri kaynağında
    Index bilgisi ve kolon bilgisi verilen alanın değerini döner
66. getRows: ƒ (groupName, filterColumn, filterValue, filterType) : Veri
    kaynağın belirtilen kolon ile filtrelenmiş datasını döner
67. getSelectedRows: ƒ (compName) : Veri kaynağında seçili satırların
    listesini döner
68. hideTab: ƒ (compName,index) : Sekme nesnesinin belirtilen indexli
    sekmesinin gizlenmesini sağlar
69. isCard: (\...) : Dosya kartı kaydı olu olmadığının bilgisini döner
70. isDesign: ƒ () : Formun ön izleme ekranında açılıp açılmadığını
    döner
71. isEnable: ƒ (compName) : Belirtilen nesnenin erişilip
    erişilmediğinin bilgisini döner
72. isNew: ƒ () : Formun ilk defa açıldığının bilgisini döner
73. isReadOnly: ƒ (compName) : Belirtilen nesnenin salt okunur olup
    olmadığını döner
74. isRequired: ƒ (compName) : Belirtilen nesnenin zorunlu olup
    olmadığını döner
75. isShow: ƒ (compName) : Belirtilen nesneyi görünüp görünmediğinin
    bilgsini döner
76. isTabEnable: ƒ isTabEnable(compName, index)  : Belirtilen sekme
    nesnesinin erişilip erişilmediğinin bilgisini döner
77. isTabVisible: ƒ (compName, index) : Belirtilen sekme nesnesinin
    görünüp görünmediğinin bilgsini döner
78. jsonDate2Date: ƒ (dt) : Json formatındaki tarih bilgisini normal
    tarih türüne dönüştürür
79. moment: ƒ () : Tarih fonksiyonlarını içeren kütüphane
80. openDocument: ƒ (dialogName, htmlName, objectId, readonly = true) :
    Nesne numarası verilen dokümanı popup olarak açar
81. pasteEnable: ƒ (controlName) : Veri kaynağına paste özelliğini açmak
    için kullanılır. ControlName:tablo adıdır.
82. pasteDesable: ƒ (controlName) : Veri kaynağına paste özelliğini
    kapatmak için kullanılır. ControlName:tablo adıdır.
83. openDialog: ƒ (dialogName, gridName, dialogType, data, headers) :
    Belirtilen dialog nesnesinin verilen data ile açılmasını sağlar
84. readOnly: ƒ (compName, isReadOnly) : Belirtilen nesnenin salt okunur
    olmasını yada olmamasını sağlar
85. removeAllRow: ƒ (groupName) : Veri kaynağındaki tüm satırları siler
86. removeRow: ƒ (groupName, index) : Veri kaynağındaki Index bilgisi
    verilen satırı siler
87. required: ƒ (compName, isRequired) : Belirtilen nesneyi zorunlu
    yapar yada zorunluluğunu kaldırır
88. rowSet: ƒ (row, column, value) : Veri kaynağında belirtilen satırın
    belirtilen kolonundaki datasını günceller
89. set: ƒ (compName, value) : Belirtilen nesnenin datasını günceller
90. setEvent: ƒ (compName, event, func) : Belirtilen nesne için olay
    tanımlar
91. setRow: ƒ (groupName, index, row) : Veri kaynağında belirtilen
    satırın datasını günceller
92. setRowValue: ƒ (groupName, columnName, index, value): Veri
    kaynağında belirtilen kolonun belirtilen indexindeki datasını
    günceller
93. setTab: ƒ (compName,index) : Belirtilen sekme nesnesinin verilen
    indexi görünen sekmesi yapar
94. show: ƒ (compName, isVisible) : Belirtilen nesneyi gösterir yada
    gizler
95. showTab: ƒ (compName,index) : Belirtilen sekmenin belirtilen
    indexini gösterir
96. webService: async ƒ (aServiceName, aMethodName, aInputs) :  Tanımlı
    web servisin tetiklenmesini sağlar
