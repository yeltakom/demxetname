# demxetname

zaman çizelgesi, 1853–2026.

Araştırma · derleme: Yıldız Tahtacı — Pelin Tan — Yelta Köm
2020 / 2026
Arazi Assembly 

---

## Olayları Nasıl Düzenlerim?

Tüm olaylar **`events.csv`** dosyasındadır. Excel, Google Sheets ya da herhangi bir spreadsheet uygulamasında açıp düzenleyebilirsin.

### Sütunlar

| Sütun | Açıklama | Örnek |
|---|---|---|
| `id` | Benzersiz numara (her olay için farklı) | `91` |
| `year` | Olay yılı | `2026` |
| `lat` | Enlem (Google Maps'ten al) | `37.9144` |
| `lng` | Boylam | `40.2306` |
| `category` | Şu beş seçenekten biri: `hukuki`, `yikim`, `yerinden`, `mimarlik`, `direnis` | `hukuki` |
| `title_tr` | Türkçe başlık | `TBMM Komisyonu Raporu` |
| `location_tr` | Türkçe lokasyon | `Ankara` |
| `description_tr` | Türkçe açıklama (uzun yazabilirsin) | `18 Şubat 2026...` |
| `title_en` | İngilizce başlık | |
| `location_en` | İngilizce lokasyon | |
| `description_en` | İngilizce açıklama | |

### Yeni Olay Ekleme

1. `events.csv` dosyasını aç (GitHub'da "Edit" butonuyla ya da bilgisayarına indirip Excel/Numbers/Google Sheets ile)
2. Sona yeni satır ekle, tüm sütunları doldur
3. `id` numarasını bir önceki olaydan büyük yap (örn: 91, 92, 93...)
4. Kaydet ve GitHub'a yükle (commit)
5. 1-2 dakika sonra site güncellenir

### Olay Düzenleme

Sadece o satırı değiştir, kaydet, GitHub'a yükle.

### Olay Silme

O satırı sil, kaydet, GitHub'a yükle.

### Önemli Uyarılar

- **`id` numarasını değiştirme** — her satırın id'si benzersiz olmalı
- **Kategori adlarına dikkat** — sadece şu beşi geçerli: `hukuki`, `yikim`, `yerinden`, `mimarlik`, `direnis`
- **Tırnak işareti içinde tırnak** kullanırsan iki tırnak ("") yaz: `Said'in "stajını" tamamladı`
- **Virgül** sorun değil — alanlar zaten tırnak içinde

---

## Teknik

- Tek HTML dosyası (`index.html`)
- Veri: `events.csv` (112 olay)
- Beş görünüm (üst menüden): **Liste** (dikey omurga), **Yatay** (onyıl kolonlu bant),
  **Halka** (çevrede kronoloji, içeride ilişki kirişleri), **Harita 3B** (eğik perspektifli
  gerçek harita — olaylar `lat`/`lng` konumlarından iğne olarak yükselir, ilişkiler
  mekânlar arasında kırmızı yay çizer), **Ağ 3B** (kuvvet yerleşimli üç boyutlu
  ilişki haritası — coğrafyasız)
- İlişkiler yalnızca veriden türetilir: bir olayın açıklamasında anılan yıllar,
  o yıllardaki diğer olaylara bağlanır (tıklayınca kırmızı çizgilerle vurgulanır)
- Kütüphane bağımlılığı yok, build yok, framework yok — 3B görünümler elle yazılmış
  canvas projeksiyonu; yalnızca Harita 3B, karoları CARTO/OpenStreetMap'ten çeker
- Arama motorlarından gizli (`robots.txt` + `noindex` meta)

## Lisans

CC BY-NC-SA 4.0 — Creative Commons Attribution-NonCommercial-ShareAlike
