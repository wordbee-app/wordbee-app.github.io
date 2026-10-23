# WordBee kelime içeriği (`words.json`)

Uygulama bu dosyayı açılışta kontrol eder (en fazla saatte bir). Yeni içerik, çocuk uygulamayı
**bir sonraki açışında** görünür.

## Güncelleme adımları

1. GitHub'da `data/words.json` dosyasını aç → kalem simgesi (**Edit**).
2. Değişikliği yap (aşağıdaki örneklere bak).
3. En üstteki `"version"` sayısını **1 artır** (ör. `1` → `2`). Artırmazsan uygulamalar değişikliği almaz.
4. `"updated"` tarihini güncelle (isteğe bağlı).
5. **Commit changes** → birkaç dakika içinde yayında olur.

Kontrol için tarayıcıda aç: https://wordbee-app.github.io/data/words.json

## Kullanıcıya gösterilen bildirim

Yeni sürüm uygulandığında uygulama açılışta **"Yeni kelimeler geldi!"** penceresi gösterir ve eklenen
kelimeleri listeler (yeni kategori varsa "Yeni bölüm" olarak). İstersen pencereye kendi mesajını
da ekleyebilirsin; `"updated"` satırının altına:

```json
  "announcement": { "tr": "Yeni hayvanlar geldi! 🦓", "en": "New animals are here! 🦓" },
```

Bu alan isteğe bağlıdır. Bir sonraki güncellemede kaldırmazsan, o güncellemede de gösterilir.

## Kurallar (uygulama bu kurallara uymayan dosyayı yok sayar ve eski kelimelerle devam eder)

- **Var olan `id`'leri değiştirme veya silme.** Çocuğun ilerlemesi ve yıldızları bu id'lere bağlı.
  Kategori silmek yasak; kelimenin yazımını/çevirisini düzeltmek serbest.
- Her kategoride **en az 10 kelime** olmalı.
- Bir kategori içinde kelime `id`'leri **benzersiz** olmalı. Yeni kelimeye sıradaki numarayı ver.
- `word`, `translation`, `image` boş olamaz. `image` bir emoji'dir.
- Cümle şablonlarında (`sentences`) hem `en` hem `tr` içinde `___` (3 alt çizgi) olmalı.
- `stars`: kategorinin haritada açılması için gereken toplam yıldız (tam sayı).
- `"format": 1` değerine dokunma.
- Virgüllere dikkat: listedeki **son öğeden sonra virgül olmaz**.
  Emin değilsen içeriği https://jsonlint.com adresine yapıştırıp kontrol et.

## Örnek: mevcut kategoriye kelime ekleme

`animals` kategorisinde son kelime `"id": "25"` ise:

```json
        { "id": "25", "word": "octopus", "translation": "ahtapot", "image": "🐙" },
        { "id": "26", "word": "zebra", "translation": "zebra", "image": "🦓" }
```

## Örnek: yeni kategori ekleme

`categories` listesinin sonuna (son kategoriden sonra virgül koyarak):

```json
    {
      "id": "ocean",
      "titles": {"tr": "Okyanus", "en": "Ocean"},
      "stars": 950,
      "color": "#039BE5",
      "gradient": ["#81D4FA", "#0277BD"],
      "story": { "emoji": "🌊", "tr": "Arı okyanusa daldı! 🐝", "en": "Bee dived into the ocean! 🐝" },
      "sentences": [
        { "en": "I can see a ___", "tr": "Bir ___ görebiliyorum" }
      ],
      "words": [
        { "id": "1", "word": "shark", "translation": "köpek balığı", "image": "🦈" },
        ...en az 10 kelime...
      ]
    }
```

`gradient`, `story` ve `sentences` isteğe bağlıdır.
