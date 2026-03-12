---
title: "Yorumlar ve Sohbet Mimarisi"
sidebarTitle: "KS-10 Yorumlar ile Birleşik İletişim Mimarisi"
description: "PaperWork üzerinde belge, klasör ve iş akışı bağlamında yürütülen entegre sohbet ve bildirim yönetimi."
keywords: "sohbet mimarisi, yorumlar, @mention, bahsetme, iş birliği, süreç içi iletişim, bildirim sistemi, anlık mesajlaşma"
---

## Genel Bakış

PaperWork platformu; belge, klasör, dosya kartı ve iş akışları kapsamında yapılan tüm yorumları ve anlık mesajlaşmaları **Sohbet Mimarisi** altında yönetir. Bu yapı, kullanıcıların dökümanlardan kopmadan, doğrudan "işin mutfağında" izlenebilir ve bildirim destekli iletişim kurmasını sağlar.

## Sohbet Mimarisinin Kapsamı

Bu mimari, aşağıdaki bileşenlerin entegre çalışmasıyla döküman bazlı iletişimi sağlar:

- **Yorumlar Nesnesi:** Belgeler üzerindeki kalıcı ve tarihçeli geri bildirimler.
- **Akıllı Bahsetmeler (@):** Kullanıcı odaklı etkileşim ve e-posta bildirimleri.
- **Nesne Bazlı Sohbet Kanalları:** Dökümana veya klasöre özel anlık iletişim kanalları.
- **İş Akışı Sohbetleri:** Süreç adımlarında teknik veya operasyonel destek kanalları.

## 1. Yorumlar ve Etkileşim Yönetimi

Belgeler ekranındaki **Yorumlar** nesnesi, döküman veya formlar üzerinde kalıcı bir iletişim tarihçesi oluşturur.

- **Dinamik Düzenleme:** Kullanıcılar kendi yorumlarını ekleyebilir veya güncelleyebilir.
- **Görsel Destek:** Emoji kullanımı ile geri bildirimler zenginleştirilebilir.
- **Güvenli Silme:** Veri bütünlüğü için sadece eklenen **son yorum** silinebilir.
- **@Bahsetmeler (@mention):** Bir kullanıcıdan bahsettiğinizde, sistem otomatik olarak e-posta ve uygulama içi bildirim göndererek ilgili kişiyi konuya dahil eder.

## 2. Sohbet Mimarisi ve Kanal Yönetimi

Sohbet özelliği, platform üzerinde e-posta trafiğini azaltan ve dökümanla eşleşen bir anlık mesajlaşma deneyimi sunar.

- **Anlık Güncelleme:** Yazışmalar tüm katılımcılarda eş zamanlı yenilenir.
- **Çoklu Kanal:** Bir belge veya dosya kartı altında farklı konular için (Örn: "Finans Onayı", "Teknik Revizyon") ayrı kanallar açılabilir.
- **Görsel Takip:** Mesajların kimler tarafından okunduğu "Görüldü" bilgisiyle takip edilebilir.
- **Tam Metin Arama:** Sohbet Mimarisi içindeki tüm yazışmalar sistem genelindeki aramalara dahildir.

## 3. İş Akışlarında Sohbet Kullanımı

Süreç taslaklarında, işin doğasına göre iki farklı sohbet türü konumlandırılabilir:

1. **Süreç Destek:** İş mantığına ve operasyonel kararlara yönelik sohbetler.
2. **Teknik Destek:** Sürecin mimari veya sistemsel konularına yönelik teknik yazışmalar.

> **Yetki Notu:** Süreç tasarımında yer alan "Sohbet başlatabilir" seçeneği ile hangi adımda hangi kullanıcının iletişim başlatabileceği hassas bir şekilde kontrol edilir.

## 4. Bildirimler ve Okunma Takibi

Sohbet Mimarisi üzerindeki tüm trafik, sağ üst menüdeki merkezi **Bildirim İkonu** üzerinden yönetilir:

- **Sayaç Desteği:** Okunmamış mesajlar anlık sayaç ile gösterilir.
- **Akıllı Listeleme:** Listeden çıkarılan bir sohbet, yeni bir mesaj geldiğinde otomatik olarak tekrar bildirim listesinin üst sırasına taşınır.
- **Bağlantılı Erişim:** Bildirime tıklandığında doğrudan ilgili dökümana veya sohbet kanalına yönlendirme yapılır.

## Sağladığı İş Değeri

- **Bağlama Duyarlı İletişim:** İletişim dökümanla birleştiği için "hangi dosya hakkındaydı?" karmaşası biter.
- **Kurumsal Hafıza:** Sohbet Mimarisi üzerinden yürütülen tüm yazışmalar arşivlenerek kurumsal bilginin korunmasını sağlar.
- **Operasyonel Hız:** E-posta trafiğini azaltarak kararların daha hızlı alınmasına olanak tanır.
- **İzlenebilirlik:** Kimin, ne zaman, hangi konuda onay veya görüş verdiği kayıt altına alınır.

## Teknik Ön Koşullar

- **Yetki:** Kullanıcının nesne üzerinde en az **Görme Yetkisi** bulunmalıdır.
- **Sistem Ayarı:** Sohbet ve yorum modülleri sistem yönetim panelinden aktif edilmiş olmalıdır.
- **Entegrasyon:** Yorumlardaki bahsetmeler, sohbet bildirim ekranlarıyla tam uyumlu çalışır.

---

**İpucu:** Uzun sözleşme incelemelerinde "AI Belge Özetleme" ile dökümanı analiz edip, kritik bulgularınızı Sohbet Mimarisi içindeki kanallarda paylaşarak süreci hızlandırabilirsiniz.