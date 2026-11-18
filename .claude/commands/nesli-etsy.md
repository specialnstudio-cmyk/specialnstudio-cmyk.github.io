---
description: "Nesli (Etsy): ürünün Etsy ilanını baştan sona hazırlar (görseller, alt metinler, video, başlık, açıklama, etiketler, fiyat, bölüm) ve Etsy'de taslak olarak açar"
argument-hint: "[ürün; boşsa oturumun ürünü]"
---

# /nesli-etsy: Etsy ilanını hazırla ve taslağa at

Agent aracıyla **`nesli-etsy`** ajanını çalıştır (`.claude/agents/nesli-etsy.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/nesli-etsy.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Bu görevde Nesli ürüne göre Etsy ilanının tamamını hazırlar: merak uyandıran ve satışı tetikleyen ilan görselleri (alt metinleriyle), ilan videosu, başlık, açıklama, görünürlüğü artıran 13 etiket, fiyat ve dükkân bölümü. Sonunda ilan Etsy'de **taslak** olarak açılır.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: ürünün gerçek içeriği (sayfa sayısı, ölçüler, dosya biçimleri, diller), ürünün son dosyalarının yolları, hedef pazar ve ilan dili, dükkânın mevcut bölümleri ve benzer ilanların fiyatları (biliyorsan), bugünün tarihi.

## Nesli bitince (sırayla)
1. **Dil:** bütün metinleri (başlık, açıklama, etiket, alt metin, görsellerin üzerindeki yazılar) `/nazlı` ile kontrol ettir; metni değişen görselleri yeniden üret.
2. **Tasarım:** görselleri ve videoyu `/ada` ile kontrol ettir; kritik ve orta hataları düzelt, düzelttiklerine yeniden bak.
3. **Kendi kontrolün:** görselleri aç; ürünün gerçeğiyle (sayılar, sayfalar) uyuştuğuna, başlık ve etiket sınırlarına, görsel sırasına bak.
4. **Taslağa at:** `etsy_lister/README.md` adımlarını izle: girdi dosyalarını `etsy-assets` dalına koy, ürün YAML'ını ve metin dosyasını master'a gönder, `etsy-urun-listele.yml` işini `ref: master` ile önce `kontrol`, sonra `taslak` olarak çalıştır. Video için depodaki video yükleme işini kullan. Araç bölüm ya da para birimi için durursa Nesli'nin önerisini YAML'a yaz; emin değilsen Naz'a sor.
5. **Doğrula:** taslağı `goster` ile Etsy'den geri oku ve hazırlanan metinlerle karşılaştır. Geri okunamayan alanları (ör. fiyat, kategori) açıkça söyle.
6. **Rapor:** Naz'a Türkçe aktar: taslağın Shop Manager bağlantısı ve ilan numarası, görseller (sıra, görev), başlık ve etiketler (Türkçeleriyle), fiyat ve gerekçesi, bölüm, Naz'ın editörde bakması gerekenler.
7. `OTURUM_ISLERI.md` içindeki bölümüne ilan numarasını ekle.

## Yapılmayacaklar
- **Yayınlama, indirim, kupon ve reklam yok**; hepsi Naz'ın kararı. İlan taslak kalır.
- Dükkânda yeni bölüm açma; uygun bölüm yoksa öner ve Naz'a bırak.
- Başka ilanlara dokunma.
