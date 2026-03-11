---
title: "PaperWork Ürün Kalite Yaklaşımı"
---

GGSoft, kurumsal tüm iç süreçlerini iyileştirmek adına 2022 yılında
 başlattığı çalışma sonucu kalite belgelerini almıştır. Bu çalışmada tüm
 iç süreçler PaperWork BPM ile modellenmiş ve hayata geçirilmiştir.
 Aşağıda kurumsal kalite için alınan sertifikalar bulunmaktadır.

Aynı zamanda başlatılan çalışmalar ile yazılım geliştirme çalışmalarında
 3 büyük güncelleme sağlanmıştır.

Yazılım Geliştirme süreçlerinin
 şeffaflaşması; Bu çalışmalarda ISO 15504 kuralları baz
 alınmıştır. Bu kapsamda özetle yazılım geliştirme aşamaları şunları
 içermektedir;

- Sahadan gelen talepler ile veya yapılan ARGE çalışmaları sonucunda
 oluşturulan isterlerin tamamının toplanması, değerlendirilmesi.
- İsterlerin analiz dokümanlarının oluşturulması. Bu dokümanların
 standartlarının belirlenmesi.
- Analiz sonucunda Yıllık ana planın, 3 aylık versiyon planlarının ana
 çıktılarının belirlenmesi.
- Analiz dokümanı ile beraber tasarım adımının planlanması ve gerekli
 dokümanın oluşturulması.
- Etki analizinin çıkartılması.
- UI standartlarının belirlenmesi.
- Test senaryolarının oluşturulması.
- UI, Unit, Automated testlerin belirlenmesi.
- Geliştirme takviminin belirlenmesi.
- Portal içeriğinin planlanması ve üretilmesi.

Tüm geliştirme faaliyetleri yukarıda belirtilen ana çerçeve dahilinde
 yapılmaktadır.

Yapılan geliştirtişme faaliyetlerinin otomatik kontrolü ve
 denetlenmesi; Tüm CI/CD süreçleri Azure DevOps üzerine
 taşınmıştır. Bu çalışma ile şunlar sağlanmıştır;

Ölçeklenebilirlik;İhtiyaca göre kolayca ölçeklenebilir bir yapı
 kurulmuş, geliştirici sayısı artırılmıştır.​

CI/CD Desteği: Azure Pipelines ile sürekli entegrasyon ve dağıtım
 süreçlerini otomatikleştirilmiş, bu sayede günlük sürüm üretimi
 sağlanmıştır.

​İşbirliği Araçları;Azure Boards gibi özellikler sayesinde ekipler arası
 iletişim ve görev takibi güçlenmiş, olası sorunların hızlı çözümü
 sağlanmıştır.​

Güvenilirlik;SaaS mimarisi sayesinde yüksek erişilebilirlik sağlanmış ve
 her yerden çalışmayı mümkün kılmıştır.

Geliştirici Araçları: Geliştirme esnasında Copilot gibi AI tool desteği
 sağlanmış, kod kalitesini artırmak ve geliştirme süratini artırmak için
 kullanıma alınmıştır.

Otomatik Testlerin planlanması; 2023 yılı başında
 başlatılan iç proje ile Selenium platformunda otomatik testler
 kurgulanmıştır. İlk etapta 1000 civarı test senaryosu oluşturulmuş,
 günlük sürümlerin hepsinde testlerin koşturulması sağlanmıştır. Proje
 esnasında oluşturulan alt yapı ile platformun her noktasının yeni test
 senaryolarının oluşturulması, eklenmesi ve çalıştırılşması mümkün
 kılınmıştır.

## Yerinde ARGE Merkezi

GGSoft, 2023 yılı içerisinde yapılan çalışmalar ile T.C. Teknoloji ve
 Sanayii Bakanlığı denetlemeleri geçirilmiş, yerinde ARGE merkezi olmaya
 hak kazanmıştır.

## Olası Güvenlik Açıkları ve Aksiyonlar

PaperWork çok katmanlı bir yapıya sahiptir. Mimari [şu sayfadan](/tr/docs/a5x010500000) incelenebilir. Buna göre PaperWork ara yüzleri uygulama sunucusu ile
 REST---\>.NET kütüphaneleri ile haberleşir. Bu katmandaki tüm veri
 şifrelidir ve sadece geliştirme katmanı metodları üzerinde çalışır.
 Ayrıca uygulama sunucusu (Content Server) üzerinde bir metodu
 çağırabilmek için aktif bir PaperWork kullanıcı oturumuna ihtiyaç
 bulunur. Bu oturum sadece verilmiş yetkileri ile hareket eder. Tüm bu
 mimari olası güvenlik açıkları için de çeşitli önlemler içerir.

Güvenlik testleri sonucunda bulgular şu kanallardan gelebilmektedir;

1. PaperWork, her ana sürümünde (4.0, 5.0, 6.0 gibi) tüm platform
 bileşenlerini güvenlik testlerine sokmaktadır.
2. [3ncü parti](/tr/docs/paperwork-3ncü-parti-bileşenleri) bileşen üreticileri kendi versiyonları dahilinde güvenlik açığı var ise bildirimlerde bulunmaktadır.
3. Müşterilerimiz, zaman zaman kurum içi güvenlik taramaları yaparak
 bildirimlerde bulunmaktadırlar.
4. T.C. Bilgi Teknolojileri ve İletişim kurumu bünyesinde bulunan
 ilgili ekip, ülke sınırları içerisinde erişebildiği tüm sistemlerde
 güvenlik taramaları yapmakta ve üreticilere bilgi vermektedir.
 Üreticinin bu bildirimlerde yasal süre içerisinde konuyu
 çözümlemesi, yama çıkartması ve ilgili ortamı güncellemesi kanunla
 korunan bir yapıdır.

Güvenlik ile ilgili tüm bildirimler özenle ele alınmakta ve hedef olarak
 aynı gün içerisinde problemin giderilerek yama çıkartılması
 sağlanmaktadır. CI/CD süreçlerinin buluta çıkış tarihi olan 2023
 yılından itibaren alınan herhangi bir bildirimde 1 günü aşmadan yama
 çıkartılabilmiştir.

​