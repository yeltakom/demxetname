# demxetname — proje bağlamı (Claude Code için)

Diyarbakır ve Kürdistan'da bir zaman çizelgesi, 1853–2026.
Araştırma · derleme: Yıldız Tahtacı — Pelin Tan — Yelta Köm · Arazi Assembly.
Yayın: https://yeltakom.github.io/demxetname/ (GitHub Pages, main dalından)

## Mimari

- **Tek dosya:** `index.html` — build yok, framework yok, kütüphane yok.
  Harita canvas'a elle yazılmış düz Mercator karo projeksiyonu; zaman şeridi SVG;
  liste ve kart DOM. Tek dış kaynak: harita karoları
  (CARTO `light_nolabels`, `basemaps.cartocdn.com`).
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

## Arayüz — tek bütünleşik görünüm (sekme yok)

Beş sekmeli eski yapı (Liste/Yatay/Halka/Harita 3B/Ağ 3B) kaldırıldı. Yerine
tek bir sahne: harita. Dört yüzey aynı `state.sel` / `state.hov` durumunu paylaşır;
birinde seçilen olay ötekilerin hepsinde vurgulanır.

- **Harita** (`drawMap`) — tam ekran, gri tonlamalı, düz (2B) Mercator. Karolar
  `grayscale + contrast` ile çizilir, üstüne beyaz örtü; mürekkep hep en üstte.
  Aynı koordinatı paylaşan olaylar ekranda küçük bir rozet halkası olarak açılır
  (`_fi`/`_fn`, gerçek koordinat bozulmaz). Etiketler yalnız seçim/ilişki/hover
  için, sekiz aday konum denenerek çakışmasız yerleştirilir.
- **Zaman şeridi** (`renderStrip`) — altta, 1853–2026, yıla göre istiflenmiş
  çentikler; seçimde kırmızı dikey kılavuz.
- **Kronoloji** (`renderList`) — solda açılır-kapanır; seçili satır siyah blok.
- **Detay kartı** (`renderCard`) — sağda; dar ekranda alttan açılan levha.
  Dar ekranda liste ile kart birbirini dışlar (`narrow()`), harita hep görünür.
- **İlişkiler** — tüm kenarlar haritada soluk gri eğri; seçilenler kırmızı.
  Seçimde kadraj, seçim + ilişkileri kapsayacak şekilde yumuşakça kayar
  (`fitPoints`/`flyTo`), ama zaten görünürse yerinden oynamaz (`allVisibleOnScreen`).
  Panellerin örttüğü alan `clearRect()` ile kadraj dışında tutulur.
- Klavye `←`/`→` kronolojik gezinme, `Esc` seçimi bırakır; kalıcı bağlantı `#e<id>`.

## Veri notları (editörlere iletildi, karar onların)

- id 108 İHD: metin "2002'de İstanbul şubesine saldırı, Akın Birdal yaralandı"
  diyor; gerçekte saldırı 1998'de Ankara genel merkezindeydi.
- id 111 Susurluk: metindeki "emniyet müdürü Süleyman Şahin" muhtemelen
  Hüseyin Kocadağ olmalı.

## Çalışma biçimi

- Geliştirme dalı: `claude/simplify-wiki-design-2MAlX`; yayın main'e PR ile.
- Yerel test: `python3 -m http.server` (file:// altında fetch çalışmaz).
- `events.csv` düzenleme kuralları README'de.
