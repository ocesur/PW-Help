Elektronik formlar üzerindeki sekmeler ile ilgili fonksiyonlar bu
sayfada açıklanmıştır. Yapılan işlemlerin videosu aşağıdaki gibidir.

1.Videoya göre elektronik form üzerine Sekme Nesnesi eklenmiş ve 3 sekme
oluşturulmuştur.

2.Sekmelerin üzerine tuşlar yerleştirilmiş ve her birine bir fonksiyon
bağlanmıştır.

3.Global fonksiyonlar bölümünde de fonksiyonlar kodlanmıştır.
Fonksiyonlar aşağıdaki gibidir.

\

::::: {.section .warningBox}
::: title
Dikkat !
:::

::: content
Sekme indeksi 0\'dan başlamaktadır.
:::
:::::

\

``` {.javascript code-id="section-1661457662954" data-language="javascript"}
function hideTab() {
    PwForm.hideTab("pwtabs", 1);
}

function showTab() {
    PwForm.showTab("pwtabs", 1);
}

function disableTab() {
    PwForm.disableTab("pwtabs", 2, true);
}

function enableTab() {
    PwForm.disableTab("pwtabs", 2, false);
}

function isVisible() {
    var res = PwForm.isTabVisible("pwtabs", 1);
    PwForm.SetAlert('danger', "" + res);
}

function isEnable() {
    var res = PwForm.isTabEnable("pwtabs", 2);
    PwForm.SetAlert('danger', "" + res);
}

function disable() {
    PwForm.show("pwtabs", false);
}

function show() {
    PwForm.show("pwtabs", true);
}

function currentTab() {
    alert(PwForm.component("pwtabs").currentTab);
}
```
