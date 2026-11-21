---
name: urun
description: "Yeni ürün akışı: brief'ten satışa kadar sabit sıra, üç çıkış: Etsy taslağı, Bastır Kullan (bastirkullan.com) ya da Amazon KDP basılı kitap. Az token ve az GitHub Actions dakikasıyla çalışır, her onay noktasında Naz'ı bekler. Naz \"/ürün\", \"/etsy-ürün\", \"/site-ürün\", \"/kdp-ürün\" (ya da harfsiz eşlerini) yazdığında, bir brief verip yeni ürüne başladığında, \"Etsy işi\", \"siteye yeni ürün\", \"KDP kitabı\", \"yeni ürün\" dediğinde kullan."
argument-hint: "[etsy | site | kdp] [brief ya da briefler/ içindeki dosya]"
---

# /ürün: brief'ten satışa (Etsy, Bastır Kullan, Amazon KDP)

Bu akış sabittir: adımları sırayla yap, atlama, sıra değiştirme. 1–8. adımlar her çıkışta aynıdır (ürünü üretmek), sonra seçilen çıkışın adımları gelir. Naz ile Türkçe konuş, teknik kelime kullanma. Her onay noktasında **dur ve Naz'ın cevabını bekle**. Onay isterken tek mesajda, numaralı ve kısa sor.

**Çıkış:** komut söylüyorsa (`/etsy-ürün` → Etsy, `/site-ürün` → Bastır Kullan, `/kdp-ürün` → KDP) onu kullan. Söylemiyorsa 3. adımda sor.

## Tasarruf kuralları (her adımda geçerli)
- **Bir oturum = bir ürün, bir dil, bir çıkış.** Bitince Naz'a "oturumu kapatabilirsin" de; ikinci işe bu oturumda başlama.
- **Aynı ürün birden çok yere gidecekse sıra:** önce Etsy, sonra Bastır Kullan (Etsy görsellerini kullanır), sonra KDP. Her biri ayrı oturumdur. Ürün daha önce üretildiyse 4–8. adımları atla, master'daki dosyaları kullan.
- Ajanlar (Ada, Nazlı, Nesli) yalnızca çıkışın ekip adımında, **birer kez** çalışır.
- Görselleri ve sayfaları tek tek açma: önce kontak (tek görselde küçük önizlemeler) yap, onu bir kez oku. Naz'a önizlemeleri tek seferde gönder, düzeltmeleri tek listede iste.
- GitHub Actions: hata veren işi hemen yeniden gönderme; önce kaydını oku, nedeni düzelt, bir kez gönder. İşi gönderip iptal etme. Birden çok ilan varsa tek işte yükle. Başka oturumun Etsy işi çalışıyorsa bitmesini bekle.
- Eski oturumları ve `OTURUM_ISLERI.md`'nin tamamını okuma; yalnızca bu ürünün bölümü ve gereken README.

## Ortak üretim

### 1. Araştırma ve brief (Naz, kod oturumu dışında)
Chrome eklentisinde ya da sohbette yapılır. Burada yapılmaz.

### 2. Depo kontrolü
- Etsy ve KDP: yalnızca `specialnstudio1`. Bastır Kullan: `specialnstudio1` ve `specialnstudio` (site deposu).
- Gereken depo bağlı değilse dur ve Naz'a hangi depolarla yeni oturum açacağını söyle. Fazladan depo bağlıysa bir kez, tek cümleyle söyle ve devam et.
- `HAFIZA.md`'yi (master) oku, notlarına uy.

### 3. Brief'i al, eksikleri tek seferde sor
Brief'ten çıkar: ürün türü, **dil** (her dil ayrı ürün), çıkış, sayfa boyutu (TR/DE A4, EN US Letter; KDP için 9. adımda kitap ölçüsü), sayfa sayısı ve içerik, yaş ya da hedef kitle, beğenilen örnekler, istenmeyenler, hazır dosya var mı.
Eksikleri **tek mesajda** sor. Aynı mesajda: çıkış belli değilse "Etsy mi, siteye mi, KDP kitabı mı?"; ve "Görselleri fal.ai'de ben mi üreteyim, sen mi yaptıracaksın, hazır dosyan var mı?"
- Bastır Kullan: Türkçe, İngilizce ya da Almanca olur (sitede başka dilin kategorisi yok).
- KDP: yalnızca İngilizce (amazon.com) ya da Almanca (amazon.de); KDP Türkçe kitap kabul etmiyor. Türkçe istenirse söyle ve dur.
Brief uzunsa `briefler/<ürün>.md` olarak kaydet.

### 4. Kısa plan → ONAY
5–8 madde: sayfa listesi, tarz, görsellerin kaynağı, dosya biçimi, çıkış. KDP'de plan kitap düzenine göre yazılır (başlık sayfası, künye, "nasıl kullanılır", içerik, varsa cevap anahtarı; kesilecek sayfanın arkası boş). Onaysız üretme.

### 5. Tarz soruları → ONAY (görsel üretilecekse)
4–6 kısa soru (çizim tarzı, renkler, karakterler ve yaş görünümü, arka plan, yazı, kaçınılacaklar), mümkünse 2–3 seçenekle. Cevaplardan tek paragraflık **tarz kartı** yaz, onay al. Bundan sonra tarz değişmez; her prompt bu karttan türetilir.

### 6. Görseller
- **fal.ai (Naz istediyse):** onay mesajında kaç görsel, hangi model olduğunu yaz. Önce 1–2 deneme göster; beğenilince kalanını tek seferde üret. Onaylanan sayıyı aşma. Model bilgisi `HAFIZA.md`'de.
- **Naz yaptıracaksa:** tarz kartından her görsel için ayrı, kopyalanabilir blokta İngilizce prompt ve altında Türkçesi (Gemini için).
- **Hazır dosya:** 6–8. adımları atla.
- KDP boyama kitabında çizimler siyah-beyaz ve baskıya uygun çözünürlükte olur (300 dpi).

### 7. Örnek sayfalar → ONAY
Önce 1–2 örnek sayfa; onaydan sonra hepsi.

### 8. Düzeltme listesi
Bütün sayfaları tek kontakta göster, düzeltmeleri Naz'dan **tek numaralı listede** iste, hepsini birden yap.

## Çıkış A: Etsy

**9. Kapak ve ilan görselleri → ONAY.** `etsy-gorsel` skill'i (`.claude/skills/etsy-gorsel/SKILL.md`): kapak, 7 görsel, video, alt metinler. Henüz yükleme; tek kontakta onay al.

**10. Fiyat ve bölüm → ONAY.** Öneriyle sor: "Fiyat önerim X TL (KDV dahil), bölüm Y. Uygun mu?" Naz'ın fiyatı KDV dahildir, Etsy'ye aynen girilir.

**11. Ekip (birer kez).** Aynı anda `nesli-etsy` (başlık, açıklama, 13 etiket; onaylı fiyat ve bölümü değiştirmez, görsel üretmez) ve `ada` (PDF ve ilan görselleri); sonra `nazli` (bütün metinler). Hataları ana oturum düzeltir.

**12. Etsy taslağı.** Tek işte taslak aç (`etsy_lister/README.md`), `goster` ile kontrol et, linki ver. Yayın Naz'ın kararı (ilan başına 0,20 $).

**13. Kapanış** (aşağıda).

## Çıkış B: Bastır Kullan (bastirkullan.com)

**9. Fiyat ve kategori → ONAY.** Öneriyle sor: "Site fiyatı önerim X TL (KDV dahil), kategori Y. Uygun mu?" Kategoriler `siteye-ekle` skill'inde. Ürün Etsy'de de satılıyorsa Etsy fiyatını da söyle.

**10. Siteye ekle ve yayına al.** `siteye-ekle` skill'ini çalıştır (`.claude/skills/siteye-ekle/SKILL.md`): katalog, satılan dosyalar, Türkçe site metni, vitrin görseli (Etsy görselleri varsa onlar), Nazlı, Ada ve Nesli (ürün) kontrolü, hatasızsa yayın. 9. adımdaki onay, bu yayının onayıdır. Ekip bu skill'in içinde birer kez çalışır; ayrıca çağırma.

**11. Naz'ın kontrolü.** Naz'a ürün sayfasının linkini ver; sayfaya telefondan bakmasını iste.

**12. Kapanış** (aşağıda).

## Çıkış C: Amazon KDP (basılı kitap)

KDP'ye dosyaları Claude yükleyemez (Amazon'un bunun için bir yolu yok): Claude dosyaları ve adım adım yükleme kılavuzunu hazırlar, Naz yükler. Örnek olarak önceki kitaba bak: `projects/prenses-oyunlar/10-KDP/` (`README.md`, `YUKLEME_ADIMLARI.md`) ve `projects/prenses-oyunlar/09-Quality-Control/tools/kdp.py`.

**9. Kitap ayarları → ONAY.** Öneriyle sor:
- Pazar: EN → amazon.com, DE → amazon.de.
- Ölçü: EN 8.5 × 11 in, DE 8.27 × 11.69 in (A4), ya da üründe başka.
- Mürekkep: boyama ve yazı kitabında **siyah-beyaz** (baskı çok daha ucuz, satış fiyatı düşük kalır); renkli içerikte Premium Color.
- Taşma (bleed): kenara kadar resim yoksa "No bleed". Kapak yüzeyi: mat ya da parlak (Naz seçer).
Kurallar güncellenebilir: kenar payı, sırt kalınlığı ve sayfa sınırlarını KDP yardım sayfasından o gün kontrol et.

**10. İç sayfalar (kitap PDF'i).** Sayfa sayısı çift; dış kenar ve cilt payı KDP'nin sayfa sayısına göre istediği kadar; başlık sayfası, künye ("© SpecialNStudio", yıl, yapay zekâ notu gerekiyorsa), "bu kitap nasıl kullanılır"; kesilecek ya da boyanacak her sayfa sağda ve arkası boş. Dijital üründen farklı olan sayfaları (ör. mürekkep dostu sürümler) çıkar.

**11. Kapak → ONAY.** Arka + sırt + ön tek PDF, her yanda 0,125 in taşma. Sırt kalınlığı sayfa sayısı ve kâğıda göre hesaplanır; KDP sırta yazıyı yalnızca belli bir sayfa sayısının üstünde kabul eder. Arka kapakta sağ altta barkod için boş alan. Önizlemeyi onaya gönder.

**12. Fiyat → ONAY.** Baskı maliyetini (KDP'nin hesaplayıcısı) ve bu fiyattaki yaklaşık telifi yaz, bir fiyat öner, onay al.

**13. Ekip (birer kez).** Aynı anda `nesli-urun` (KDP metinleri: başlık, alt başlık, açıklama, 7 anahtar kelime, 3 kategori, okuma yaşı) ve `ada` (iç sayfalar ve kapak: kenar payı, sırt, kesim çizgisi); sonra `nazli` (bütün metinler).

**14. Yükleme kılavuzu.** Ürün klasöründe `KDP/README.md` (ayarlar tablosu) ve `KDP/YUKLEME_ADIMLARI.md` (Naz için, önceki kitaptaki gibi: hangi sayfada hangi alana ne yazılacak, metinler kopyalanabilir, yapay zekâ bildirimi dürüstçe "Yes"). Naz'a söyle: yükle, "Print Previewer"da uyarılara bak, **deneme baskısı (proof copy) sipariş et**, beğenince yayınla. Vergi ve banka bilgileri KDP hesabında tamam olmalı.

**15. Kapanış** (aşağıda).

## Kapanış (her çıkışta)
`OTURUM_ISLERI.md`'ye bu ürünün bölümünü yaz, ürünün güncel dosyalarını master'a aktar (kurallar `CLAUDE.md`'de). Naz'a tek mesaj: link (Etsy taslağı, site sayfası ya da KDP dosyaları), neyin bittiği, onun yapacağı tek şey ve "oturumu kapatabilirsin".

## Bu akış değişirse
Naz'ın sabitlediği görsel kılavuz aynı adımları gösterir: `docs/naz-etsy-urun-yolu.html` (claude.ai'de "Ürün Yolu" sayfası, slug `f4cbb6d4-0bae-4d31-8ae1-c08b70d481c7`). Bu dosyada bir adım değişirse kılavuzu da aynı oturumda güncelle ve yeniden yayınla.
