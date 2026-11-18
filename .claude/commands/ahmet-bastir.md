---
description: "Ahmet (web tasarımcısı): sitenin nasıl olması gerektiğini belirler, eksikleri söyler ve siteyi iyileştirir"
argument-hint: "[site adresi ya da depo, varsa odak; boşsa oturumun sitesi]"
---

# /ahmet-bastır: siteyi hedefe taşı ve iyileştir

Agent aracıyla **`ahmet`** ajanını **Bastır kipinde** çalıştır (`.claude/agents/ahmet.md`). Ajan türü listede yoksa (ajan dosyası bu oturum başladıktan sonra eklenmişse) `general-purpose` ajanını çalıştır ve ona ilk iş olarak `.claude/agents/ahmet.md` dosyasını okuyup oradaki role ve kurallara aynen uymasını söyle.

Bu kipte Ahmet sitenin yetenek, görsel ve altyapı olarak nasıl olması gerektiğini belirler; eklenmesi ve değiştirilmesi gerekenleri söyler ve siteyi iyileştirir.

## Ajana vereceğin bilgiler
Ajan bu sohbeti görmez. Görev metnine şunları yaz:
- oturumun ürünü ya da işi ve amacı;
- ilgili dosya ve klasörlerin tam yolları (yayındaki site ya da ilan varsa adresi);
- hedef pazar ve diller;
- bu oturumda verilmiş kararlar ve dokunulmaması gerekenler;
- Naz'ın bu komutla yazdığı ek istek: $ARGUMENTS

Ek istek boşsa kapsam bu oturumun bütün işidir. Oturumda henüz bir iş yoksa ve neyin inceleneceği belli değilse Naz'a tek soruyla sor.

Ayrıca ajana şunları ver: "Kip 2: Bastır" olduğunu, sitenin deposunun yolu ve yayın adresi, siteyi yerelde çalıştırma komutu, bu oturumda yapılmış bir `/ahmet-kontrol` raporu varsa tamamı, Naz'ın değişmesini istemediği şeyler.

## Ahmet bitince
- Değişiklikleri kendin gözden geçir: siteyi çalıştır, masaüstü ve telefon görünümünde bak, satış akışını dene.
- Değişen site metinlerini `/nazlı` ile kontrol ettir. Görünüm önemli ölçüde değiştiyse `/ada` ile ikinci göz al.
- Raporu Naz'a Türkçe aktar: hedef tanımı, yapılanlar (önce/sonra ekran görüntüsüyle), Naz'ın kararını bekleyenler.
- Commit ve push'u oturumun dalına yap. Yayındaki siteye çıkarmak (master'a birleştirme, alan adı, ödeme ayarı) Naz'ın onayıyla olur.
