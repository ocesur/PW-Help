---
title: "Koşula Bağlı Yetki ile Dinamik Erişim Kontrolü"
sidebarTitle: "KS-08 Koşula Bağlı Yetki ile Dinamik Erişim"
description: "Belge ve kayıtların erişim yetkilerini, form alanlarına girilen değerlere göre otomatik ve dinamik olarak yönetin."
keywords: "dinamik yetkilendirme, erişim kontrolü, veri gizliliği, kabinet yetkisi, arşiv tipi güvenliği, koşullu erişim"
---

## Genel Bakış

**Koşula Bağlı Yetki** özelliği; belge veya dosya kartı kayıtlarının erişim yetkilerinin, kayıt anında tip alanlarına (metadata) girilen değerlere göre otomatik olarak belirlenmesini sağlar. Bu sayede yetkilendirme, sabit rol tanımlarına bağlı kalmadan, belgenin içeriğine göre dinamik ve esnek bir şekilde uygulanır.

Bu yapı, özellikle tek bir arşiv tipi altında toplanan ancak farklı departman veya gizlilik seviyelerine göre ayrıştırılması gereken dökümanlar için üst düzey güvenlik sağlar.

## Ne Zaman Kullanılmalıdır?

Aşağıdaki durumlarda Koşula Bağlı Yetki kullanımı operasyonel yükü azaltır ve güvenliği artırır:

- **Çoklu Birim Yönetimi:** Aynı arşiv tipinde (Örn: Sözleşmeler) farklı birimlerin sadece kendi belgelerini görmesi istendiğinde.
- **Veri Gizliliği:** Belgenin "Gizlilik Derecesi" alanına göre erişimin otomatik kısıtlanması gerektiğinde.
- **Dinamik Rol Atama:** Statik kullanıcı listeleri yerine, döküman içeriğine (Örn: Şehir, Proje Kodu, Tutar) dayalı erişim kontrolü hedeflendiğinde.
- **Hassas Veri Yönetimi:** Belge ve dosya kartlarında kişi bazlı veri gizliliği kritik bir öneme sahipse.

## Teknik Çalışma Mekanizması

Koşula Bağlı Yetki, **klasör yetkileri etkin olmayan kabinetlerde** doğrudan Arşiv Tipleri veya Dosya Kartı Tipleri üzerinde yapılandırılır.

**İşleyiş Adımları:**

1. **Konfigürasyon:** Arşiv tipi içindeki "Yetkiler" sekmesinden "Koşula Bağlı Yetki" seçeneği aktif edilir.
2. **Kriter Tanımlama:** Tip alanlarına (Örn: Departman, Tutar, Bölge) bağlı mantıksal koşullar oluşturulur.
3. **Yetki Seti Atama:** Her koşul için (Örn: Departman = 'Finans') hangi kullanıcı grubunun hangi yetkilere (Görüntüleme, Yazma, Silme vb.) sahip olacağı belirlenir.
4. **Otomatik Uygulama:** Belge arşivlendiği anda sistem girilen değerleri kontrol eder ve ilgili yetki setini saniyeler içinde atar.

## Örnek Kullanım Senaryoları

### 1. Departman Bazlı Belge Erişimi

Belge arşivlenirken "Departman" alanı "İnsan Kaynakları" olarak seçilirse, bu belgeye sadece İK yetki setine dahil olan kişiler erişebilir. Diğer departmanlar belgeyi arama sonuçlarında dahi göremez.

### 2. Gizlilik Seviyesine Göre Filtreleme

Form üzerinde gizlilik seviyesi "Çok Gizli" seçilen bir döküman, sadece üst yönetim yetki setine sahip kullanıcılara açılırken; "Genel" seçilen dökümanlar tüm personele açılabilir.

### 3. Proje Bazlı Dosya Kartı Yönetimi

Dosya kartı oluşturulurken girilen "Proje Kodu" sayesinde, sadece o projede görevli ekip üyelerine otomatik erişim izni verilir.

## Sağladığı İş Değeri

- **Maksimum Güvenlik:** İnsan hatasına yer bırakmadan, verinin içeriğine göre otomatik zırh oluşturur.
- **Yönetim Kolaylığı:** Yüzlerce belgeyi tek tek yetkilendirmek yerine, sistemin bu işlemi arka planda yapmasını sağlar.
- **Süreç Esnekliği:** Farklı senaryoların tek bir arşiv tipi altında, karmaşaya yol açmadan yönetilmesine olanak tanır.
- **Gizlilik Uyumu:** KVKK ve benzeri veri gizliliği yönetmeliklerine uyumu teknik seviyede destekler.

## Kritik Teknik Notlar

- **Kabinet Yapısı:** Bu özellik yalnızca **klasör yetkileri etkin olmayan** kabinetlerde çalışır. Klasör yetkisi aktifse, yetki yönetimi kabinet hiyerarşisi üzerinden yürütülür.
- **Performans:** Koşul tanımları ne kadar sade ve mantıklı kurgulanırsa, sistem performansı o kadar optimize olur.
- **Kalıcılık:** Yetkilendirme işlemi kayıt anında gerçekleştirilir; alan değerleri değiştiğinde yetkilerin güncellenmesi için sistem tetiklenmelidir.

---

**İpucu:** Bu dökümanı "Filigran ile Belge Güvenliği" dökümanı ile birlikte inceleyerek, PaperWork'ün çok katmanlı güvenlik mimarisini tam olarak kavrayabilirsiniz.