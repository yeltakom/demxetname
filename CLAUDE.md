# demxetname — proje bağlamı (Claude Code için)

Diyarbakır ve Kürdistan'da bir zaman çizelgesi, 1853–2026.
Araştırma · derleme: Yıldız Tahtacı — Pelin Tan — Yelta Köm · Arazi Assembly.
Yayın: https://yeltakom.github.io/demxetname/ (GitHub Pages, main dalından)

## Mimari

- **Tek dosya:** `index.html` — build yok, framework yok, kütüphane yok.
  Tüm görünümler elle yazılmış canvas/SVG. Tek dış kaynak: harita karoları
  (CARTO/OSM, `basemaps.cartocdn.com`).
- **Veri:** `events.csv` — 112 olay. Sütunlar: id, year, lat, lng, category,
  title_tr/en, location_tr/en, description_tr/en. Kategoriler: hukuki, yikim,
  yerinden, mimarlik, direnis. ID'ler 1–90 eski, 91–112 yeni; ID'leri değiştirme.
- **İlişkiler yalnızca veriden türetilir:** bir olayın TR metninde geçen yıllar
  (1853–2026 aralığında regex), o yıllardaki diğer olaylara çift yönlü kenar olur.
  Şu an 92 kenar / 75 olay. Elle ilişki uydurma; yeni ilişki istenirse açıklama
  metnine yıl referansı eklenir.
- Sayfa arama motorlarından gizli (noindex + robots.txt) — bunu koru.

## Tasarım dili

Beyaz zemin, siyah mürekkep, tek vurgu kırmızısı `#ff2d00` (yalnız ilişkiler,
seçim ve direniş kategorisi). Serif (Georgia) yıllar ve marka; Arial gövde;
küçük büyük-harf etiketler; ince (1px) çizgiler. Referanslar: Japon bahçe
bakım çizelgeleri, Terminator Studies ilişki posteri, deck.gl yay haritaları.
İstatistik kutusu, sayac, süsleme istenmiyor — "saçma sapan detay olmasın".

## GÜNCEL GÖREV — tek bütünleşik site (kullanıcının son brifi)

Kullanıcı şu anki 5 sekmeli yapıdan (Liste/Yatay/Halka/Harita 3B/Ağ 3B) memnun
değil: "tek bir site olsun, bir harita üzerinde, Claude AI tasarımı gibi
durmasın". İstenen:

1. Sekmeli görünüm değiştirici KALKACAK; tek, bütünleşik bir deneyim.
2. Sahne gerçek coğrafya: tam ekran, gri tonlamalı, sade DÜZ (2B) harita
   (3B eğik perspektif istenmiyor). Harita kodu `index.html` içinde mevcut
   (mp* fonksiyonları, Mercator karo matematiği) — düzleştirilip yeniden
   kullanılabilir ya da sadeleştirilir.
3. Olaylar haritada kategori işaretleriyle; tıklayınca ilişkiler haritada
   kırmızı eğriler olarak çizilir (tüm ilişkiler soluk, seçim kırmızı).
4. Altta yatay zaman şeridi (1853–2026): olay çentikleri, hover/seçim haritayla
   senkron. Yanda açılır-kapanır kronolojik liste (mevcut Liste estetiği).
   Harita + şerit + liste üçü tek seçim durumunu paylaşır.
5. Detay kartı: yıl (serif büyük), başlık, konum, açıklama, ↔ ilişki linkleri.
6. Editoryal, poster gibi dursun — jenerik "AI dashboard" görünümü istenmiyor.

## Veri notları (editörlere iletildi, karar onların)

- id 108 İHD: metin "2002'de İstanbul şubesine saldırı, Akın Birdal yaralandı"
  diyor; gerçekte saldırı 1998'de Ankara genel merkezindeydi.
- id 111 Susurluk: metindeki "emniyet müdürü Süleyman Şahin" muhtemelen
  Hüseyin Kocadağ olmalı.

## Çalışma biçimi

- Geliştirme dalı: `claude/simplify-wiki-design-2MAlX`; yayın main'e PR ile.
- Yerel test: `python3 -m http.server` (file:// altında fetch çalışmaz).
- `events.csv` düzenleme kuralları README'de.
