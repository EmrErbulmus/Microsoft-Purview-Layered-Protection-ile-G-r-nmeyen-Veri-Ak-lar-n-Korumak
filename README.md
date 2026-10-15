## Microsoft Purview Layered Protection ile Görünmeyen Veri Akışlarını Korumak

# Veri Artık Bir Dosya Değil

Microsoft Purview Layered Protection mimarisinin veri koruma yaklaşımını detaylandırarak Endpoint DLP, Browser Data Security ve Network Data Security katmanlarının birbirini nasıl tamamladığını verinin cihaz, tarayıcı, SaaS uygulamaları ve ağ seviyesinde nasıl keşfedildiğini, sınıflandırıldığını, denetlendiğini ve korunduğunu mimari ve operasyonel boyutlarıyla ele almaktadır.

![Microsoft Purview Layered Protection genel mimarisi](assets/architecture.svg)

Genel mimari; Endpoint DLP, Browser Data Security ve Network Data Security katmanlarının birbirinin alternatifi olmadığını, farklı veri hareketleri için tamamlayıcı yaptırım noktaları sunduğunu gösterir. Endpoint katmanı cihaz ve işletim sistemi aktivitelerine, tarayıcı katmanı desteklenen web oturumlarına, ağ katmanı ise desteklenen ve yönlendirilmiş HTTP/HTTPS trafiğine odaklanır.

## Neden bu makale?

Birçok kurum Endpoint DLP yatırımı sonrasında veri çıkış riskinin büyük ölçüde kontrol edildiğini düşünebilir. Ancak modern veri hareketleri yalnızca USB, yazdırma veya e-posta eki üzerinden gerçekleşmez. Hassas içerik bugün aşağıdaki kanallarda da hareket edebilir:

- Tüketici AI uygulamalarına yazılan veya yapıştırılan istemler
- AI ve bulut uygulamalarına yüklenen dosyalar
- Office eklentilerinin oluşturduğu API çağrıları
- Yerel masaüstü uygulamalarının ağ trafiği
- Yönetilen SaaS oturumları ve BYOD erişimleri
- Desteklenen SASE/SSE yollarından geçen gelen ve giden içerik

Bu çalışma, her veri hareketinde doğru kontrol katmanını seçebilmek için kapsam, sınıflandırma, yaptırım, telemetri, PoC ve ürün sınırlamalarını birlikte değerlendirir.

## Makaleyi oku

➡️ **[Teknik makaleyi aç](docs/article.md)**

## Purview Layered Protection Makalenin kapsamı

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
 
Aynı hassas veri; kullanıcı işlemleri, tarayıcı oturumları, bulut uygulamaları veya ağ trafiği üzerinden farklı kanallarla hareket edebilir. Bu nedenle modern veri koruma yaklaşımı, tek bir güvenlik kontrolüne bağımlı olmak yerine verinin bulunduğu konum, kullanım şekli ve hareket ettiği kanala göre devreye giren katmanlı koruma mekanizmalarına dayanır. Her katman farklı bir görünürlük ve denetim noktası sağlayarak diğer katmanların eksik bıraktığı senaryoları tamamlar. Bu kapsamda Network Data Security, cihaz üzerinde gerçekleşen kullanıcı aktivitelerini gözlemleyemezken; Endpoint DLP de ağ seviyesindeki tüm veri akışlarını veya hizmetler arası trafiği tek başına kapsayamaz. Etkin bir veri güvenliği stratejisi, bu teknolojilerin birbirinin yerine geçmesi üzerine değil, birlikte çalışarak uçtan uca koruma sağlaması üzerine tasarlanır.

### 2. The Void

![Görünürlük ve yaptırım boşluğu](assets/the-void.svg)
 
“The Void” Endpoint DLP ve Browser Data Security gibi koruma mekanizmalarının doğal görünürlük sınırları dışında kalan veri hareketlerini ifade eder. Office eklentileri, masaüstü uygulama entegrasyonları, yönetilmeyen tarayıcılar ve yapay zeka tabanlı veri akışları bu kapsamda değerlendirilebilir. Network Data Security ise trafiğin desteklenen bir Global Secure Access (GSA) veya SASE/SSE altyapısı üzerinden geçirilmesi durumunda bu görünürlük boşluğunu azaltarak, diğer koruma katmanlarının erişemediği bazı veri hareketleri üzerinde ek denetim ve koruma sağlayabilir. Ancak tek başına tüm boşluğu ortadan kaldırmaz; katmanlı veri koruma mimarisinin tamamlayıcı bir bileşeni olarak çalışır.

### 3. Office eklentisi veri yolu

![Office eklentisi ve harici LLM veri akışı](assets/office-addin.svg)

Bazı veri hareketleri, kullanıcı tarafından başlatılan klasik dosya işlemleri veya tarayıcı tabanlı oturumlar üzerinden gerçekleşmez. Örneğin bir Office eklentisi, Word, Excel veya Outlook içerisindeki belge içeriğini arka planda çalışan API çağrıları aracılığıyla harici bir LLM veya bulut servisine iletebilir. Bu senaryoda veri hareketi ne geleneksel bir kopyalama işlemi ne de yönetilen bir tarayıcı oturumu üzerinden gerçekleştiği için Endpoint DLP ve Browser Data Security katmanlarının görünürlüğü sınırlı kalabilir.

Bu tür uygulama tabanlı veri akışlarında, trafik desteklenen bir Global Secure Access (GSA) veya SASE/SSE mimarisi üzerinden yönlendirildiğinde Network Data Security katmanı kritik bir kontrol noktası hâline gelir. Ağ seviyesinde gerçekleştirilen içerik inceleme, veri sınıflandırma ve politika değerlendirme mekanizmaları sayesinde hassas bilgiler analiz edilebilir; engelleme, denetim veya kullanıcı uyarısı gibi yaptırımlar uygulanabilir. Bu nedenle Office eklentileri tarafından oluşturulan API tabanlı veri akışlarında Network Data Security, görünürlük ve yaptırım açısından birincil koruma katmanı olarak konumlanır.

### 4. Kapsama matrisi

![Endpoint Browser ve Network kapsama matrisi](assets/coverage-matrix.svg)

Matris, hangi katmanın hangi veri hareketinde güçlü olduğunu özetler. `✓` doğrudan desteği, `◐` koşula bağlı veya kısmi desteği, `—` ise doğrudan uygulanabilir bir kontrol bulunmadığını gösterir. Koşullu yetenekler cihaz yönetimine, tarayıcıya, uzantıya, ağ ajanına, trafik yönlendirmesine ve entegrasyon sağlayıcısına bağlı olabilir.

## Yazar

**Emre Erbulmuş**  
Microsoft Purview, Data Loss Prevention, Information Protection ve veri güvenliği mimarileri üzerine çalışmalar yürütmektedir.

[Emre Erbulmuş web sitesi](https://www.emreerbulmus.com)

## Kullanım notu

Bu çalışma teknik öğrenme ve mimari değerlendirme amacıyla hazırlanmıştır. Ürün yetenekleri, lisanslama koşulları, önizleme durumu ve desteklenen entegrasyonlar değişebileceği için üretim uygulamasından önce güncel Microsoft belgeleri doğrulanmalıdır.
