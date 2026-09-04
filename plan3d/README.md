# Plan3D – Plandan 3B Yükseltme ve Odalarda Gezinti

Tarayıcıda çalışan, tek dosyalık (bağımlılık: yerel three.js) bir uygulama:
2B kat planını çiz (ya da plan görselinin üstünden geç) → tek tıkla 3B'ye yükselt → odalarda birinci şahıs olarak dolaş.

## Çalıştırma

ES module kullandığı için bir HTTP sunucusu gerekir (dosyayı doğrudan çift tıklayarak açmak çalışmaz):

```bash
cd DataLab
python3 -m http.server 8765
# tarayıcıda: http://localhost:8765/plan3d/
```

## Akış

1. **2B Plan** sekmesinde odaları çiz: `Oda` aracı (1) ile köşelere tıkla, ilk noktaya tıklayarak / Enter ile kapat.
   - Odalar arasında ortak kenarlar otomatik olarak tek duvara birleştirilir (eşdoğrusal segment birleştirme).
   - Serbest bölme duvarları için `Duvar` aracı (2).
2. `Kapı` (3) ve `Pencere` (4) araçlarıyla duvarların üstüne tıkla; açıklık en yakın duvara oturur.
3. İstersen **Plan görseli** yükle, `Ölçek` (7) aracıyla bilinen bir uzunluğu kalibre et ve üstünden çiz.
4. **3B'ye Yükselt ve Gez** → `W A S D` ile yürü, fare ile bak, `Shift` koş.
   - `Kuşbakışı` ile modeli dıştan döndür (sürükle / tekerlek).
   - Sağ alttaki mini haritaya tıklayarak ışınlan, `Odaya git…` ile odaya atla.
   - HUD sol üstte bulunduğun odanın adını ve alanını gösterir.
   - `C` tavan, `L` etiket, `V` görünüm, `Tab` 2B'ye dön.

Plan tarayıcıda (localStorage) otomatik saklanır; `JSON indir / JSON yükle` ile dosya olarak taşınır.

## Parametreler

Duvar yüksekliği/kalınlığı, kapı ve pencere ölçüleri, pencere alt kotu paneldeki alanlardan ayarlanır ve 3B model her girişte yeniden üretilir.

## Teknik notlar

- `vendor/three.module.min.js` + `three.core.min.js`: three.js r185 (MIT, lisans dosyası `vendor/LICENSE.three`).
- Duvarlar: oda kenarları + serbest duvarlar → yön/ofset anahtarıyla gruplanıp aralık birleştirme ile tekilleştirilir; açıklıklar duvarı parçalara böler (lento, denizlik, yan parçalar).
- Çarpışma: yürüme yüksekliğindeki duvar parçalarına karşı daire-segment itme; kapı boşluklarından geçilir, pencerelerden geçilmez.
- Oda tespiti: oyuncu konumu için nokta-poligon testi.
- Mobil: sol yarı sürükle = yürü, sağ yarı sürükle = bak.
