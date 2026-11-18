---
description: "Nesli (ürün): ilan görsellerini tasarlar; platforma göre başlık, açıklama, SEO, etiket ve alt metinleri hazırlar"
argument-hint: "[ürün ve platform; boşsa oturumun ürünü, Etsy]"
---

# /nesli-ürün: ilan görselleri ve ilan SEO'su

Agent aracıyla **`nesli-urun`** ajanını çalıştır (`.claude/agents/nesli-urun.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/nesli-urun.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Bu görevde Nesli, satın almayı tetikleyen ve en çok dikkat çeken ilan görsellerini tasarlar; ürünün yükleneceği platforma göre başlık, açıklama, SEO, etiket ve görsel alt metinlerini hazırlar.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: platform (belirtilmediyse Etsy), ürünün gerçek içeriği (sayfa sayısı, ölçüler, dosya biçimleri, diller), ürünün son dosyalarının yolları, mevcut ilan görselleri ve metinleri, varsa ilan numarası.

## Nesli bitince
- Bütün metinleri (başlık, açıklama, etiket, alt metin, görsellerin üzerindeki yazılar) `/nazlı` ile kontrol ettir.
- Görselleri `/ada` ile kontrol ettir; kritik ve orta hataları düzelt.
- Raporu Naz'a Türkçe aktar: görseller (sıra, görev, alt metin), metinler ve karakter sayıları, anahtar kelime gerekçesi.
- Etsy'ye yükleme ya da yayındaki ilanı güncelleme için `etsy_lister/README.md` adımlarını izle. Yeni ilanı yayınlamak Naz'ın kararıdır.
