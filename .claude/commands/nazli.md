---
description: "Nazlı (dil editörü): Türkçe, Almanca, Danca ve İngilizce metinleri kontrol eder ve oturumun belgelerini düzeltir"
argument-hint: "[dosya, klasör ya da metin; boşsa oturumun bütün metinleri]"
---

# /nazlı: dil kontrolü ve düzeltme

Agent aracıyla **`nazli`** ajanını çalıştır (`.claude/agents/nazli.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/nazli.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Nazlı dört dilde (Türkçe, Almanca, Danca, İngilizce) anadili düzeyinde editördür: metinlerin akıcı, doğal ve o dilin cümle kuruluşuna ve dilbilgisi kurallarına uygun olup olmadığını kontrol eder, düzeltilecek yerleri belirler ve **oturuma ait belgeleri yerinde düzeltir**.

Nazlı yalnızca dilbilgisine değil, **alıcının gözünden** anlaşılırlığa da bakar: yanlış anlaşılabilen kelimeleri (ör. İngilizce oyun zarı için "die" yerine **"dice"**) ve oyunu hiç görmemiş birinin anlayamayacağı talimatları (ör. "puts her pawn on the start star" → "Stand her paper figure on the gold star at the start of the path") kendiliğinden düzeltir; eksik kesme, katlama, yapıştırma adımlarını ekler. Ayrıntı ve örnekler `.claude/agents/nazli.md` içinde.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana, metinlerin geçtiği **bütün** dosyaları ver: ilan metinleri (başlık, açıklama, etiket, alt metin), PDF ve görsel üreten betiklerdeki yazılar, sosyal medya metinleri, site metinleri, Aslı'nın hazırladığı belgeler.

## Nazlı bitince
- Metni değişen PDF ve görselleri yeniden üret; taşma ya da kesilme olmadığına gözle bak.
- Raporu Naz'a Türkçe aktar: değişen dosyalar, önemli düzeltmeler (yabancı dildeki örneklerin Türkçesiyle), Nazlı'nın karar veremediği ve ürün gerçeğiyle çelişen yerler.
- Değişen metin Etsy'de yayındaki ya da taslaktaki bir ilana aitse `CLAUDE.md` içindeki kurala göre ilanı güncelle.
