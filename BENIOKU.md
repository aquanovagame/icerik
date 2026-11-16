# Uzak İçerik (sürüm göndermeden level ve görsel)

Bu klasör oyuna GÖMÜLMEZ (Assets dışında). İçindekiler sunucuya yüklenir; oyuncunun telefonu arka planda indirir ve
**bir sonraki açılışta** kullanır. Yalnızca level, görsel ve yazı — yeni mekaniğin KODU yine mağaza güncellemesi ister.

## Dosyalar nereye

Yollar oyunun `Assets/_Project/Resources` içindeki yollarla aynıdır:

| Ne | Nereye | Etkisi |
|---|---|---|
| Yeni / düzeltilmiş level | `LevelOverrides/Level_2001.txt` | Level Düzenleyici biçimi. 2000 sonrası haritaya eklenir; var olan numara oyundakinin yerine geçer |
| Engel görseli | `Sprites/Covers/Lava_1.png`, `Volcano_0.png` … | Oyundaki aynı adlı görselin yerine geçer (boyu/yeri korunur) |
| Harita bölgesi | `Sprites/LevelMap/Map_<Bölge>_1.jpg`, `_2` … | Yeni bölgenin haritası; level dosyasında `region:` adıyla eşleşir |
| Çeviri | `Localization/en.txt`, `de.txt` … | Yalnızca yeni satırlar yeter; oyundakilerin üstüne eklenir |

Level'lar sırayla gelmeli: 2001 yoksa 2002 ve sonrası haritada görünmez.

## Yükleme adımları

1. Dosyaları yukarıdaki yerlere koy.
2. Unity → **Okyanus → Uzak İçerik → Paket Listesini Hazırla** (files.txt yazılır, hatalı level'lar listelenir).
3. Denemek için: **Editörde Yerel Klasörü Kullan** işaretle → Play (bu klasör sunucudan inmiş gibi davranır).
4. Klasörün TAMAMINI (files.txt dahil) sunucuya yükle.

## Eski sürüm koruması

Bir dosya yalnızca yeni uygulamada çalışacaksa (ör. volkanlı level, 0.1.7'de gelen kodu ister), files.txt'de o
satırın sonuna elle `min=0.1.7` ekle. Daha eski uygulamalar o dosyayı indirmez. Paket Listesini Hazırla bu işaretleri korur.
Ayrıca eski uygulama bir level'ı okuyamazsa onu atlar; harita o level'dan önce biter.

## Sunucu

`Assets/_Project/Scripts/Gameplay/RemoteContent.cs` → `BaseUrl` BOŞKEN indirme kapalıdır. Unity Cloud Content
Delivery kovası açılınca adresi oraya yazılır ve o sürümden itibaren telefonlar indirmeye başlar.
