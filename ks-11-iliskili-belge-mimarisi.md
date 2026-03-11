[]{#X1e25b732d3d982370c5164fda7744aa12b774bc display="false"}

## İlişkili Belge Mimarisi ile Doküman Ağı Oluşturma {#ilişkili-belge-mimarisi-ile-doküman-ağı-oluşturma block-id="mm3en7pp-v1hrsg-309"}

[]{#amaç display="false"}

## Amaç {#amaç block-id="mm3en7pp-0jtx35-310"}

Bu kullanım senaryosunun amacı; PaperWork platformunda arşivlenen
belgeler arasında ilişki kurularak, birbirini tamamlayan dokümanların
anlamlı bir doküman ağı (doküman ekosistemi) içerisinde yönetilmesini
açıklamaktır. Bu yapı sayesinde kullanıcılar, bir belgeye bağlı tüm
ilgili dokümanlara hızlı ve bağlamsal olarak erişebilir.

[]{#kapsam display="false"}

## Kapsam {#kapsam block-id="mm3en7pq-ufdv2m-312"}

Bu senaryo aşağıdaki konuları kapsar: - Belge tipleri arasında otomatik
ilişkilendirme - Belgeler ekranında manuel ilişkilendirme - Tek yönlü ve
çift yönlü ilişki yapıları - İlişkili belgelerin görüntülenmesi

[]{#ön-koşullar display="false"}

## Ön Koşullar {#ön-koşullar block-id="mm3en7pq-6xc3zr-314"}

- Belgelerin **Arşiv** tipi kullanılarak arşivlenmiş olması gerekir.

- Otomatik ilişkilendirme için belge tipleri ve tip alanları tanımlanmış
  olmalıdır.

- Kullanıcının ilgili belgeleri görüntüleme yetkisine sahip olması
  gerekir.

[]{#kullanım-senaryosu-adımları display="false"}

## Kullanım Senaryosu Adımları {#kullanım-senaryosu-adımları block-id="mm3en7pq-qrintv-319"}

[]{#otomatik-ilişkilendirme display="false"}

### 1. Otomatik İlişkilendirme {#otomatik-ilişkilendirme block-id="mm3en7pq-omqlw6-320"}

Belge tipleri arasında tanımlanan kurallar doğrultusunda, sistem
belgeleri otomatik olarak ilişkilendirebilir.

- İlişkilendirme tanımı **Kabinet Tanımları** ekranında, belge tipi
  üzerinde yapılır.

- Kaynak belge tipi ile hedef belge tipine ait tip alanları koşul olarak
  eşleştirilir.

- Eşleşen alanlardaki veriler belirtilen koşulları sağladığında belgeler
  otomatik olarak ilişkilendirilir.

- İlişkilendirme işlemi sistem tarafından **asenkron** olarak
  gerçekleştirilir (yaklaşık 1 dakika).

[]{#ilişki-yönü-seçenekleri display="false"}

#### İlişki Yönü Seçenekleri {#ilişki-yönü-seçenekleri block-id="mm3en7pr-5yy8h4-327"}

- **Çift Yönlü İlişki:** İlişkilendirilen tüm belgelerden karşılıklı
  olarak erişim sağlanır.

- **Tek Yönlü İlişki:** İlişkili belgelere yalnızca birincil belgeden
  erişilebilir.

[]{#otomatik-ilişkilerin-görüntülenmesi display="false"}

### 2. Otomatik İlişkilerin Görüntülenmesi {#otomatik-ilişkilerin-görüntülenmesi block-id="mm3en7pr-akmc9z-331"}

Otomatik olarak ilişkilendirilen belgeler, **Belgeler** ekranında yer
alan **İlişkili Belgeler** tuşu aracılığıyla görüntülenir.

- Kullanıcı, ilgili belgeye bağlı tüm ilişkili belgelere tek ekrandan
  erişebilir.

- İlişkiler, tanımlanan ilişki yönüne göre listelenir.

[]{#manuel-ilişkilendirme display="false"}

### 3. Manuel İlişkilendirme {#manuel-ilişkilendirme block-id="mm3en7pr-1soh3g-336"}

Kullanıcılar, belgeler arasında manuel olarak da ilişki kurabilir.

Manuel ilişkilendirme adımları: 1. Belgeler ekranında ilişkilendirilmek
istenen bir veya birden fazla belge panoya eklenir. 2. Pano içerisinde
**İlişkilendirme** sekmesi açılır. 3. Belgeler seçilerek ilişkilendirme
işlemi tamamlanır.

- Manuel oluşturulan tüm ilişkiler **çift yönlüdür**.

[]{#belge-detaylarından-ilişkili-belgeler display="false"}

### 4. Belge Detaylarından İlişkili Belgeler {#belge-detaylarından-ilişkili-belgeler block-id="mm3en7ps-klb9s5-341"}

Belge detay ekranında yer alan **İlişkili Belgeler** seçeneği ile,
belgeye bağlı tüm ilişkili dokümanlar görüntülenebilir.

- Bu ekran, otomatik ve manuel olarak oluşturulmuş tüm ilişkileri
  kapsar.

- İlişkilendirme kurallarına bağlı olarak oluşturulan ilişkiler asenkron
  olarak güncellenir.

[]{#iş-değeri display="false"}

## İş Değeri {#iş-değeri block-id="mm3en7ps-g0k0qt-346"}

İlişkili Belge mimarisi sayesinde: - Belgeler arasında bağlamsal
bütünlük sağlanır - Dağınık doküman yapıları anlamlı bir ağ yapısına
dönüşür - Denetim, inceleme ve karar süreçleri hızlanır - Belgeye bağlı
tüm referanslara tek noktadan erişim mümkün olur

[]{#sonuç display="false"}

## Sonuç {#sonuç block-id="mm3en7ps-xk5qwv-348"}

İlişkili belge mimarisi ile PaperWork platformunda belgeler, yalnızca
tekil kayıtlar olarak değil; birbirleriyle ilişkili, izlenebilir ve
yönetilebilir bir doküman ağı içerisinde ele alınır.
