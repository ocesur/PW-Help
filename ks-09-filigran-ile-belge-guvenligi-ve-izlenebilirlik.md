---
title: "Filigran ile Belge Güvenliği ve İzlenebilirlik"
sidebarTitle: "KS-09 Filigran Yönetimi"
description: "PDF dokümanlar üzerinde dinamik filigranlar kullanarak belge güvenliğini ve kurumsal izlenebilirliği artırın."
keywords: "filigran, belge güvenliği, pdf koruma, izlenebilirlik, yazdırma güvenliği, versiyon kontrolü, dinamik filigran"
---

## Genel Bakış

**Filigran** özelliği, arşivlenen PDF dokümanları üzerinde metin tabanlı katmanlar kullanarak belge güvenliğini ve izlenebilirliğini en üst seviyeye taşır. Filigranlar; belgenin görüntülenmesi, kaydedilmesi, yazdırılması veya eski versiyonlarına erişilmesi gibi farklı senaryolarda otomatik olarak uygulanır.

Bu yapı sayesinde, belgelerin yetkisiz ekran görüntülerinin alınması veya paylaşılması caydırılır; döküman çıktıları üzerinde kaynağı ve kullanım amacını gösteren kalıcı izler yer alır.

## Ne Zaman Kullanılmalıdır?

Aşağıdaki durumlarda Filigran kullanımı kurumsal bir zorunluluk ve güvenlik önlemi olarak önerilir:

- **Hassas Veri Paylaşımı:** Gizli belgelerin üçüncü taraflarla paylaşılması veya dışarı aktarılması gerektiğinde.
- **Fiziksel Arşiv Güvenliği:** PDF belgelerin yazdırıldığı durumlarda, dökümanın kime ait olduğunun çıktı üzerinde görünmesi istendiğinde.
- **Kullanım Takibi:** Belgenin kim tarafından, ne zaman ve hangi amaçla (Örn: "Sadece Bilgi İçindir") görüntülendiğinin belirtilmesi gerektiğinde.
- **Sürüm Karışıklığını Önleme:** Versiyonlanmış belgelerin eski sürümlerinin güncel belgeden net bir şekilde ayırt edilmesi hedeflendiğinde.

## Teknik Çalışma Mekanizması

Filigran tanımları, Arşiv Tipleri üzerinde yer alan **Filigran** sekmesi üzerinden merkezi olarak yönetilir.

**İşleyiş Adımları:**

1. **Tanımlama:** Arşiv tipinde yeni bir filigran kurgusu oluşturulur.
2. **Tasarım:** Filigran metni, yazı tipi, boyutu, açısı ve rengi belirlenir. (Önizleme üzerinden anlık kontrol edilebilir.)
3. **Kural Atama:** Filigranın hangi durumlarda (Görüntüleme, Yazdırma vb.) devreye gireceği seçilir.
4. **Dinamik Uygulama:** Tanımlanan kurallar sağlandığında, sistem PDF üzerine filigranı saniyeler içinde "render" ederek yerleştirir.

## Görünürlük ve Tetikleyici Seçenekleri

Filigranlar, işlem türüne göre özelleştirilebilir:

| İşlem Türü          | Açıklama                                                    |
| :------------------ | :---------------------------------------------------------- |
| **Görüntülemede**   | Belge ekranda açıldığı an kullanıcıyı karşılar.             |
| **Kaydetmede**      | Kullanıcı belgeyi bilgisayarına indirdiğinde PDF'e gömülür. |
| **Yazdırmada**      | Sadece fiziksel çıktı alınırken kağıt üzerinde görünür.     |
| **Eski Versiyonda** | Belgenin güncel olmayan sürümüne bakıldığında uyarır.       |

## Koşullu Filigran Kullanımı (Dinamik Güvenlik)

Filigranlar, form üzerindeki tip alanlarına girilen değerlere göre **koşullu** olarak değişebilir.

- **Örnek:** Belgenin "Gizlilik" alanı "Kritik" seçilmişse kırmızı bir "GİZLİDİR" filigranı; "Genel" seçilmişse şeffaf bir kurumsal logo filigranı gösterilebilir.

## Sağladığı İş Değeri

- **Caydırıcılık:** Belge üzerinde kullanıcı bilgilerinin yer alması, yetkisiz paylaşım riskini minimize eder.
- **Karışıklığı Önleme:** "Eski Versiyon" filigranı sayesinde hatalı (eski) döküman üzerinden işlem yapılmasının önüne geçilir.
- **Denetim Uyumu:** Belgelerin kullanım amacını (Örn: "Maliye Denetimi İçindir") dökümana mühürleyerek izlenebilirlik sağlar.
- **Marka Güvenliği:** Çıktı alınan dökümanların kurumsal standartlarda ve kontrollü dağıtılmasını garanti eder.

## Kritik Notlar

- **Format Kısıtı:** Filigran özelliği teknik olarak yalnızca **PDF** formatındaki dokümanlar için geçerlidir.
- **Merkezi Yönetim:** Tanımlar Arşiv Tipi bazında yapıldığı için o tipteki tüm geçmiş belgelere de uygulanabilir.
- **Esneklik:** Düzenle seçeneği ile filigran metinleri süreçlerin ihtiyacına göre anlık olarak güncellenebilir.

---

**İpucu:** Bu özelliği "Koşula Bağlı Yetki" ile birleştirerek, sadece yetkili kişilerin filigransız döküman görmesini sağlayabilir, güvenliği katmanlı hale getirebilirsiniz.