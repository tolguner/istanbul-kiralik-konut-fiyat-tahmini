# İstanbul Konut Fiyat Tahmini

Emlakjet İstanbul **satılık** konut ilanları üzerinden fiyat tahmini yapan makine öğrenmesi projesi. Veri temizleme, keşifsel veri analizi (EDA), öznitelik mühendisliği ve regresyon modellemesi adımlarını kapsar.

> **Not:** Proje başlangıçta kiralık konut üzerine planlanmış (depo adı bu nedenle `istanbul-kiralik-konut-fiyat-tahmini`), ancak kullanılan veri seti tamamen satılık ilanlardan oluştuğu için model **satış fiyatı** tahmin etmektedir.

**YÖBİ4487.1 Özel Konular: Makine Öğrenmesi** dersi kapsamında geliştirilmiş takım projesidir.

## Ekip

| Öğrenci No | Ad Soyad |
|---|---|
| 22yöbi1041 | Çağan Hatun |
| 23yöbi1039 | İrem Arslan |
| 20yöbi1011 | Serdar Onur Karadağ |
| 21yöbi1014 | Bekir Kadir Demiraslan |
| 23yöbi1053 | Tolga Olguner |

## Veri Seti

`Real Estate in ISTANBUL (Emlakjet).csv` — Emlakjet üzerinden derlenen İstanbul konut ilanları.

| | |
|---|---|
| Kayıt sayısı | 2.983 ilan |
| Sütun sayısı | 27 |
| Kategori | Tamamı satılık konut |
| Kapsam | 13 ilçe |
| Dönem | 2022 ilanları |

Öne çıkan değişkenler: brüt/net metrekare, oda sayısı, bina yaşı, bulunduğu kat, banyo sayısı, ısıtma tipi, eşya durumu, krediye uygunluk, site içerisinde olma, ilçe/mahalle, yaka, mahalle yaşam endeksi ve nüfus.

Veri setinde kişisel veri (isim, telefon, e-posta) bulunmamaktadır; konum bilgisi ilçe/mahalle düzeyindedir.

## Yöntem

**Veri temizleme ve dönüşümler**
- `Binanın_Yaşı`: `"6-10"`, `"21 Ve Üzeri"` gibi aralıklar temsili sayısal değerlere eşlendi
- `Oda_Sayısı`: `"3+1"` → toplam oda sayısı (4) olarak hesaplandı
- `Bulunduğu_Kat`: `"Bahçe Katı"`, `"Kot 1"`, `"Yüksek Giriş"` gibi serbest metin değerler sayısal kat seviyesine dönüştürüldü; kat kavramı olmayanlar (villa, dubleks, müstakil) boş bırakıldı
- `Banyo_Sayısı`: `"Yok"` → 0, mantıksız değerler (>6) elendi
- Aykırı değerler IQR yöntemiyle temizlendi

**Öznitelik mühendisliği**
- `Mahalle` için hedef kodlama (mahalle bazlı ortalama fiyat)
- `Isıtma_Tipi` için one-hot kodlama
- Eşya durumu, yaka, site içerisinde olma ve krediye uygunluk için ikili değişkenler
- İlan tarihlerinden `Yayında_Kalma_Süresi` türetildi
- Hedef değişken sağa çarpık olduğu için **log dönüşümü** uygulandı (`Fiyat_Log`)

**Modelleme**

Üç regresyon modeli karşılaştırıldı; ayrıca `GridSearchCV` ile hiperparametre denemesi yapıldı. Eğitim/test ayrımı %80/%20 (`random_state=42`).

## Sonuçlar

Log dönüştürülmüş hedef değişken üzerinde model karşılaştırması:

| Model | R² | RMSE | MAE |
|---|---|---|---|
| Lineer Regresyon | 0,56 | 0,69 | 0,46 |
| Karar Ağacı | 0,55 | 0,70 | 0,50 |
| **Rastgele Orman** | **0,76** | **0,51** | **0,37** |

En iyi sonucu Rastgele Orman verdi. Seçilen model 300 ağaçlı `RandomForestRegressor` ile 14 öznitelik üzerinde yeniden eğitildiğinde, tahminler orijinal TL ölçeğine geri çevrilerek şu performansı gösterdi:

- **R² = 0,661**
- **RMSE ≈ 4.378.882 TL**

Fiyatların milyonlarca TL düzeyinde ve geniş bir aralıkta (169 bin – 1,8 milyar TL) dağılması nedeniyle mutlak hata yüksektir.

**Bulgular:** Fiyat üzerinde en belirleyici değişkenler metrekare, oda sayısı ve konum (ilçe/mahalle) olarak öne çıktı. Kat bilgisi ve ısıtma tipi ikincil etkiye sahip. Mahalle bazlı fiyat farkları, mekânsal faktörlerin modeldeki ağırlığını göstermektedir.

## Dosyalar

| Dosya | Açıklama |
|---|---|
| `konut_fiyat_tahmini.ipynb` | Analiz not defteri — veri temizleme, EDA, modelleme (çıktılarıyla birlikte) |
| `Real Estate in ISTANBUL (Emlakjet).csv` | Kullanılan veri seti |
| `Proje Sunumu.pptx` | Proje sunumu (37 slayt) |

### Raporlar

Teslim edilen Word belgeleri depo kökünde durmaktadır; aşağıdaki Markdown sürümleri GitHub üzerinde doğrudan okunabilir (içerik birebir aynıdır):

| Rapor | Markdown | Word |
|---|---|---|
| Ön işleme ve keşifsel veri analizi | [raporlar/on-isleme-ve-eda.md](raporlar/on-isleme-ve-eda.md) | `Ön İşleme ve Keşifsel Veri Analizi Raporu.docx` |
| Görselleştirme, yorumlama ve tartışma | [raporlar/gorsellestirme-yorumlama-tartisma.md](raporlar/gorsellestirme-yorumlama-tartisma.md) | `Görselleştirme, Yorumlama ve Tartışma Belgesi.docx` |
| Etik tefekkür | [raporlar/etik-tefekkur.md](raporlar/etik-tefekkur.md) | `Etik Tefekkür Belgesi.docx` |

## Çalıştırma

Not defteri Google Colab üzerinde geliştirilmiştir:

**[Colab'da aç](https://colab.research.google.com/drive/1iiN3Oh3mOIrzkiAZR0t_UlxdJY7alTnz?usp=sharing)**

Yerel ortamda çalıştırmak için:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook konut_fiyat_tahmini.ipynb
```

Not defterinin ilk hücrelerinde Colab'a özel `files.upload()` çağrısı bulunur; yerelde çalıştırırken bu hücre atlanmalı ve CSV dosyası not defteriyle aynı klasörde bulunmalıdır.

## Sunum Videosu

Sunum videosu, depo geçmişini şişirmemesi için sürüm eki olarak yüklenmiştir:

**[Sunum videosunu indir (59,5 MB)](https://github.com/tolguner/istanbul-kiralik-konut-fiyat-tahmini/releases/download/v1.0/Sunum.Videosu.mp4)**

Tüm sürümler: [Releases](https://github.com/tolguner/istanbul-kiralik-konut-fiyat-tahmini/releases)

## Gereksinimler

- Python 3
- pandas, numpy, matplotlib, seaborn, scikit-learn
