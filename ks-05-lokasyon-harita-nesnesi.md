---
title: "Lokasyon (Harita) Nesnesi ile Saha ve Konum Bazlı Süreçler"
sidebarTitle: "KS-05 Lokasyon ve Harita"
description: "Saha operasyonlarında Google Haritalar entegrasyonu ile coğrafi konum verisi toplama rehberi."
keywords: "harita nesnesi, google maps api, konum seçme, saha operasyonu, lokasyon bazlı bildirim, gps, adres doğrulama"
---

## Genel Bakış

Lokasyon (Harita) nesnesi, PaperWork formları üzerinde coğrafi konum bilgisinin interaktif bir harita üzerinden seçilmesini sağlar. Kullanıcılar, Google Haritalar altyapısı üzerinden arama yaparak veya harita üzerindeki imleci manuel olarak hareket ettirerek ilgili konumu belirleyebilir.

Bu nesne; saha denetimi, teknik servis bakımı, keşif süreçleri ve lokasyon bazlı arıza bildirimleri gibi senaryolarda adres bilgilerinin standart ve hatasız toplanması amacıyla kullanılır.

## Ne Zaman Kullanılmalıdır?

Aşağıdaki durumlarda Lokasyon (Harita) nesnesinin kullanımı önerilir:

- **Saha Operasyonları:** Dış lokasyonlu çalışmaların koordinasyonu gerektiğinde.
- **Adres Doğrulama:** Konum bilgisinin manuel yazım hatalarından arındırılıp harita üzerinden kesinleştirilmesi istendiğinde.
- **Denetim ve Keşif:** Belirli bir noktanın coğrafi koordinatlarıyla kayıt altına alınması gereken süreçlerde.
- **Görsel İzleme:** Harita destekli raporlama ve saha takibi hedeflendiğinde.

## Teknik Çalışma Mekanizması

Lokasyon nesnesi, Google Haritalar servislerini kullanarak çalışır ve form tasarımı aşamasında yapılandırılır.

**Kurulum ve İşleyiş Adımları:**

1. **Veri Bağlantısı:** Lokasyon nesnesi, "Yazı" veri tipindeki bir tip alanına (database field) bağlanır.
2. **Google Cloud Yapılandırması:** Google Cloud Console üzerinden gerekli **API Anahtarı (API Key)** ve **Map ID** bilgileri temin edilir.
3. **Entegrasyon:** Alınan API Key ve Map ID, PaperWork form nesnesi özelliklerine girilir.
4. **Veri Girişi:** Kullanıcı form üzerinde harita aracılığıyla konum seçimini yapar; seçilen koordinatlar sistemde saklanır.

## Örnek Kullanım Senaryoları

### 1. Saha Arıza ve Bakım Bildirimleri

Teknik personel, arıza veya bakım yapılacak noktayı harita üzerinden seçer. Bu sayede saha ekibi, açıklama satırlarına ihtiyaç duymadan doğrudan doğru konuma yönlendirilir.

### 2. Denetim ve Keşif Süreçleri

Keşif yapılan alan harita üzerinde işaretlenir. Denetim raporları bu lokasyon verisiyle ilişkilendirilerek geçmişe dönük coğrafi analiz yapılmasına olanak tanır.

### 3. İSG ve Uygunsuzluk Bildirimleri

Fabrika veya saha içerisinde tespit edilen riskli noktalar işaretlenir. İSG uzmanları, harita üzerindeki yoğunlaşmaya göre riskli bölgeleri daha net analiz edebilir.

## Sağladığı İş Değeri

- **Hata Payının Azalması:** Adres ve konum bilgilerindeki yazım/yorum hataları tamamen ortadan kalkar.
- **Hızlı Müdahale:** Saha süreçlerinde doğru lokasyona en kısa sürede erişim sağlanır.
- **Gelişmiş Raporlama:** Bildirimler coğrafi verilerle zenginleştirilerek harita bazlı dashboard'lara veri sağlar.
- **Şeffaflık:** Saha ekipleri ve merkez arasındaki bilgi akışı somut konumlara dayandırılır.

## Kritik Teknik Notlar

- **API Gereksinimi:** Google Cloud Map API ücretli bir servistir ve kullanım bazlı faturalandırılır. API anahtarı olmadan harita yüklenmeyecektir.
- **Güvenlik (CSP):** `Web.config` dosyasındaki _Content Security Policy_ ayarlarında Google domainlerine gerekli izinlerin verilmiş olması şarttır.
- **Veri Tipi:** Nesne sadece "Yazı" veri tipindeki alanlarla tam uyumlu çalışır.

> **İpucu:** Bu nesneyi "Fotoğraf/Video Kaydı" nesnesiyle birlikte kullanarak saha bildirimlerini hem görsel hem de coğrafi olarak kanıtlanabilir hale getirebilirsiniz.