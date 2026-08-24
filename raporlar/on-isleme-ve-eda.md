# Ön İşleme ve Keşifsel Veri Analizi (EDA) Özet Raporu

> Bu belge, `Ön İşleme ve Keşifsel Veri Analizi Raporu.docx` dosyasının Markdown'a dönüştürülmüş hâlidir. Metin içeriği değiştirilmemiştir.

## 1. Veri Setinin Tanımı

Bu çalışmada kullanılan veri seti, İstanbul'da yer alan emlak ilanlarından elde edilmiştir. Veri setinde dairelerin fiyatı, oda sayısı, metrekare bilgisi, bulunduğu kat, ısıtma tipi ve konum gibi değişkenler yer almaktadır. Toplamda binlerce satır ve birçok sütun bulunmaktadır. Bu veriler kullanılarak, kiralık konut fiyatlarının tahmin edilmesi amacıyla bir model oluşturulacaktır. Öncelikle veri temizleme ve keşifsel veri analizi (EDA) adımlarıyla, verinin daha sağlıklı hale getirilmesi hedeflenmiştir.

## 2. Veri Temizleme Adımları

- **Eksik Değerler:** Kat bilgisi, banyo sayısı gibi bazı sütunlarda eksik veriler tespit edilmiştir. Bu değerler, uygun yerlerde ortalama/medyan ile doldurulmuş ya da çok fazla eksik içeren kayıtlar veri setinden çıkarılmıştır.
- **Tutarsız Değerler:** Kat bilgisi sütununda "Bahçe Katı", "Giriş Katı", "Çatı Katı" gibi farklı yazımlar mevcuttu. Bunlar ortak kategoriler altında birleştirilmiştir.
- **Aykırı Değerler:** Metrekare sütununda 20 m²'den küçük veya 1000 m²'den büyük daireler çıkarılmıştır. Fiyat sütununda 100 TL veya 100 milyon TL gibi olağan dışı değerler tespit edilerek temizlenmiştir.
- **Veri Tipi Dönüşümleri:** Fiyat, metrekare gibi sayısal sütunlar uygun formatlara çevrilmiştir. Kategorik sütunlar (ısıtma tipi, eşyalı olup olmama vb.) one-hot encoding için hazırlanmıştır.

## 3. Keşifsel Veri Analizi (EDA)

- **Fiyat Dağılımı:** Fiyatların büyük çoğunluğu 1.000.000 TL altında yoğunlaşırken, az sayıda uç değer üst sınırda toplanmaktadır.
- **Metrekare Dağılımı:** Ortalama metrekare 100–120 m² aralığında, en sık görülen değerler 80–150 m² civarındadır.
- **Oda Sayısı:** 2+1 ve 3+1 daire tipleri en yaygın olanlardır. Daha az sayıda 1+0 (stüdyo) ve 4+1 daireler görülmektedir.
- **İlçelere Göre Fiyat:** Beşiktaş, Kadıköy, Şişli gibi merkezi ilçelerde fiyatlar yüksek; Esenyurt, Sancaktepe gibi kenar ilçelerde daha düşüktür.
- **Kat Bilgisi:** İlanların çoğu orta katlarda yoğunlaşmaktadır. Bahçe katı ve çatı katı gibi özel durumlar düşük frekanstadır.
- **Korelasyon Analizi:** Fiyat ile metrekare arasında güçlü pozitif bir ilişki vardır. Kat bilgisi ile fiyat arasında zayıf ilişki görülmektedir. İlçe bazlı fiyat farkları, mekânsal faktörlerin önemini göstermektedir.

## 4. Çıkarımlar ve İyileştirmeler

- Outlier temizliği ve kategorik değişkenlerin standardizasyonu sonrası veri seti daha güvenilir hale getirilmiştir.
- Kat bilgisi serbest metin şeklinde olduğundan, modele dahil edilmeden önce standartlaştırılmalıdır. Bunun için "kat seviyesi" gibi sayısal değişkenler türetilebilir.
- İlçe bilgisi model için kritik önem taşımaktadır. İlçelere göre ortalama fiyat veya m² fiyatı gibi yeni değişkenler eklenerek model güçlendirilebilir.
- Hedef değişken olan fiyatın dağılımı sağa çarpık olduğu için log dönüşümü uygulanarak model performansı artırılabilir.
- Bu analizler sonucunda, veri seti makine öğrenmesi modeline hazır hale getirilmiş ve İstanbul'daki kiralık konut fiyatlarının daha doğru tahmin edilebilmesi için gerekli temel adımlar atılmıştır.
