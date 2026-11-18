---
description: "Nesli (pazarlama uzmanı): ürünü 360 derece ele alır; strateji, plan, reklam planı, sosyal medya içeriği, görsel ve video"
argument-hint: "[ürün ya da kampanya; boşsa oturumun ürünü]"
---

# /nesli: pazarlama stratejisi, plan ve içerik

Agent aracıyla **`nesli`** ajanını çalıştır (`.claude/agents/nesli.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/nesli.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Nesli ürünü 360 derece ele alır, satış yerine göre pazarlama stratejisi kurar, tarihli bir plan çıkarır, reklam faaliyetlerine kadar her şeyi planlar, sosyal medya içeriği üretir ve yalnızca kendi planına bağlı olarak görsel ve video hazırlar.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: ürünün satıldığı yer(ler) ve ilan adresleri, fiyat, lansman tarihi ya da sezon, ürünün gerçek dosyalarının ve mevcut görsellerinin yolları, bağlı araçlar (Metricool, Canva).

## Nesli bitince
- Nesli'nin ürettiği **bütün metinleri** `/nazlı` ile kontrol ettir (Nesli kendisi yaptırdıysa raporundaki durumu doğrula). Dil kontrolünden geçmemiş metin Naz'a "hazır" diye sunulmaz.
- Görsel ve videoları kendin aç, plana ve ürünün gerçeğine uyduğuna bak.
- Raporu Naz'a Türkçe aktar: strateji özeti, tarihli plan, reklam planı, dosya yolları, Naz'ın yapacakları.
- **Naz onaylamadan** Metricool'da planlama ya da yayın, reklam, hesap ya da ilan değişikliği yapma.
