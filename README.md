# Veri Artık Bir Dosya Değil

## Microsoft Purview Layered Protection ile Görünmeyen Veri Akışlarını Korumak

Microsoft Purview Layered Protection ile veri hareketlerinin cihaz, tarayıcı ve ağ seviyesinde korunmasını; Endpoint DLP'den Browser Data Security'ye ve Network Data Security'ye uzanan yeni nesil veri koruma mimarisinin teknik analizi üzerinden ele alan öğrenme odaklı bir çalışma.

![Microsoft Purview Layered Protection genel mimarisi](assets/architecture.svg)

Genel mimari; Endpoint DLP, Browser Data Security ve Network Data Security katmanlarının birbirinin alternatifi olmadığını, farklı veri hareketleri için tamamlayıcı yaptırım noktaları sunduğunu gösterir. Endpoint katmanı cihaz ve işletim sistemi aktivitelerine, tarayıcı katmanı desteklenen web oturumlarına, ağ katmanı ise desteklenen ve yönlendirilmiş HTTP/HTTPS trafiğine odaklanır.

## Neden bu makale?

Birçok kuruluş Endpoint DLP yatırımı sonrasında veri çıkış riskinin büyük ölçüde kontrol edildiğini düşünebilir. Ancak modern veri hareketleri yalnızca USB, yazdırma veya e-posta eki üzerinden gerçekleşmez. Hassas içerik bugün aşağıdaki kanallarda da hareket edebilir:

- Tüketici AI uygulamalarına yazılan veya yapıştırılan istemler
- AI ve bulut uygulamalarına yüklenen dosyalar
- Office eklentilerinin oluşturduğu API çağrıları
- Yerel masaüstü uygulamalarının ağ trafiği
- Yönetilen SaaS oturumları ve BYOD erişimleri
- Desteklenen SASE/SSE yollarından geçen gelen ve giden içerik

Bu çalışma, her veri hareketinde doğru kontrol katmanını seçebilmek için kapsam, sınıflandırma, yaptırım, telemetri, PoC ve ürün sınırlamalarını birlikte değerlendirir.

## Makaleyi oku

➡️ **[Teknik makaleyi aç](docs/article.md)**

## Makalenin kapsamı

- Endpoint DLP, Browser Data Security ve Network Data Security rolleri
- Üç katman arasındaki görünürlük ve yaptırım farkları
- “The Void” olarak tanımlanan görünürlük boşluğu
- Office eklentileri, yerel uygulamalar ve API çağrıları
- Collection Policy ile DLP enforcement arasındaki ayrım
- Entra Global Secure Access ve desteklenen SASE/SSE bağımlılıkları
- Örnek müşteri PoC tasarımı ve başarı kriterleri
- Kademeli üretim geçişi, izleme ve operasyon modeli
- Lisanslama, PAYG, teknik uyarılar ve ürün sınırlamaları

## Temel mimari görseller

### 1. Katmanlı koruma yaklaşımı

![Katmanlı veri koruması](assets/layered-protection.svg)
 
Aynı hassas veri, cihaz işlemi, tarayıcı oturumu veya ağ trafiği olarak farklı yollardan hareket edebilir. Bu nedenle koruma modeli tek bir ürün kontrolüne değil, verinin hareket ettiği bağlama göre seçilen tamamlayıcı katmanlara dayanır. Ağ katmanı çevrimdışı cihaz hareketlerinin, Endpoint DLP de API trafiğinin yerine geçmez.

### 2. The Void

![Görünürlük ve yaptırım boşluğu](assets/the-void.svg)
 
“The Void”, Endpoint DLP veya Browser Data Security tarafından doğrudan değerlendirilemeyebilen potansiyel çıkış yollarını temsil eder. Office eklentileri, masaüstü API çağrıları, yönetilmeyen tarayıcılar ve gelen AI yanıtları bu alanda değerlendirilir. Network Data Security, yalnızca trafik desteklenen bir GSA veya SASE/SSE yolu üzerinden geçtiğinde ve gerekli inceleme koşulları sağlandığında bu boşluğu azaltabilir.

### 3. Office eklentisi veri yolu

![Office eklentisi ve harici LLM veri akışı](assets/office-addin.svg)

Bir Office eklentisi belge içeriğini arka planda harici bir API'ye gönderebilir. Bu işlem klasik bir USB kopyası değildir ve bir Edge oturumu da oluşturmayabilir. Böyle bir senaryoda desteklenen ağ yolu üzerindeki Network Data Security, sınıflandırma ve yaptırım için birincil kontrol katmanı hâline gelir.

### 4. Kapsama matrisi

![Endpoint Browser ve Network kapsama matrisi](assets/coverage-matrix.svg)

Matris, hangi katmanın hangi veri hareketinde güçlü olduğunu özetler. `✓` doğrudan desteği, `◐` koşula bağlı veya kısmi desteği, `—` ise doğrudan uygulanabilir bir kontrol bulunmadığını gösterir. Koşullu yetenekler cihaz yönetimine, tarayıcıya, uzantıya, ağ ajanına, trafik yönlendirmesine ve entegrasyon sağlayıcısına bağlı olabilir.

## Yazar

**Emre Erbulmuş**  
Microsoft Purview, Data Loss Prevention, Information Protection ve veri güvenliği mimarileri üzerine çalışmalar yürütmektedir.

[Emre Erbulmuş web sitesi](https://www.emreerbulmus.com)

## Kullanım notu

Bu çalışma teknik öğrenme ve mimari değerlendirme amacıyla hazırlanmıştır. Ürün yetenekleri, lisanslama koşulları, önizleme durumu ve desteklenen entegrasyonlar değişebileceği için üretim uygulamasından önce güncel Microsoft belgeleri doğrulanmalıdır.
