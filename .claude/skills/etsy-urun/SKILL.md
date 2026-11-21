---
name: etsy-urun
description: "Yeni Etsy ürünü akışı: brief'ten Etsy taslağına kadar sabit sırayla, az token ve az GitHub Actions dakikasıyla çalışır. Naz \"/etsy-urun\" ya da \"/etsy-ürün\" yazdığında, bir brief verip yeni ürüne başladığında, \"Etsy işi\", \"yeni ürün\", \"bu brief'le ürünü yap\" dediğinde kullan."
argument-hint: "[brief ya da briefler/ içindeki dosya]"
---

# /etsy-urun: brief'ten Etsy taslağına

Bu akış sabittir: adımları sırayla yap, atlama, sıra değiştirme. Naz ile Türkçe konuş, teknik kelime kullanma. Her onay noktasında **dur ve Naz'ın cevabını bekle**; onay gelmeden sonraki adıma geçme. Onay isterken tek mesajda, numaralı ve kısa sor.

## Tasarruf kuralları (her adımda geçerli)
- **Bir oturum = bir ürün** (bir dil). Ürün bitince Naz'a "oturumu kapatabilirsin" de. İkinci ürüne bu oturumda başlama; yeni oturum öner.
- Ajanlar (Ada, Nazlı, Nesli) **yalnızca 7. adımda, birer kez** çalışır.
- Görselleri ve sayfaları tek tek açıp bakma: önce kontak (tek görselde küçük önizlemeler) yap, onu bir kez oku.
- Naz'a önizleme gönderirken hepsini tek seferde gönder; düzeltmeleri tek listede iste.
- GitHub Actions: bir iş hata verirse aynısını hemen yeniden gönderme. Önce kaydını oku, nedeni düzelt, sonra bir kez gönder. İşi gönderip iptal etme. Birden çok ilan ya da dil varsa tek işte yükle (`etsy-toplu-yukle.yml`). Başka oturumun Etsy işi çalışıyorsa bitmesini bekle.
- Eski oturumları ve `OTURUM_ISLERI.md`'nin tamamını okuma; yalnızca bu ürünle ilgili bölüm ve gereken README.

## 0. Depo kontrolü
- Bu akış yalnızca `specialnstudio1` deposunda çalışır. O depo bağlı değilse dur: Naz'a "Yeni oturumu açarken depo olarak yalnızca specialnstudio1'i seç" de.
- Oturuma başka depolar da bağlıysa Naz'a bir kez, tek cümleyle söyle: "Bu oturumda fazladan depo var; bir dahaki sefere yalnızca specialnstudio1'i seçersen daha az harcar." Sonra devam et (depoları sen kaldıramazsın).
- `HAFIZA.md`'yi (master) oku ve notlarına uy.

## 1. Brief'i al, eksikleri tek seferde sor
Brief'ten şunları çıkar: ürün türü, **dil** (her dil ayrı ürün), sayfa boyutu (TR/DE A4, EN US Letter), sayfa sayısı ve içerik, yaş ya da hedef kitle, beğenilen örnekler, istenmeyenler, Naz'ın hazır dosyası var mı.
Eksik olanları **tek mesajda** sor. Aynı mesajda şunu da sor: "Görselleri fal.ai'de ben mi üreteyim, yoksa sen mi yaptıracaksın? Hazır dosyan varsa ver."
Brief uzunsa `briefler/<ürün>.md` olarak kaydet; sonra hep o dosyaya bak.

## 2. Kısa plan → ONAY
5–8 maddelik plan yaz: sayfa listesi, tarz, görsellerin kaynağı (fal.ai / Naz / hazır dosya), dosya biçimi. **Naz onaylamadan üretme.**

## 3. Tarz soruları → ONAY (görsel üretilecekse)
Görsel ister fal.ai'de ister Naz tarafından üretilecek olsun, önce tarzı sabitle. Tek mesajda 4–6 kısa soru sor: çizim tarzı (ör. kalın çizgili boyama / sulu boya / düz vektör), renk paleti, karakterler ve yaş görünümü, arka plan, yazı olacak mı, kaçınılacaklar. Mümkünse 2–3 seçenek ver.
Cevaplardan **tarz kartı** yaz (tek paragraf) ve onay iste. Bu karttan sonra tarz değişmez; her görsel promptu bu karttan türetilir.

## 4. Görseller
**A) fal.ai ile (Naz istediyse):** Onay mesajında şunu açıkça yaz: kaç görsel üretilecek, hangi model, deneme turu. Önce **1–2 deneme** görseli üret ve göster. Naz beğenince geri kalanını tek seferde üret. Naz'ın onayladığı sayıyı aşma; aşmak gerekirse yeniden sor. Model ve betik bilgisi `HAFIZA.md`'de (fal.ai notu).
**B) Naz yaptıracaksa:** Tarz kartından her görsel için kopyalanabilir, ayrı bloklarda prompt ver (Gemini'ye yapıştırılacak biçimde, İngilizce prompt + altında Türkçesi). Naz görselleri verince devam et.
**C) Naz hazır dosya verdiyse:** 4. ve 5. adımı atla, 6. adıma geç.

## 5. İçerik sayfaları
Görseller gelince planla gereken sayfaları (kapak sayfası, talimat, içindekiler, yazılı sayfalar, sertifika gibi) yap ve PDF'i üret. Önce **1–2 örnek sayfa** göster; onaydan sonra hepsini üret. Bitince bütün sayfaları tek kontak görselinde göster ve düzeltmeleri **tek listede** iste.

## 6. Etsy kapağı ve ilan görselleri → ONAY
`etsy-gorsel` skill'ini çalıştır (`.claude/skills/etsy-gorsel/SKILL.md`): kapak, 7 ilan görseli, video ve alt metinler. Etsy'ye henüz yükleme. Kapağı ve görselleri tek kontakta Naz'a gönder, onay al.

## 7. Fiyat ve bölüm → ONAY, sonra ekip kontrolü
- Fiyat ve dükkân bölümü için Naz'a **önerili** soru sor: "Fiyat önerim X TL (KDV dahil), bölüm Y. Uygun mu?" Naz'ın söylediği fiyat KDV dahildir, Etsy'ye aynen girilir. Gerekirse diğer kararları (indirim, kişiselleştirme) da aynı mesajda sor.
- Onaydan sonra ekibi **birer kez** çalıştır, bağımsız oldukları için aynı anda:
  - **Nesli (Etsy)** (`nesli-etsy`): başlık, açıklama, 13 etiket, alt metinler; Naz'ın onayladığı fiyat ve bölümü kullanır, kendisi değiştirmez. Görselleri yeniden üretmez, 6. adımdakileri kullanır.
  - **Ada** (`ada`): PDF sayfaları ve ilan görselleri.
  - Ardından **Nazlı** (`nazli`): Nesli'nin metinleri ve PDF'deki yazılar.
- Bulunan hataları ana oturum düzeltir. Ajanları ikinci kez çalıştırma; yalnızca büyük bir değişiklik olduysa Naz'a sor.

## 8. Etsy taslağı
İlanı Etsy'de **taslak** olarak tek işte aç (`etsy_lister/README.md`). Sonucu `goster` ile kontrol et. Yayınlama: yayın ilan başına 0,20 $ tutar ve Naz'ın kararıdır. Naz'a taslak linkini ver.

## 9. Kapanış
`OTURUM_ISLERI.md`'ye bu ürünün bölümünü yaz, ürünün güncel dosyalarını master'a aktar (kurallar `CLAUDE.md`'de). Naz'a tek mesajla söyle: taslak linki, neyin bittiği, onun yapacağı tek şey (taslağa bakıp yayınlamak) ve "oturumu kapatabilirsin".

## Bu akış değişirse
Naz'ın sabitlediği görsel kılavuz aynı adımları gösterir: `docs/naz-etsy-urun-yolu.html` (claude.ai'de "Etsy Ürün Yolu" sayfası, slug `f4cbb6d4-0bae-4d31-8ae1-c08b70d481c7`). Bu dosyada bir adım değişirse kılavuzu da aynı oturumda güncelle ve yeniden yayınla.
