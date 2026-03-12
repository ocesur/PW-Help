---
title: "Hesap Tablosu Nesnesi ile Bütçe ve Planlama Formları"
sidebarTitle: "KS-04 Hesap Tablosu"
description: "Formlar içerisinde Excel benzeri satır-sütun yapısında düzenli veri girişi sağlayan tablo nesnesi."
keywords: "hesap tablosu, excel, bütçe formu, tablo veri girişi, kopyala yapıştır, planlama kalemleri, form tasarımı"
---

## Genel Bakış

Hesap Tablosu nesnesi, PaperWork formları içerisinde Excel benzeri satır-sütun yapısında veri girişi yapılmasını sağlar. Bu nesne; çok kalemli ve tablo bazlı bilgilerin tek bir form alanı üzerinden düzenli, okunabilir ve kontrollü şekilde toplanması amacıyla kullanılır.

**Önemli Ayrım:** Hesap Tablosu, karmaşık formüllerle otomatik toplam üretmekten ziyade; yapılandırılabilir kolonlar, zengin biçimlendirme seçenekleri ve **kopyala-yapıştır** desteği ile kullanıcıların tablo verilerini forma hızlıca işlemesine odaklanır.

## Ne Zaman Kullanılmalıdır?

Aşağıdaki durumlarda Hesap Tablosu nesnesinin kullanımı önerilir:

- **Çok Kalemli Veriler:** Bütçe, maliyet veya planlama kalemlerinin tablo halinde girilmesi gerektiğinde.
- **Excel Alışkanlığı:** Excel benzeri kullanım alışkanlığının form içine taşınması istendiğinde.
- **Hızlı Veri Girişi:** Başka bir kaynaktan kopyala-yapıştır yoluyla toplu veri aktarımı hedefleniyorsa.
- **Düzenli Yapı:** Satır ve kolon bazlı, hiyerarşik bir veri toplama ihtiyacı varsa.

## Çalışma Mekanizması

Hesap Tablosu nesnesi, form tasarımı aşamasında eklenir ve projenin ihtiyacına göre özelleştirilir.

**Temel İşleyiş Adımları:**

1. **Yapılandırma:** Form tasarımında satır/kolon sayıları ve kolon başlıkları belirlenir.
2. **Veri Girişi:** Kullanıcı form üzerinde hücrelere veri girer veya Excel'den veri yapıştırır.
3. **Veri Entegrasyonu:** Girilen veriler, form kaydı ile birlikte sistemde saklanır ve sürecin sonraki adımlarında görüntülenebilir.

> Bu yapı sayesinde, tablo verilerini yönetmek için süreçten bağımsız harici dosyalara (Excel, CSV vb.) ihtiyaç duyulmaz.

## Örnek Kullanım Senaryoları

### 1. Bütçe Kalemlerinin Girilmesi

Bütçeye ait gider veya gelir kalemleri satır bazında tabloya işlenir. Her kolon; kalem adı, açıklama veya tutar gibi belirli bir bilgi türünü temsil eder.

### 2. Proje ve Operasyonel Planlama

Projeye ait iş kalemleri ve zaman planlaması tabloya eklenir. Tüm bilgiler süreç boyunca tek noktadan izlenebilir ve güncellenebilir.

### 3. Excel'den Veri Aktarımı

Kullanıcı, Excel üzerinde hazırladığı bir listeyi doğrudan kopyalayıp PaperWork Hesap Tablosu'na yapıştırarak manuel giriş yükünü ortadan kaldırır.

## Sağladığı İş Değeri

- **Dosya Bağımsızlığı:** Süreçlerin harici Excel dosyalarına olan bağımlılığı azalır.
- **Veri Tutarlılığı:** Tablo verileri süreç kaydıyla birleşik şekilde saklanır, kaybolma riski önlenir.
- **Zaman Tasarrufu:** Kopyala-yapıştır desteği ile manuel veri giriş süresi kısalır.
- **Okunabilirlik:** Karmaşık veriler form üzerinde daha düzenli ve taranabilir hale gelir.

## Kritik Notlar

- **Fonksiyon Kısıtı:** Hesap Tablosu nesnesi bir hesaplama motoru değildir; temel amacı **veri toplama ve düzenleme** işlemleridir.
- **Tasarım:** Satır ve kolon limitleri formun performansını etkilememesi adına tasarım aşamasında optimize edilmelidir.