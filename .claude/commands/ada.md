---
description: "Ada (tasarım direktörü): oturumdaki bütün tasarımları kontrol eder, hataları ve önerileri raporlar"
argument-hint: "[ürün, klasör ya da dosya; boşsa oturumun ürünü]"
---

# /ada: tasarım direktörü kontrolü

Agent aracıyla **`ada`** ajanını çalıştır (`.claude/agents/ada.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/ada.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

## Ada bitince
- Raporu Naz'a Türkçe aktar: genel karar, hatalar tablosu (dosya, sayfa, yer, önem), öneriler. Ada'nın bulduğu hataları yumuşatma ya da eleme.
- Kritik ve orta hataları, Naz başka bir şey demediyse, bu oturumun ürününde düzelt; düzelttikten sonra aynı sayfalara yeniden bak. Önerileri (yeni sayfa, bonus, tarz değişikliği) uygulamadan önce Naz'a sor.
