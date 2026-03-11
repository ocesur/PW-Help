#### Formda mesajı nasıl verilir?

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/ezgif.com-gif-maker.gif){.fr-fil
.fr-dib}

Örnek kod aşağıdaki gibidir.

``` {.javascript code-id="section-1715076848944" data-language="javascript"}
PwForm.Info("Başlık","mesaj");
```

####  Formda hata mesajı nasıl verilir?

Hata ve uyarı mesajları ekranda aynı görünür. Her 2 metod geri uyumluluk
için bulunur.

``` {.javascript code-id="section-1715076848946" data-language="javascript"}
PwForm.Error("Başlık","mesaj");
```

####  Formda uyarı mesajı nasıl verilir? {#formda-uyarı-mesajı-nasıl-verilir sider-select-id="a7f6b36f-59d3-4354-8eff-cff720ce3c9c"}

Aşağıda warning tipinde mesaj verilmiştir. Diğer tiplerde de mesaj
verilebilir.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/ezgif.com-gif-maker%20(1).gif){.fr-fil
.fr-dib}

``` {.javascript code-id="section-1715077153925" data-language="javascript"}
PwForm.SetAlert("warning","mesaj");// type : warning,info,error,danger
```

[\
]{.code-enhance-copy-9TQ90J
style="--tw-border-spacing-x: 0; --tw-border-spacing-y: 0; --tw-translate-x: 0; --tw-translate-y: 0; --tw-rotate: 0; --tw-skew-x: 0; --tw-skew-y: 0; --tw-scale-x: 1; --tw-scale-y: 1; --tw-scroll-snap-strictness: proximity; --tw-ring-offset-width: 0px; --tw-ring-offset-color: #fff; --tw-ring-color: rgba(59, 130, 246, .5); --tw-ring-offset-shadow: 0 0 #0000; --tw-ring-shadow: 0 0 #0000; --tw-shadow: 0 0 #0000; --tw-shadow-colored: 0 0 #0000; box-sizing: border-box; display: inline-flex; cursor: pointer; align-items: center; gap: 6px; font-size: 12px; word-spacing: -4px;"}

``` {style="--tw-border-spacing-x: 0; --tw-border-spacing-y: 0; --tw-translate-x: 0; --tw-translate-y: 0; --tw-rotate: 0; --tw-skew-x: 0; --tw-skew-y: 0; --tw-scale-x: 1; --tw-scale-y: 1; --tw-scroll-snap-strictness: proximity; --tw-ring-offset-width: 0px; --tw-ring-offset-color: #fff; --tw-ring-color: rgba(59, 130, 246, .5); --tw-ring-offset-shadow: 0 0 #0000; --tw-ring-shadow: 0 0 #0000; --tw-shadow: 0 0 #0000; --tw-shadow-colored: 0 0 #0000; box-sizing: border-box; margin: 0px 0px 16px; padding: 0px; overflow: auto; font-family: ui-monospace, SFMono-Regular, \"SF Mono\", Menlo, Consolas, \"Liberation Mono\", monospace; font-size: 11.9px; overflow-wrap: normal; line-height: 1.45; background-color: rgb(255, 255, 255); border-radius: 6px;"}
Formda "Başarılı Olundu" Mesajı  Verme
```

Aşağıda [formunuzda bir tuş nesnesi aracılığıyla  \"Başarılı Olundu\"
mesajı vermenin nasıl yapılacağını
öğreneceksiniz.]{sider-select-id="581994b5-6bae-4265-8675-46a5292f77f9"
style="color: rgb(34, 34, 34); font-family: Inter, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: pre-wrap; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}

[]{sider-select-id="581994b5-6bae-4265-8675-46a5292f77f9"
style="color: rgb(34, 34, 34); font-family: Inter, sans-serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: left; text-indent: 0px; text-transform: none; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; white-space: pre-wrap; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial; display: inline !important; float: none;"}

::: fr-img-space-wrap
[[![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1715078100765.png){.fr-fic
.fr-fil .fr-dii .fr-shadow .fr-bordered}[\
]{.fr-inner sider-insert-id="9523a426-f12a-44f9-9aac-092943322dcf"
sider-select-id="35621747-7f3b-4c3e-85c4-91252ad88da5"}]{.fr-img-wrap}]{.fr-img-caption
.fr-fic .fr-fil .fr-dii .fr-shadow .fr-bordered style="width: 1098px;"}

 

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

\

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1715078251284.png){.fr-fic
.fr-fil .fr-dib}

``` {.javascript code-id="section-1715078278024" data-language="javascript"}
PwForm.Success("Başarılı Olundu","Açılan pencerenin rengi yeşil");
```
:::
