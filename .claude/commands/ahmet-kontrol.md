---
description: "Ahmet (web tasarımcısı): verilen sitenin tasarımını, altyapısını, yeteneklerini ve özelliklerini inceler; hiçbir şeyi değiştirmez"
argument-hint: "[site adresi ya da depo; boşsa oturumun sitesi]"
---

# /ahmet-kontrol: site incelemesi

Agent aracıyla **`ahmet`** ajanını **Kontrol kipinde** çalıştır (`.claude/agents/ahmet.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/ahmet.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Bu kipte Ahmet verilen sitenin bütün tasarımını, altyapısını, yeteneklerini ve özelliklerini inceler. **Hiçbir dosyayı değiştirmez.**

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: "Kip 1: Kontrol" olduğunu, sitenin deposunun yolu ve yayın adresi, siteyi yerelde çalıştırma komutu (biliyorsan), sitenin amacı (ne satıyor, kime).

## Ahmet bitince
- Raporu Naz'a Türkçe ve sade bir dille aktar: genel durum, sitenin yetenek listesi, başlıklara göre bulgular, en önemli 5 sorun. Önemli ekran görüntülerini Naz'a göster.
- Hiçbir şeyi düzeltme; düzeltme `/ahmet-bastır` işidir. Hukuki eksikler için `/aslı` öner.
