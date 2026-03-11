#### PwForm.getPL fonksiyonunun url parametresi nasıl belirlenir?

Form arkası kodlarda PwForm.getPL ile productivity layer çağrısı
yaparken verilmesi gereken url parametresinin formatı önceden belirli
bir şekile uygun olmalıdır.

Örnek url: /Services/Ado/Query

Yukarıdaki örnekteki gibi getPL fonksiyonuna verdiğimiz url 3 parçadan
oluşmaktadır. İlk parçası üzerinde herhangi bir değişiklik yapılmamalı.
İkinci parçada metodu kapsayan RemObject sınıfını, üçüncü parçada ise
metodun adını yazıyoruz. 

SDK Dökümantasyonu üzerinden örneklersek eğer şu şekilde yol izlemeliyiz
:

SDK üzerinden sistemde tanımlı yetki setlerini getirmek için GetACLS
metotunu kullanmak istediğimizi varsayalım.

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1711960256522.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

RemLookup sınıfı içerisinde GetACLs ismiyle bulunduğunu SDK dökümanı
üzerinde gördük.

Sınıf ismindeki Rem ibaresini URL içine dahil etmeden kullandığımızda
doğru URL belirlemiş oluyoruz.

Oluşan PwForm.getPL URL parametresi şu şekilde olacaktır :
**/Services/Lookup/GetACLs**

\
