Formda bulunan nesnelerin "Doğrulama" sekmesinde bulunan "Gelişmiş
Kontrol" alanı üzerisinde verilerin doğrulaması yapılabilmektedir.
Burada konuşacağımız durum ise tablo içerisinde bulunan bir liste
nesnesinin kaydedilen alan üzerisinden doğrulamasıdır.

Tabloda halihazırda bulunan satırların arasında eklenmek istenen liste
değeri bulunuyor ise kaydetme işleminin yapılmaması ve kullanıcıya bir
uyarı mesajı verilmesidir.

İlgili kod şu şekildedir :

``` {.javascript code-id="section-1683098754267" data-language="javascript"}
valid = PwForm.getRows("CUSTOMERS","CUSTOMERNAME",data.CUSTOMERNAME,FilterTYPES.Equal).length > 0) ? false : true;
```

Burada  "CUSTOMERS" tablosunun altında bulunan "CUSTOMERSNAME" kolonu
üzerisinden kontrol yapılmaktadır. Eğer eklenmek istenen liste değeri
halihazırda var ise "Özel Hata Mesajı" alanına yazılan uyarıyı
vermektedir.

Gelişmiş Kontrol alanı içerisinde form arkasında olduğu gibi PwForm
kütüphanesini kullanabilmekteyiz. Burada PwForm kütüphanesi altında olan
"getRows" fonksiyonu sayesinde tablomuzda bulunan verilere
ulaşabilmekteyiz. Ayrıca bu fonksiyon sayesinde filtreleme de
yapılabilmektedir. Burada bu filtreleme özelliği kullanılarak
"CUSTOMERNAME" alanının eklemek istediğimiz veri içeren satırların
uzunluğuna ulaşmaktayız. Eğer bu uzunluk "0" dan büyük ise demek oluyor
ki, bu tabloda ekelemek istediğimiz veri bulunmaktadır. Ve uyarı
vermektedir. 

![](https://cdn.document360.io/e072f215-2317-4c24-b7a8-132a798e9cac/Images/Documentation/image-1683098830313.png){.fr-fic
.fr-fil .fr-dib .fr-bordered .fr-shadow}

\
