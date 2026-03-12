---
title: "QR Kod ve Barkod Okuyucu ile Akıllı Saha Operasyonları"
sidebarTitle: "KS-01 QR Kod & Barkod Okuyucu"
description: "Fiziksel varlıklar ile dijital süreçleri birbirine bağlayan, mobil cihaz tabanlı veri girişi ve süreç başlatma rehberi."
keywords: "qr kod, barkod okuyucu, mobil süreç, saha operasyonu, makine bakım, döküman tetikleme, envanter yönetimi"
---

## Genel Bakış

**QR Kod ve Barkod Okuyucu**, PaperWork form ve süreçlerinde fiziksel varlıklar (makine, ekipman, ürün, lokasyon) ile dijital iş akışları arasında hızlı, hatasız ve mobil odaklı bir köprü kurar. Bu nesne sayesinde kullanıcılar, karmaşık seri numaraları veya makine kodlarını manuel girmek yerine, cihaz kamerasını kullanarak saniyeler içinde doğru süreci başlatabilir.

Özellikle üretim tesisleri, depolar ve saha operasyonlarında manuel veri girişinden kaynaklanan hataları sıfıra indirmek ve operasyonel hızı artırmak amacıyla kullanılır.

## Ne Zaman Kullanılmalıdır?

Aşağıdaki senaryolarda QR/Barkod entegrasyonu yüksek verimlilik sağlar:

- **Varlık Bazlı Süreçler:** Belirli bir makine veya ekipmanla ilişkili bakım, arıza veya denetim süreçleri yürütülüyorsa.
- **Hızlı Veri Girişi:** Seri numarası, IMEI, ürün kodu gibi manuel yazımı zor ve hataya açık verilerin okunması gerekiyorsa.
- **Çoklu Süreç Tetikleme:** Aynı varlık (QR kod) üzerinden farklı kullanıcıların farklı süreçler (Bakım, Arıza, Talep vb.) başlatması hedefleniyorsa.
- **Saha ve Depo Yönetimi:** Klavye kullanımının zor olduğu üretim veya depo ortamlarında pratik giriş yöntemleri aranıyorsa.

## Çalışma Mekanizması

QR Kod ve Barkod Okuyucu nesnesi, PaperWork mobil uygulaması üzerinden cihaz kamerasını tetikleyerek çalışır.

**İşleyiş Adımları:**

1. **Tarama:** Kullanıcı form üzerindeki okuyucu nesnesine dokunarak kodu taratır.
2. **Eşleştirme:** Okunan kod, sistemdeki ilgili kayıtla (Makine kartı, Ürün kartı vb.) otomatik olarak eşleştirilir.
3. **Veri Entegrasyonu:** Kodla ilişkili tüm bilgiler (Marka, model, garanti durumu vb.) form alanlarına otomatik dolar.
4. **Süreç Başlatma:** Kullanıcı, o varlık için tanımlanmış uygun iş akışını seçerek süreci başlatır.

## Örnek Kullanım Senaryoları

### 1. Üretimde Akıllı Bakım Bildirimi

Bakım teknisyeni makine üzerindeki QR kodu okutur. Makine bilgileri otomatik gelir. Teknisyen "Periyodik Bakım" seçeneğini işaretlediğinde, ilgili iş emri akışı o makineye özel parametrelerle başlatılır.

### 2. Anlık Arıza ve DÖF Bildirimi

Operatör, arızalanan ekipmanın QR kodunu taratır. Arıza fotoğrafını ve sesli notunu ekleyerek "Arıza Bildir" butonuna basar. Düzeltici Önleyici Faaliyet (DÖF) süreci konum bilgisiyle birlikte anında ilgili birime düşer.

### 3. Dinamik Sarf Malzeme Talebi

Makine üzerindeki kod okutulduğunda, sadece o makineye uygun sarf malzemeler listelenir. Yanlış parça talep etme riski ortadan kalkarak satın alma veya depo çıkış süreci doğru verilerle başlar.

## Sağladığı İş Değeri

- **Sıfır Hata:** Yanlış makine veya ürün seçimine bağlı operasyonel hatalar engellenir.
- **Maksimum Hız:** Manuel giriş süreleri ortadan kalkar, sahada form doldurma süresi %90 oranında kısalır.
- **Tek Merkezden Çoklu Süreç:** Tek bir fiziksel QR kod, yetkilere göre onlarca farklı sürecin (Bakım, Envanter, Arıza, Denetim) giriş kapısı haline gelir.
- **İzlenebilirlik:** Fiziksel varlık ile dijital kayıt arasındaki ilişki kopmaz bir bağla kurulur; hangi makineye ne zaman müdahale edildiği netleşir.

## Teknik Notlar

- **Donanım:** Bu özellik mobil cihazların (iOS/Android) kamera donanımını kullanır.
- **Format Desteği:** Piyasada yaygın olarak kullanılan tüm QR ve Barkod standartları (EAN, Code 128, QR vb.) desteklenir.
- **Çevrimdışı Çalışma:** Tarama sonrası veri çekme işlemi için internet bağlantısı gereklidir (Entegrasyonun çalışması adına).

---

**İpucu:** QR kod okutulduktan sonra "Lokasyon (Harita) Nesnesi" ile kullanıcının gerçekten o makinenin başında olup olmadığını doğrulayabilir, saha denetimlerinizi %100 güvenli hale getirebilirsiniz.