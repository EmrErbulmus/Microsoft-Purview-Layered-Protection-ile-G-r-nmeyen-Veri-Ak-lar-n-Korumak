# Veri Artık Bir Dosya Değil

## Microsoft Purview Layered Protection ile Endpoint DLP, Browser Data Security ve Network Data Security Katmanlarında Modern Veri Koruma Mimarisi

![Genel mimari](../assets/architecture.svg)

## Katmanlı koruma yaklaşımı

Her katman farklı bir veri hareketi bağlamında çalışır. Endpoint DLP cihaz ve işletim sistemi düzeyindeki hareketlere, Browser Data Security desteklenen tarayıcı oturumlarına, Network Data Security ise desteklenen ve yönlendirilmiş ağ trafiğine odaklanır.

![Katmanlı veri koruması](../assets/layered-protection.svg)

## The Void

Tek bir katmanın göremediği veya doğrudan yaptırım uygulayamadığı yollar, görünürlük ve yaptırım boşluğu oluşturur. Office eklentileri, masaüstü API çağrıları ve yönetilmeyen tarayıcı trafiği bu değerlendirmede ayrıca ele alınmalıdır.

![The Void görünürlük boşluğu](../assets/the-void.svg)

## Office eklentisi senaryosu

Office eklentisi, belge içeriğini arka planda harici bir API'ye gönderebilir. Tarayıcı oturumu olmayan bu senaryoda Network Data Security, desteklenen ağ yolu ve entegrasyon mevcutsa birincil kontrol katmanıdır.

![Office eklentisi ve harici LLM veri akışı](../assets/office-addin.svg)

## Kapsama matrisi

Aşağıdaki matris, katmanların güçlü olduğu alanları basitleştirilmiş biçimde gösterir. Kısmi veya koşullu hücreler; cihaz yönetimi, tarayıcı, uzantı, ağ ajanı, trafik yönlendirmesi ya da entegrasyon desteğine bağlıdır.

![Purview katmanları kapsama matrisi](../assets/coverage-matrix.svg)

## Teknik uyarı

- Tek katman tam kapsama sağlamaz.
- Network Data Security çevrimdışı USB veya yerel yazdırma hareketlerinin yerine geçmez.
- Ağ görünürlüğü trafik yönlendirmesi, TLS inceleme yaklaşımı ve desteklenen GSA/SASE/SSE entegrasyonuna bağlıdır.
- Browser Data Security yetenekleri yönetilen cihaz, Edge oturumu veya yönetilen uygulama bağlamına göre değişebilir.
- Kapsama ve lisanslama üretim öncesinde güncel resmi belgelerle doğrulanmalıdır.
