# SpecialNStudio: ekip kuralları (bu depo)

- Naz ile Türkçe konuş. Almanca ya da İngilizce her metnin Türkçesini de yaz.
- Ekip komutlarının ve ajanlarının **asıl kopyası `specialnstudio1` deposundadır** (`.claude/agents/`, `.claude/commands/`). Bu depodaki dosyalar oradan kopyalandı. Bir ajanı ya da komutu değiştireceksen önce `specialnstudio1` içinde değiştir, sonra bütün depolara aynen kopyala.
- Ajan ve komut metinlerinde adı geçen `OTURUM_ISLERI.md`, `FIKIRLER.md`, `specialnstudio/` klasörü ve `etsy_lister/` yalnızca `specialnstudio1` deposundadır. O depo oturuma bağlıysa oradan oku; bağlı değilse o adımı atla ve bunu raporda söyle.

## Ekip: komutlar ve ajanlar
Bundan sonraki bütün işlerde bu ekip kullanılır. Naz komutu yazınca (`/ada` gibi) ilgili ajan çalışır. **Ajanlar yalnızca Naz çağırınca ya da bir görevin sonunda, yayından önce bir kez çalışır; her değişiklikten sonra kendiliğinden çalıştırılmaz** (Naz, 19 Kasım 2026: ajan turları çok kaynak harcıyor). Küçük düzeltmeleri ana oturum kendisi yapar; görev bitince hangi ajanların bakmadığını Naz'a söyler, Naz isterse çağırır. Komutlar `.claude/commands/`, ajanlar `.claude/agents/` içinde.

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

Türkçe harfli komutların harfsiz eşleri de var: `/nazli`, `/asli`, `/nesli-urun`, `/nesli-arastirma`, `/ahmet-bastir`.

Kim neye bakar (çağrıldığında ya da görev sonunda):
- Metinler (yazılan, çevrilen; Etsy'ye ya da siteye yüklemeden önce): **Nazlı**. Nesli'nin ve Aslı'nın ürettiği metinler de Nazlı'dan geçer.
- Bir tasarım (PDF, kart, oyun parçası, ilan görseli, sosyal medya görseli) yayından önce: **Ada**.
- Bir ürün Etsy'de ilk kez listelenirken (ilanın tamamı ve taslak): **Nesli (Etsy)**. Yalnızca görsel ya da metin iyileştirilirken ve başka platformlarda: **Nesli (ürün)**. Ürün yayına çıkarken ve sosyal medya, reklam işlerinde: **Nesli**.
- Yeni ürüne başlamadan ya da Naz "sıradaki ürün ne" diye sorunca: **Nesli (araştırma)**, `FIKIRLER.md` ile birlikte.
- Bir web sitesi ya da satış sayfası işinde: önce **Ahmet (kontrol)**, sonra **Ahmet (bastır)**; sitenin hukuki belgeleri için **Aslı**.
- Ajanlar rapor verir; commit, push, Etsy ve Metricool işlemlerini ana oturum yapar. Yayınlama, reklam ve para harcayan her şey Naz'ın onayıyla olur.

Adlar: sosyal medya stratejistinin adı 18 Kasım 2026'da "Nazlı"dan **Nesli**'ye değişti (`specialnstudio/` klasörü). **Nazlı** yalnızca dil editörüdür. **Ada** tek başına tasarım direktörüdür; `specialnstudio/ada_prompt.md` Nesli'nin içerik üretim modülünün brief'idir.
