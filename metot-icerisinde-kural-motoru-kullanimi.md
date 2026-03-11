#### Metot İçerisinde Kural Motoru Kullanımı

Kural motorunu kullanabilmek için öncelikle metot içerisine ilgili
kütüphanelerin eklenmesi gerekir.

``` {.csharp code-id="section-1687519169653" data-language="csharp"}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Paperwork.Methods;
using Paperwork.Library;
 
using System.Data;
using ContentServer;
using Paperwork.Types;
using System.Reflection;
using System.Globalization;
using System.Collections.ObjectModel;
using System.IO;
using System.Xml;
```

Örnekleyebilmek için bir kural motoru tablosu hazırlıyoruz :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687519206975.png){.fr-fic
.fr-fil .fr-dib .fr-shadow .fr-bordered}

Kural motoru fonksiyonumuz da şu şekilde :

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687519234038.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

Metot içerisinde kural motorunu çağırmak için gerekli yapı şu şekilde:

``` {.csharp code-id="section-1687520795375" data-language="csharp"}
AssemblyItem ai = server.rAssembly.GetAssembly("MainRule.dll", "CURRENT", "RULE.NET");
Assembly assembly = Assembly.Load(ai.Data);
dynamic ruleEngine = assembly.CreateInstance("Paperwork.Library.MainRule");
```

Referans kütüphanelerimiz ekleyip bu yapıyı kurduktan sonra ruleEngine.
İle kural motorumuz içindeki değişkenler, listeler, tablolar ve
fonksiyonlara ulaşabilir oluyoruz. Yukarıda gördüğünüz kural motoru
tablosunun satır ve sütunlarına ulaşmak istersek şu şekilde
çağırabiliriz:

``` {.csharp code-id="section-1687520915368" data-language="csharp"}
var paperRuleEngine = ruleEngine.tablePaperWork.Rows[2][1]; 
var workRuleEngine = ruleEngine.tablePaperWork.Rows[0][1];
```

ruleEngine.tablePaperWork.Rows bize 2 boyutlu bir dizi dönecektir.
Vereceğimiz ilk indeks satır(row), ikinci indeks ise sütun(column)
değerlerini ifade eder. Satırlar(row) için her zaman indeks vermemiz
gerekir fakat sütunlar(column) için isim vererek de çağırabiliriz;

``` {.csharp code-id="section-1687520947554" data-language="csharp"}
var paperProduct = ruleEngine.tablePaperWork.Rows[2]["Product"]; 
var workProduct = ruleEngine.tablePaperWork.Rows[0]["Product"];
```

Metod içinde çağırılmış kural motorunun örneğini tek görsel ile şu
şekilde anlayabiliriz.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1687521002353.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
