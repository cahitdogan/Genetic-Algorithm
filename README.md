# Genetik Algoritma ile Çalışma Programı Optimizasyonu

Bu proje, bir öğrencinin sınav başarısını maksimize etmek için Matematik ve Fen derslerine ayıracağı etüt sürelerini Genetik Algoritma kullanarak optimize etmeyi amaçlar.

### Amaç Fonksiyonu
Maksimize edilecek başarı skoru:
y = 4x₁ + 5x₂ - 0.5x₁² - 0.2x₂²

### Değişkenler
*   x₁: Matematik çalışma süresi (0-10 saat)
*   x₂: Fen çalışma süresi (0-10 saat)

### Kısıtlar
1.  Toplam çalışma süresi 12 saati geçemez: x₁ + x₂ ≤ 12
2.  Fen çalışma süresi en az 2 saat olmalıdır: x₂ ≥ 2

## Kullanılan Yöntemler (Genetik Algoritma)

1.  **Birey Temsili**: Her çözüm adayı [x₁, x₂] genlerinden oluşan bir kromozomdur.
2.  **Başlangıç Popülasyonu**: Rastgele üretilen 4 birey ile başlar.
3.  **Fitness Hesaplama**: Amaç fonksiyonu değeri hesaplanır. Kısıtları sağlamayan bireylere ceza puanı verilir.
4.  **Seçilim (Selection)**: Fitness değerine orantılı olarak **Rulet Tekerleği (Roulette Wheel)** yöntemi ile ebeveynler seçilir.
5.  **Çaprazlama (Crossover)**: Seçilen her ikili ebeveyn çifti için, birinci ebeveynin ilk geni ve ikinci ebeveynin ikinci geni alınarak yeni birey oluşturulur.
6.  **Mutasyon**: Yeni bireylere aritmetik mutasyon uygulanır:
    *   Yeni = Eski + MutasyonBüyüklüğü × (Rastgele - 0.5)
7.  **Yeni Nesil Seçimi**:
    *   **Elitizm**: Önceki nesil ve yeni üretilenler (havuz) arasından en iyi birey doğrudan bir sonraki nesle aktarılır.
    *   **Turnuva Seçimi**: Geri kalan kontenjanlar, havuzdan rastgele seçilen bireylerin yarıştırılmasıyla doldurulur.

## Kullanılan Kütüphaneler

Proje Python dili ile geliştirilmiştir ve aşağıdaki kütüphaneleri kullanır:

*   **numpy**: Sayısal işlemler (bu versiyonda temel python listeleri ağırlıklı kullanılmıştır, ancak import edilmiştir).
*   **random**: Rastgele sayı üretimi, seçim ve örnekleme işlemleri.
*   **matplotlib**: Nesiller boyunca fitness değişimini görselleştirmek ve `fitness_degisimi.png` grafiğini oluşturmak için.

## Kod Yapısı ve Fonksiyonlar

`genetic_algorithm.py` dosyası içerisindeki temel fonksiyonlar şunlardır:

*   **`Birey` Sınıfı**: Genleri ve fitness değerini tutan veri yapısı.
*   **`fitness_hesapla(birey)`**: Amaç fonksiyonunu hesaplar ve kısıt ihlallerini kontrol eder.
*   **`populasyon_olustur()`**: Rastgele başlangıç popülasyonunu üretir.
*   **`rulet_tekerlegi_secimi(populasyon)`**: Fitness değerlerine göre olasılık tabanlı seçim yapar.
*   **`caprazlama(parent1, parent2)`**: İki ebeveynden gen alışverişi ile çocuk üretir.
*   **`mutasyon(birey)`**: Gen değerlerinde küçük rastgele değişimler yapar.
*   **`turnuva_secimi(havuz)`**: Rastgele seçilen adaylar arasından en iyisini seçer.
*   **`genetik_algoritma_calistir()`**: Algoritmanın ana döngüsüdür. Nesilleri yönetir, en iyi çözümü takip eder ve sonuç grafiğini çizer.

## Çalıştırma

Terminal veya komut satırında proje dizinine giderek aşağıdaki komutu çalıştırın:

```bash
python3 genetic_algorithm.py
```

Çalıştırma sonucunda:
1.  Her nesildeki en iyi fitness değeri ekrana yazdırılır.
2.  Bulunan en iyi çözüm (Matematik ve Fen süreleri) raporlanır.
3.  Başarı skorunun gelişimini gösteren `fitness_degisimi.png` dosyası oluşturulur.
