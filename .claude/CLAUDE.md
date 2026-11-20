# SpecialNStudio: ekip kuralları (bu depo)

- Naz ile Türkçe konuş. Almanca ya da İngilizce her metnin Türkçesini de yaz.
- Ekip komutlarının ve ajanlarının **asıl kopyası `specialnstudio1` deposundadır** (`.claude/agents/`, `.claude/commands/`). Bu depodaki dosyalar oradan kopyalandı. Bir ajanı ya da komutu değiştireceksen önce `specialnstudio1` içinde değiştir, sonra bütün depolara aynen kopyala.
- Ajan ve komut metinlerinde adı geçen `OTURUM_ISLERI.md`, `HAFIZA.md`, `FIKIRLER.md`, `specialnstudio/` klasörü ve `etsy_lister/` yalnızca `specialnstudio1` deposundadır. O depo oturuma bağlıysa oradan oku; bağlı değilse o adımı atla ve bunu raporda söyle.
- Kalıcı hafıza `specialnstudio1` deposunun master dalındaki `HAFIZA.md` dosyasıdır: oturum başında oku, Naz bir tercih ya da karar bildirince `/hafıza` ile not ekle (talimat: `specialnstudio1/.claude/skills/hafiza/SKILL.md`).

## Ekip: komutlar ve ajanlar
Bundan sonraki bütün işlerde bu ekip kullanılır. Naz komutu yazınca (`/ada` gibi) ilgili ajan çalışır; Naz yazmasa da işin sırası gelince ajanı kendin çalıştır. Komutlar `.claude/commands/`, ajanlar `.claude/agents/` içinde.

| Komut | Ajan | Ne yapar |
| --- | --- | --- |
| `/ada` | Ada, tasarım direktörü (`ada`) | Bütün tasarımları kontrol eder: çizgi kayması, sapma, fazladan nokta, taşma, tutarsızlık; trendlere ve bütün görünüme göre değerlendirir, öneri verir. Dosya değiştirmez. |
| `/nazlı` | Nazlı, dil editörü (`nazli`) | Türkçe, Almanca, Danca ve İngilizce metinleri anadili düzeyinde kontrol eder ve oturumun belgelerinde yerinde düzeltir. |
| `/aslı` | Aslı, avukat (`asli`) | E-ticaret, dijital ürün ve web sitesi hukuku: gereken belgeleri çıkarır, verilenleri kontrol eder, düzenler ve üretir. |
| `/nesli` | Nesli, pazarlama uzmanı (`nesli`) | Ürünü 360 derece ele alır: satış yerine göre strateji, tarihli plan, reklam planı, sosyal medya içeriği, plana bağlı görsel ve video. |
| `/nesli-ürün` | Nesli, ilan tasarımcısı (`nesli-urun`) | İlan görsellerini tasarlar; platforma göre başlık, açıklama, SEO, etiket ve alt metin. |
| `/nesli-etsy` | Nesli, Etsy ilan uzmanı (`nesli-etsy`) | Ürünün Etsy ilanını baştan sona hazırlar: görseller ve alt metinler, video, başlık, açıklama, 13 etiket, fiyat, bölüm; ilanı Etsy'de taslak olarak açar. Yayınlamaz. |
| `/nesli-araştırma` | Nesli, ürün araştırmacısı (`nesli-arastirma`) | Etsy, Google Trends ve bütün webde trend ve yeni ürün araştırması; yeni fikirler. |
| `/ahmet-kontrol` | Ahmet, web tasarımcısı (`ahmet`) | Sitenin tasarımını, altyapısını, yeteneklerini ve özelliklerini inceler. Dosya değiştirmez. |
| `/ahmet-bastır` | Ahmet, web tasarımcısı (`ahmet`) | Sitenin nasıl olması gerektiğini belirler, eksikleri söyler ve siteyi iyileştirir. |
| `/siteye-ekle` | Skill (Nazlı, Ada ve Nesli'yi çalıştırır) | Türkçe, İngilizce ya da Almanca ürünü bastirkullan.com'a ekler: katalog, satılan dosyalar, siteye özel metin, vitrin görseli (vitrin görsel aracı); Nazlı, Ada ve Nesli (SEO) kontrolünden sonra sitede yayına alır. Skill `.claude/skills/siteye-ekle/` içinde. |

Türkçe harfli komutların harfsiz eşleri de var: `/nazli`, `/asli`, `/nesli-urun`, `/nesli-arastirma`, `/ahmet-bastir`.

Ne zaman kim:
- Bir metin yazıldığında ya da çevrildiğinde, Etsy'ye ya da siteye yüklemeden önce: **Nazlı**. Nesli'nin ve Aslı'nın ürettiği metinler de Nazlı'dan geçer.
- Bir tasarım (PDF, kart, oyun parçası, ilan görseli, sosyal medya görseli) üretildiğinde ya da değiştiğinde, yayından önce: **Ada**.
- Bir ürün Etsy'de ilk kez listelenirken (ilanın tamamı ve taslak): **Nesli (Etsy)**. Yalnızca görsel ya da metin iyileştirilirken ve başka platformlarda: **Nesli (ürün)**. Ürün yayına çıkarken ve sosyal medya, reklam işlerinde: **Nesli**.
- Yeni ürüne başlamadan ya da Naz "sıradaki ürün ne" diye sorunca: **Nesli (araştırma)**, `FIKIRLER.md` ile birlikte.
- Bir web sitesi ya da satış sayfası işinde: önce **Ahmet (kontrol)**, sonra **Ahmet (bastır)**; sitenin hukuki belgeleri için **Aslı**.
- Ajanlar rapor verir; commit, push, Etsy ve Metricool işlemlerini ana oturum yapar. Yayınlama, reklam ve para harcayan her şey Naz'ın onayıyla olur.

Adlar: sosyal medya stratejistinin adı 18 Kasım 2026'da "Nazlı"dan **Nesli**'ye değişti (`specialnstudio/` klasörü). **Nazlı** yalnızca dil editörüdür. **Ada** tek başına tasarım direktörüdür; `specialnstudio/ada_prompt.md` Nesli'nin içerik üretim modülünün brief'idir.
