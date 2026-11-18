---
description: "Aslı (avukat): oturuma göre gereken hukuki belgeleri çıkarır, verilenleri kontrol eder, düzenler ve üretir"
argument-hint: "[site, belge ya da konu; boşsa oturumun işi]"
---

# /aslı: hukuki kontrol ve belgeler

Agent aracıyla **`asli`** ajanını çalıştır (`.claude/agents/asli.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/asli.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Aslı, e-ticaret ve dijital ürün satışında 20 yıllık uzman avukattır; özellikle web sitelerinin hukuki süreçlerinde. Oturuma göre gereken belgeleri çıkarır, verilen belgeleri kontrol eder, gerekli düzenlemeleri ve çıktıları hazırlar.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: satışın yapıldığı yer ve ülkeler, sitenin kodu ya da adresi, toplanan veriler ve kullanılan araçlar (analitik, piksel, e-posta, ödeme), mevcut hukuki belgelerin yolları, bugünün tarihi. Belgelerin nereye yazılacağını söyle (ürünün ya da sitenin kendi klasörü).

## Aslı bitince
- Çok dilli belgeleri `/nazlı` ile kontrol ettir.
- Raporu Naz'a Türkçe aktar: en acil konular, gereken belgeler tablosu, hazırlanan dosyalar, Naz'ın doldurması gereken bilgiler (`[DOLDURULACAK: …]`) ve kaynaklar. "Doğrulanamadı" diye işaretlenenleri ve bir avukat ya da mali müşavirle teyit edilmesi gerekenleri açıkça söyle.
- Yayındaki sitede değişiklik gerektiren maddeleri Naz onaylayınca uygula.
