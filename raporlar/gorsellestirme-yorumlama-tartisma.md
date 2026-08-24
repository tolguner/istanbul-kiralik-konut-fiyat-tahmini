# Görselleştirme, Yorumlama ve Tartışma Belgesi

> Bu belge, `Görselleştirme, Yorumlama ve Tartışma Belgesi.docx` dosyasının Markdown'a dönüştürülmüş hâlidir. Metin içeriği değiştirilmemiştir. Belgede atıfta bulunulan grafikler `Proje Sunumu.pptx` dosyasında ve `konut_fiyat_tahmini.ipynb` not defterinin çıktılarında yer almaktadır.

## 1. Giriş

Bu çalışma, İstanbul'daki kiralık konut ilanlarından elde edilen veriler kullanılarak daire fiyatlarını tahmin eden bir regresyon modeli geliştirmeyi amaçlamaktadır.

Veri temizleme, keşifsel veri analizi (EDA), modelleme, yorumlanabilirlik ve etik farkındalık bileşenleri birlikte ele alınmıştır.

## 2. Görselleştirme Bulguları

### 2.1. Fiyat Dağılımı

- Çoğu ilan 1.000.000 TL altında toplanmaktadır.
- Yüksek uç değerler nadiren görülmüş ve modelin dengesi için temizlenmiştir.

### 2.2. Metrekare Dağılımı

- Ortalama: 100–120 m²
- En sık aralık: 80–150 m²

### 2.3. Oda Sayısı

- En yaygın tipler: 2+1 ve 3+1
- Daha az görülenler: 1+0 (stüdyo) ve 4+1

### 2.4. İlçelere Göre Fiyat

- Beşiktaş, Kadıköy, Şişli: yüksek fiyatlı bölgeler.
- Esenyurt, Sancaktepe: düşük fiyatlı bölgeler

### 2.5. Korelasyon Analizi

- Metrekare ↔ Fiyat: güçlü pozitif ilişki.
- Kat bilgisi ↔ Fiyat: zayıf ilişki.
- İlçe: mekânsal farklılıklar önemli bir faktör

## 3. Modelin Yorumlanması

### 3.1. Öznitelik Önemi

- Fiyat tahmininde en kritik değişkenler: metrekare, oda sayısı ve ilçe.
- Kat bilgisi ve ısıtma tipi gibi değişkenler ikincil öneme sahiptir.

### 3.2. Açıklanabilirlik Yöntemleri

- SHAP ve LIME kullanılarak her tahminde hangi özelliklerin etkili olduğu görselleştirilebilir.
- Bu sayede "kara kutu" etkisi azaltılır, kullanıcı güveni artar

## 4. Tartışma

### 4.1. Modelin Toplumsal Etkileri

- Doğru tahminler → adil fiyatlama, piyasa dengesine katkı.
- Hatalı tahminler → alıcıya ek yük, satıcıya gelir kaybı, ekonomik adaletsizlik riski

### 4.2. Sosyoekonomik Gösterge Riski

- Semt bilgisi gelir, eğitim, altyapı gibi sosyoekonomik göstergeleri yansıtır.
- Model, tarihsel eşitsizlikleri öğrenip pekiştirebilir → düşük gelirli bölgelerin sürekli düşük tahmin edilmesi riski

### 4.3. Etik ve Sorumluluk

- Veri seçimi ve temizliği önyargıların azaltılması için kritik.
- Açıklanabilirlik yöntemlerinin entegrasyonu → kullanıcı güveni ve toplumsal kabul

## 5. Sonuç

Bu çalışmada:

- İstanbul'daki kiralık konut fiyatları için veri temizliği ve görselleştirmeler yapılmış,
- Regresyon modeli kurulmuş,
- Modelin öznitelik önemi ve açıklanabilirliği tartışılmış,
- Etik ve toplumsal boyutlar değerlendirilmiştir.

Sonuç olarak, yalnızca teknik doğruluk değil, aynı zamanda etik sorumluluk ve şeffaflık ilkeleri de dikkate alınarak güçlü bir tahmin sistemi geliştirilmiştir.
