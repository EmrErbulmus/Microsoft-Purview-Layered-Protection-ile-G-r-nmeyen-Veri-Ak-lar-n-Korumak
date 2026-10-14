# Veri Artık Bir Dosya Değil

## Microsoft Purview Layered Protection ile Endpoint DLP, Browser Data Security ve Network Data Security Katmanlarında Modern Veri Koruma Mimarisi

Microsoft Purview Layered Protection ile veri hareketlerinin cihaz, tarayıcı ve ağ seviyesinde korunmasını; Endpoint DLP'den Browser Data Security'ye ve Network Data Security'ye uzanan yeni nesil veri koruma mimarisinin teknik analizi üzerinden ele alan öğrenme odaklı bir çalışma.

![Microsoft Purview Layered Protection genel mimarisi](assets/architecture.svg)

## Makaleyi oku

➡️ **[Teknik makaleyi aç](docs/article.md)**

## Makalenin kapsamı

- Endpoint DLP, Browser Data Security ve Network Data Security rolleri
- Üç katman arasındaki görünürlük ve yaptırım farkları
- “The Void” olarak tanımlanan denetim boşluğu
- Office eklentileri, yerel uygulamalar ve API çağrıları
- Örnek müşteri PoC tasarımı
- Politika karar akışı ve kademeli devreye alma
- Teknik uyarılar, bağımlılıklar ve ürün sınırlamaları
- GitHub uyumlu Mermaid ve SVG mimari diyagramları

## Temel mimari görseller

### Katmanlı koruma yaklaşımı

![Katmanlı veri koruması](assets/layered-protection.svg)

### The Void

![Görünürlük ve yaptırım boşluğu](assets/the-void.svg)

### Office eklentisi veri yolu

![Office eklentisi ve harici LLM veri akışı](assets/office-addin.svg)

### Kapsama matrisi

![Endpoint Browser ve Network kapsama matrisi](assets/coverage-matrix.svg)

## Depo yapısı

```text
.
├── README.md
├── docs
│   └── article.md
└── assets
    ├── architecture.svg
    ├── layered-protection.svg
    ├── the-void.svg
    ├── office-addin.svg
    └── coverage-matrix.svg
```

## Yazar

**Emre Erbulmuş**  
Microsoft Purview, Data Loss Prevention, Information Protection ve veri güvenliği mimarileri üzerine çalışmalar yürütmektedir.

[emreerbulmus.com](https://www.emreerbulmus.com)

## Kullanım notu

Bu çalışma teknik öğrenme ve mimari değerlendirme amacıyla hazırlanmıştır. Ürün yetenekleri, lisanslama koşulları, önizleme durumu ve desteklenen entegrasyonlar değişebileceği için üretim uygulamasından önce güncel Microsoft belgeleri doğrulanmalıdır.
