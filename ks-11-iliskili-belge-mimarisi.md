---
title: "İlişkili Belge Mimarisi ile Doküman Ağı Oluşturma"
sidebarTitle: "KS-11 İlişkili Belge Mimarisi"
description: "PaperWork üzerinde belgeler arasında anlamlı bağlar kurarak döküman ekosistemi oluşturma rehberi."
keywords: "ilişkili belge mimarisi, döküman ağı, otomatik ilişkilendirme, manuel ilişkilendirme, kabinet tanımları, belge ekosistemi"
---

## Genel Bakış

**İlişkili Belge Mimarisi**, PaperWork platformunda arşivlenen belgeler arasında mantıksal ve operasyonel bağlar kurulmasını sağlar. Bu mimari sayesinde, birbirini tamamlayan dokümanlar (Örn: Sözleşme, Fatura ve İrsaliye) anlamlı bir doküman ağı içerisinde yönetilir. Kullanıcılar, tek bir belge üzerinden ilgili tüm dökümanlara hızlı ve bağlamsal olarak erişebilirler.

## Mimari Bileşenler ve Kapsam

İlişkili Belge Mimarisi, döküman yönetimini bir ekosisteme dönüştüren şu yetenekleri kapsar:

- **Otomatik İlişkilendirme:** Veri eşleşmesine dayalı sistem üretimi bağlar.
- **Manuel İlişkilendirme:** Kullanıcı inisiyatifiyle kurulan çift yönlü bağlar.
- **Yönlü İlişki Yapıları:** Tek yönlü veya çift yönlü erişim kontrolleri.
- **Merkezi Görüntüleme:** Tüm ilişkili ağın tek ekrandan izlenmesi.

## 1. Otomatik İlişkilendirme Mekanizması

Belge tipleri arasında tanımlanan kurallar doğrultusunda, sistem dökümanları herhangi bir kullanıcı müdahalesi olmaksızın birbirine bağlar.

- **Tanımlama:** İlişkilendirme kuralları **Kabinet Tanımları** ekranında, ilgili belge tipi üzerinde kurgulanır.
- **Koşul Eşleştirme:** Kaynak ve hedef belge tiplerindeki alanlar (Örn: "Müşteri No" veya "Proje Kodu") birbiriyle eşleştirilir.
- **Asenkron İşlem:** Performansı korumak adına ilişkilendirme işlemi arka planda asenkron olarak yürütülür (ortalama 1 dakika içinde tamamlanır).

### İlişki Yönü Seçenekleri

- **Çift Yönlü İlişki:** Belgelerden herhangi birine erişildiğinde diğerine karşılıklı olarak geçiş yapılabilir.
- **Tek Yönlü İlişki:** İlişki sadece birincil (ana) belgeden alt belgelere doğru kurulur; tersi yönde erişim sağlanmaz.

## 2. Manuel İlişkilendirme

Kullanıcılar, sistemin otomatik olarak yakalayamayacağı ancak iş süreci açısından kritik olan bağları manuel olarak kurabilirler.

**İşlem Adımları:**

1. İlgili belgeler panoya (basket) eklenir.
2. Pano içerisindeki **İlişkilendirme** sekmesi açılır.
3. Belgeler seçilerek bağlama işlemi tamamlanır.

> **Önemli Not:** Manuel olarak oluşturulan tüm ilişkiler sistem tarafından otomatik olarak **çift yönlü** kabul edilir.

## 3. Doküman Ağının Görüntülenmesi

İlişkili Belge Mimarisi ile birbirine bağlanan dökümanlara iki farklı noktadan erişilebilir:

1. **Belgeler Ekranı:** Liste görünümünde yer alan "İlişkili Belgeler" butonu ile hızlı önizleme yapılır.
2. **Belge Detayları:** Döküman detay sayfasındaki özel sekme üzerinden, otomatik veya manuel fark etmeksizin tüm döküman ağı listelenir.

## Sağladığı İş Değeri

- **Bağlamsal Bütünlük:** Bir dökümana bakarken, o dökümanı doğuran veya onun sonucu olan diğer tüm belgelere anında erişilir.
- **Denetim Kolaylığı:** Denetçiler veya yöneticiler için "belge setine" ulaşma süresi saniyelere iner.
- **Karar Hızı:** Karar vericiler, tüm referans dökümanları (teklif, onay yazısı, sözleşme) tek bir ağ yapısında görerek süreci hızlandırır.
- **Veri Düzenleme:** Dağınık ve tekil döküman yapıları, anlamlı bir kurumsal hafızaya dönüşür.

## Teknik Ön Koşullar

- **Arşiv Tipi:** Belgelerin mutlaka bir Arşiv Tipi ile sisteme dahil edilmiş olması gerekir.
- **Alan Tanımları:** Otomatik ilişki için dökümanların en az bir ortak "Anahtar Alan" (Tip Alanı) içermesi şarttır.
- **Yetkilendirme:** Kullanıcı, sadece görme yetkisine sahip olduğu ilişkili belgeleri görüntüleyebilir.

---

**İpucu:** İlişkili Belge Mimarisi'ni "Sohbet Mimarisi" ile birleştirerek, bir belge ağındaki tüm paydaşların tüm ilişkili dökümanlar hakkında ortak bir sohbet kanalında konuşmasını sağlayabilirsiniz.