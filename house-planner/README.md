# Tek Kat Plan Stüdyosu

Parametrik tek katlı konut plan üretici. Tek dosya (`index.html`), bağımlılık yok (PDF için jsPDF CDN).

- Program: yatak odası (1–4), banyo (1–2, ikincisi en-suite), ayrı WC, açık/kapalı mutfak, yemek masası konumu
- Kabuk: genişlik, gündüz/gece bandı derinliği, koridor, duvar kalınlıkları
- Çıktı: katmanlı SVG (`<g id="A-WALL-EXT">` …), renk kodlu A3 1:100 PDF, DXF R12 (`.dxf.txt` → uzantıyı `.dxf` yapın)

Katmanlar AutoCAD adlandırma + ACI renk indeksiyle eşlenir: A-WALL-EXT(7) A-WALL-INT(8) A-DOOR(1) A-GLAZ(4) A-FURN(3) A-ANNO(5) A-DIMS(6) A-AREA(9).
