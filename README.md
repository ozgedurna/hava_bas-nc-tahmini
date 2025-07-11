# Hava Durumu Veri Analizi 🌦️
Bu analizde, günlük hava durumu verileri kullanılarak **ertesi günün atmosfer basıncını (target_pressure)** tahmin etmeye yönelik istatistiksel ve makine öğrenmesi tabanlı bir yaklaşım izlenmiştir. Amaç, sıcaklık, nem, rüzgar hızı gibi değişkenlerin, atmosfer basıncıyla olan ilişkisini analiz ederek basit bir regresyon modeli geliştirmektir.

---


## İçerik
- Korelasyon analizi
- Doğrusal regresyon modeli
- Görselleştirme
- Model değerlendirme

## Kullanılan Araçlar
- Python
- Pandas, Matplotlib, Seaborn, Scikit-learn
- Google Colab



## 📁 Veri Seti Özellikleri

Kullanılan veri setinde aşağıdaki değişkenler bulunmaktadır:

- `meantemp`: Günlük ortalama sıcaklık (°C)  
- `humidity`: Günlük ortalama nem oranı (%)  
- `wind_speed`: Günlük ortalama rüzgar hızı (km/h)  
- `meanpressure`: Günlük ortalama atmosfer basıncı (atm)  
- `date`: Gözlem tarihi  
- `day_of_year`, `month`, `season`: Tarihten türetilen tarihsel öznitelikler  
- `target_pressure`: Ertesi günün atmosfer basıncı (hedef değişken)  
- `BackupLatitude`, `BackupLongitude`, `BackupElevation`: İstasyon konum bilgileri

---

## 🔍 Korelasyon Analizi

Veri setindeki sayısal değişkenler arasında Pearson korelasyon katsayısı hesaplanmıştır.

### Öne Çıkan Bulgular:

| Değişken Çifti              | Korelasyon | Yorum |
|-----------------------------|------------|-------|
| `meantemp` & `humidity`     | -0.57      | Sıcaklık arttıkça nem azalma eğiliminde – beklenen fiziksel ilişki. |
| `meantemp` & `season`       | 0.53       | Mevsimsel sıcaklık artışı – yaz mevsiminde sıcaklık artıyor. |
| `wind_speed` & `humidity`   | -0.37      | Rüzgar arttıkça nemde azalma eğilimi olabilir. |
| `target_pressure` & Diğerleri| ≈ 0.00    | Hedef değişken ile anlamlı korelasyon bulunmamaktadır. |

Sonuç olarak, `target_pressure` değişkeni ile girdi değişkenleri arasında güçlü doğrusal ilişkiler görülmemektedir.

---

## 🤖 Modelleme: Doğrusal Regresyon

### Kullanılan Model:
- **Linear Regression** (scikit-learn)

### Girdi Değişkenleri:
- `meantemp`, `humidity`, `wind_speed`, `day_of_year`, `month`, `season`

### Performans Sonuçları:

| Metrik | Değer |
|--------|-------|
| MSE (Mean Squared Error) | 124.12 |
| R² Skoru | -2.84 |

🔴 **Yorum:**
Modelin doğruluk performansı zayıf kalmıştır. R² skorunun negatif olması, modelin tahminlerinin, sabit ortalama değerinden bile daha kötü olduğunu göstermektedir.


## 📌 Yorum & Değerlendirme

Modelin başarısız olmasının temel nedeni, `target_pressure` ile diğer değişkenler arasında anlamlı istatistiksel korelasyonların olmamasıdır. Bu durum, basıncın daha karmaşık ve çok faktörlü bir değişken olduğunu, basit lineer modellerle doğru şekilde tahmin edilemeyeceğini göstermektedir.

---
