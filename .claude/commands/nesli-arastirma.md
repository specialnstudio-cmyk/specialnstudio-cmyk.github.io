---
description: "Nesli (araştırma): Etsy, Google Trends ve bütün webde yeni ürün araştırması yapar, trendleri ve yeni fikirleri listeler"
argument-hint: "[konu, sezon ya da kategori; boşsa genel araştırma]"
---

# /nesli-araştırma: yeni ürün araştırması

Önce master'daki `FIKIRLER.md` dosyasını oku. Sonra Agent aracıyla **`nesli-arastirma`** ajanını çalıştır (`.claude/agents/nesli-arastirma.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/nesli-arastirma.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Bu görevde Nesli, Etsy'yi, Google Trends'i ve dijital ürün satılan bütün yerleri webde tarar; trend olan ürünleri bulur ve listeler, potansiyeli yüksek ve daha önce kimsenin yapmadığı ürün fikirleri geliştirir.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- bugünün tarihi ve önümüzdeki sezonlar;
- Naz'ın bu komutla yazdığı konu ya da kısıt: $ARGUMENTS (boşsa genel araştırma);
- `FIKIRLER.md` içindeki mevcut fikirlerin kısa listesi (tekrar önermesin) ve dükkândaki ürün türleri;
- hedef pazarlar: ABD, Almanya, Danimarka, Birleşik Krallık.

Konu genişse birkaç `nesli-arastirma` ajanını aynı anda farklı alanlara (ör. Etsy, Google ve Pinterest trendleri, diğer pazarlar) gönderebilirsin.

## Nesli bitince
- Kanıtsız rakamları ve bağlantısı olmayan iddiaları ele; şüpheli olanı kendin bir kez kontrol et.
- Raporu Naz'a Türkçe aktar: en güçlü üç fırsat, trend listesi, boşluklar, puanlı fikir tablosu, kaynaklar.
- Naz'ın beğendiği ya da "listeye ekle" dediği fikirleri `FIKIRLER.md` dosyasına, dosyanın başındaki kurallara göre ekle ve `CLAUDE.md` kuralına göre yalnızca o dosya değişecek şekilde master'a gönder.
