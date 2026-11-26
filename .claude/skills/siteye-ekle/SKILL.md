---
name: siteye-ekle
description: Etsy'deki (ya da Etsy'ye eklenmek üzere hazırlanan) Türkçe, İngilizce ya da Almanca bir ürünü bastirkullan.com'a uygun hâle getirir ve sitede yayına alır. Görseller, sayfa metni, SSS, yapısal veri, iç bağlantılar ve SEO dâhil ürünü tek seferde eksiksiz hazırlar; kapak olarak Etsy ilan görsellerini kullanır (Etsy kapak görselleri `tools/vitrin_kart.py` ile uyarlanır; vitrin aracı varsa onu). Ada (tasarım), Nesli (SEO) ve Nazlı (dil) kontrolünden ve `--seo-kontrol` derlemesinden geçirir, hatasız olunca yayınlar, canlı sitede kontrol eder. Naz "/siteye-ekle" yazdığında, "bu ürünü siteye ekle", "sitede yayına al" dediğinde kullan.
argument-hint: "[Etsy ilan numarası, ürün klasörü ya da boş: oturumun ürünü]"
---

# /siteye-ekle: ürünü Bastır Kullan sitesine ekle ve yayına al

Naz bu skill'i çalıştırdığında **bu ürünün sitede yayına alınmasını onaylamış olur**. Yayın, aşağıdaki bütün kontroller geçtiyse yapılır. Bir kontrol kalırsa ya da bir bilgi eksikse yayınlama, Naz'a neyin eksik olduğunu söyle.

**Hedef:** ürün tek seferde, eksiksiz ve kontrol edilmiş olarak sitede çıksın: görseller, sayfa metni, SSS, yapısal veri, iç bağlantılar, SEO ve canlı kontrol. Birden fazla ürün eklenirken her ürün için 1–3. bölümleri ayrı ayrı yap, kontrolleri (4. bölüm) hepsine birlikte çalıştır.

**Bilgi kuralı:** ürünle ilgili her bilgi (içerik, sayfa sayısı, boyut, yaş, biçim, kullanım) yalnızca ürünün kendi dosyalarından (satılan PDF/ZIP, `teslim.json`) ve Etsy ilanından (metin, etiketler, özellikler, görseller) alınır. Bulamadığın bilgiyi uydurma, yazma; gerekiyorsa Naz'a sor.

Naz ile Türkçe konuş. Her adımda kısa bilgi ver, sonunda tek bir rapor yaz. Token ve GitHub kullanımını az tut: dosyaları bir kez oku, ekran görüntüsünü yalnızca kontrol adımlarında al, sitenin deposuna tek kayıt ve tek push yap.

## 0. Hazırlık

1. **Site deposu:** `specialnstudio` (bastirkullan.com). Bu skill yalnızca Claude Code oturumunda çalışır (claude.ai sohbetinde depo ve derleme yoktur).
   - Depo oturumda klasör olarak varsa (`specialnstudio/` ya da çalışma klasörünün yanında), onu kullan ve `git fetch origin main && git checkout -B urun-ekle origin/main` ile güncel `main`'e geç.
   - Yoksa `add_repo` aracı varsa onunla ekle (`specialnstudio-cmyk/specialnstudio`, push yetkisiyle) ve verdiği komutla klonla.
   - `add_repo` yoksa `git clone https://github.com/specialnstudio-cmyk/specialnstudio.git` dene.
   - Hiçbiri olmazsa dur ve Naz'a söyle: oturuma `specialnstudio` deposunu da seçerek yeni bir oturum açmalı.
2. Şunları oku, başka dosya okuma:
   - `specialnstudio/PROJECT-STATUS.md`
   - `specialnstudio/README.md`: "Ürün eklemek", "Mağaza kapakları", "Arama motorları (SEO)", "Yönetim panosu" ve "Sepet, ödeme ve teslim" bölümleri.
3. **Ürünün kaynağı (sırayla bak):**
   - Argümanda Etsy ilan numarası, klasör ya da dosya varsa o.
   - Yoksa oturumda üzerinde çalışılan ürün: ilan metni (`specialnstudio1/listings/` ya da oturumun ürün klasörü), satılan PDF/ZIP dosyaları, ilan görselleri.
   - `specialnstudio/catalog/etsy.json` ve `catalog/urunler.json`'da aynı Etsy numarasıyla gizli bir taslak varsa (Etsy köprüsü ekler), yeni ürün açma: o taslağı tamamla.
4. **Sürüm kontrolü:** `main`'de `catalog/site_metin.json` ve `tools/kesit_uret.py` yoksa yeni site tasarımı henüz yayına alınmamış demektir. Dur ve Naz'a söyle: önce yeni tasarım (`claude/quirky-gates-2o26rd` dalı) `main`'e alınmalı.
5. **Dil kuralı:** iki dilli ürün olmaz; her dil ayrı üründür.
   - Türkçe ürün: Türkçe kategorilerden biri (Çocuk ve aile, Dijital planlayıcı, Yazdırılabilir ajanda, Planlayıcı uygulamaları, Düğün ve davet).
   - İngilizce ürün: `english` ana kategorisinin alt kategorilerinden biri (`en-planners`, `en-christmas`, `en-kids`, `en-parties`).
   - Almanca ürün: `deutsch` altında (`de-advent`, `de-spiele`).
   - Başka bir dil (örn. Danca): sitede kategorisi yok, dur ve Naz'a söyle.
   - Ürünün `ad` alanı ürünün kendi dilinde kalabilir. Sitedeki bütün açıklamalar (`ozet`, `site_metin.json`, `ozellik.json`) Türkçe yazılır ve ürünün dilini açıkça söyler.

## 1. Ürünü kataloğa ekle (`specialnstudio` deposu)

Mevcut ürünlerin biçimini örnek al, alanları aynı adlarla yaz. `tools/etsyden_al.py` ÇALIŞTIRILMAZ (kataloğu baştan yazar, pano değişikliklerini siler).

1. **Kimlik ve adres:** kısa, Türkçe harfsiz, tireli (örn. `kina-gecesi-seti`). Taslak varsa onun kimliğini kullan. Sayfa adresi `/urun/<kimlik>/` olur; kimlik ürünü anlatsın (ürün türü + tema ya da fark, 2–5 sözcük, örn. `yilbasi-boyama-kitabi-2-4-yas`), Etsy başlığının uzun hâli, sayı dizisi ya da `-2` gibi ek olmasın. Etsy köprüsünün açtığı taslağın kimliği uzunsa ya da ürünü anlatmıyorsa `urunler.json`'daki `adres` alanına kısa bir adres yaz (yalnızca `a-z`, `0-9`, `-`; Worker eski adresi yenisine yönlendirir); görsel klasörü ve diğer kayıtlar kimlikle kalır.
2. **`catalog/urunler.json`:**
   - `ad`: Etsy başlığının kısa, okunur hâli; anahtar sözcük yığını olmaz.
   - `ozet`: tek satır, sonu noktasız; bu ürüne özgü (aşağıdaki "aynı türden birden fazla ürün" kuralı). **Boş bırakılmaz:** boşsa derleme açıklama kuramaz ve SEO kontrolü "açıklama eksik" hatası verir.
   - `kategori`: var olan kategorilerden uygunu.
   - `fiyat`: Etsy fiyatı × 1,20 (KDV dâhil), 2 ondalığa yuvarla. Fiyat belli değilse Naz'a sor.
   - `aciklama`: Etsy metni.
   - `etiketler`, `gorseller` (ilan görselleri; `NN.jpg` 1400, `NN_k.jpg` 560, `NN_m.webp` 160, `catalog/img/<kimlik>/` içinde), `etsy` (ilan numarası).
   - `yayinda`: yayına alma adımına kadar `false` kalır.
3. **Satılan dosyalar:** `dosyalar/<kimlik>/` içine koy (tek dosya en çok 25 MB; büyükse böl ya da Naz'a söyle). `catalog/teslim.json`'a her dosya için `dosya`, `ad` (alıcının göreceği ad) ve `mb` yaz. Satılan dosya yoksa ürün yayına alınamaz: dur ve Naz'a hangi dosyanın gerektiğini söyle.
4. **`catalog/ozellik.json`:** `tur`, `ton`, `yazdir` (yalnızca yazdırılabilirde), `bakista` (5–8 satır, gerçek bilgiler) ve `hizli`: `icerik`, `format`, `uyum`, `teslim`. Boş bırakılanlar türetilir; yanlış olacaksa yaz.
5. **`catalog/site_metin.json`:** `urunler.<kimlik>`:
   - `tanim`: arama sonucu açıklaması, **zorunlu, 120–160 karakter** (boşluklar dâhil). Ürünün ne olduğu, kime göre olduğu, biçimi. **Yalnızca bu ürünün sayfasındaki bilgilerden yaz** (`ad`, `ozet`, `ozellik.json`, `giris`, `teslim.json`'daki dosyalar); sayfada olmayan bir bilgi, sayı ya da vaat ekleme. Ürüne özgü olsun: temanın ya da varyasyonun adını ve bu ürünü ayıran en az bir içerik ayrıntısını söylesin. **Sitedeki başka hiçbir sayfanınkiyle aynı olmasın**, neredeyse aynı da olmasın.
   - `giris`: 2 paragraf, Etsy metninden FARKLI, "sen" hitabıyla. **O ürüne özgü olsun:** içinde neler var, kaç sayfa ya da parça, boyut (A4, US Letter, ekran), kimin için (yaş, kullanıcı), nasıl kullanılır (yazdır, Canva'da düzenle, tablette aç). Bilgiler yalnızca üründen ve Etsy ilanından gelir (yukarıdaki bilgi kuralı); bilinmeyeni yazma.
   - Kategorinin `sss` listesi yoksa 2–4 soru-cevap ekle.
   - **Ürüne özel SSS:** `urunler.<kimlik>.sss` alanına 3–5 kısa soru-cevap yaz (`[["Soru?", "Cevap."], ...]`). Doluysa ürün sayfası kategorinin SSS'i yerine bunu gösterir ve FAQPage yapısal verisi de bunu izler. Sorular bu ürüne özgü olsun (ne kadar sürede biter, hangi kâğıda basılır, Canva hesabı gerekir mi, kaç kişi oynar gibi), cevaplar yalnızca üründen ve Etsy ilanından.
6. **Arama başlığı (`<title>`):** her yeni ürüne, uzunluğuna bakılmadan, `catalog/seo.json` → `"/urun/<kimlik>/"` → `baslik` alanına ekisiz bir başlık yazılır (Naz, 26 Kasım 2026). Başlığı 4. bölümde **Nesli (ürün)** önerir, Nazlı bakar; sen yazma, `ad` + " | Bastır Kullan" otomatik başlığına da bırakma.
   - Kurallar: 20–60 karakter, " | Bastır Kullan" eki yok, büyük harfle yazılmış başlık, emoji ve ünlem yok. İngilizce üründe sonda "(İngilizce)", Almanca üründe "(Almanca)" yazar, Türkçede işaret yok. Başlık aranan sözcükle başlasın, temanın ya da varyasyonun adı sonda olsun. Başka hiçbir sayfanın başlığıyla aynı olmasın (örn. `"Bekârlığa Veda Web Sitesi ve Parti Seti: Y2K Pop Gelin"`).
   - Başlığı elle `seo.json`'a yazma: 4. bölümün 4. adımında `tools/seo_toplu.py` ile yaz.
   - Bu alan ekisiz kullanılır, `og:title` da onu izler; ürünün `ad`'ı ve H1'i değişmez. Açıklamayı da buraya yazma, açıklama `site_metin.json` → `tanim`'dadır.
7. **Aynı adlı ya da aynı türden birden fazla ürün** (aynı ürünün temaları, renkleri ya da varyasyonları; Etsy'de aynı başlıkla duran ilanlar) birlikte eklenince her biri **farklı başlık ve farklı açıklama** alır; `tanim`, `ozet` ve başlığı her biri için ayrı yaz. Bir ürünün metnini kopyalayıp yalnızca adını değiştirme; her biri kendi temasını ve kendi farkını söylesin. **Farkı başlıkta söyle:** renk, tema, sayfa sayısı, yaş ya da sürüm (örn. "Yılbaşı Fotoğraf Kartı Şablonu: Kırmızı Ekose", "Yılbaşı Boyama Kitabı 2-4 Yaş, 30 Sayfa"). Ürünlerin `ad`'ı aynı kalsa da 6. maddedeki `seo.json` başlıkları farklı olur; aynı başlık iki sayfada olursa SEO kontrolü geçmez.
8. **Etsy'ye özgü görseller:** üzerinde "Etsy" yazan ilan görselleri (Etsy'deki indirme adımları) sitede gösterilmez. `build.py` → `ETSY_YAZILI` listesine ekle (2. bölümde dosyaya verdiğin anlamlı adla).
9. **Rehber bağlantısı:** `pages/rehber/` içinde konusu bu ürüne uyan bir yazı varsa ürünü o yazının `urunler:` satırına ekle. Yazının gövdesinde ürünün konusunun geçtiği bir yer varsa oraya ürün sayfasına bir metin bağlantısı da ver (`<a href="/urun/<kimlik>/">…</a>`); yazının metnini başka türlü değiştirme.
10. **İlgili ürünler:** ürün sayfasının altındaki "Bunlara da bak" bölümü 4 ürünü kendisi seçer: yalnızca aynı dildeki ürünlerden, ortak etiketi en çok olandan başlayarak; ortak etiketli ürün yetmezse aynı kategoriden, o da yetmezse satıştaki diğer ürünlerden (aynı ürünün diğer seçenekleri hariç). Bu yüzden `etiketler` ürünün gerçek konusunu söylemeli (tema, tür, yaş, gün). 3. bölümde 3–4 ürünün göründüğünü ve konuyla ilgili olduğunu kontrol et. İlgisiz ürünler çıkıyorsa etiketleri düzelt; düzelmiyorsa raporda söyle.

## 2. Görseller

Sitede kullanılan görseller ürünün **Etsy ilan görselleridir**: 1. görsel (Etsy kapağı) sitenin ürün görseline uyarlanır, diğerleri ürün sayfasının galerisinde kullanılır. Aşağıdaki 2.1–2.5 her üründe zorunludur.

### 2.1 Dosyalar: anlamlı ad, WebP, küçültülmüş

Etsy görselleri `catalog/img/<kimlik>/` içine şu adlarla konur (Etsy köprüsünün indirdiği `01.jpg`, `02.jpg`... varsa yeniden adlandır, eski `NN*` dosyalarını sil):

- Ad: `<kimlik>-<ne gösterdiği>`, Türkçe harfsiz, tireli. İlk görsel `<kimlik>-kapak`, diğerleri içeriğine göre (örn. `yilbasi-boyama-kitabi-ornek-sayfalar`, `-paket-icerigi`, `-olculer`). Aynı ad iki kez olmaz.
- Her görsel için dört dosya (Pillow ile; en uzun kenar):
  - `<ad>.jpg`: 1400 px, JPEG kalite 82. Paylaşım görseli (og:image), site haritası ve Shopier için; bu platformlar WebP'yi her zaman kabul etmez.
  - `<ad>.webp`: 1400 px, WebP kalite 82. Sayfada gösterilen görsel.
  - `<ad>_k.webp`: 560 px, WebP kalite 78.
  - `<ad>_m.webp`: 160 px, WebP kalite 80 (galerideki küçük resim).
- `urunler.json` → `gorseller` listesinde her görsel: `{"dosya": "<ad>.jpg", "orta": "<ad>.webp", "kucuk": "<ad>_k.webp", "mini": "<ad>_m.webp", "alt": "..."}`. Sıra Etsy'deki sırayla aynı.
- Not: Etsy'de ilanın görselleri sonradan değişirse Etsy köprüsü onları yine `NN.jpg` adlarıyla indirir ve listeyi değiştirir. Bu beklenen bir durumdur; sayfa çalışmaya devam eder.

### 2.2 Alt metinler

Her görselin `alt` alanı **Türkçe**, açıklayıcı ve o görsele özgü olur: görselde ne göründüğünü söyler (örn. "Yılbaşı boyama kitabı, kardan adamlı ve geyikli dört örnek sayfa"). Ürünün dili İngilizce ya da Almanca olsa da alt metin Türkçedir. Aynı alt metin iki görselde olmaz (ne bu üründe ne sitedeki başka bir üründe); "görsel 2" gibi numaralı alt metin olmaz. Kontrol: aşağıdaki komut bu ürünün boş ya da sitede bir kez daha geçen alt metinlerini yazar; boş liste dönmeli (`<kimlik>` yerine ürünün kimliği; birden fazla ürün eklendiyse her biri için çalıştır):

```bash
python3 -c "import json,sys,collections;u=json.load(open('catalog/urunler.json'))['urunler'];c=collections.Counter(g.get('alt','').strip() for x in u for g in x.get('gorseller',[]));print([g.get('alt','') for x in u if x['kimlik']==sys.argv[1] for g in x.get('gorseller',[]) if not g.get('alt','').strip() or c[g['alt'].strip()]>1])" <kimlik>
```

Liste doluysa yalnızca bu ürünün alt metinlerini değiştir. Başka ürünlerin eski alt metinlerine dokunma (sitede aynı alt metni kullanan eski ürünler var; bu PR'ın konusu değil).

### 2.3 Etsy kapağını sitenin ürün görseline uyarla (zorunlu)

```bash
python3 tools/vitrin_kart.py <kimlik>
```

Bu araç ilk ilan görselinden (Etsy kapağı) ürün kartının kare vitrin görselini (`vkart.webp`, 640 × 640), ikinci görselden de kartın üzerine gelince görünen `vkart2.webp` dosyasını üretir. Kartın düğme yazısını ve zemin tonunu `catalog/vkart.json` dosyasına yazar. Araç çalışmazsa ürünü yayına alma, Naz'a söyle. Kartın bu araç olmadan ilk ilan görseline dönmesi bir çözüm değildir.

### 2.4 Telefon sürümleri ve ölçüler (zorunlu)

```bash
python3 tools/kucuk_surum.py <kimlik>
```

Bu araç ürün sayfasının ana görselinin `_800.webp` sürümünü ve kartın `vkart_360.webp` sürümünü üretir, ölçüleri `catalog/img/boyutlar.json` dosyasına yazar. `build.py` bu ölçülerden `width`/`height` ve `srcset` yazar. İlk görsel öncelikli (`fetchpriority="high"`) yüklenir, galerinin küçük resimleri, kartlar ve diğer görseller geç (`loading="lazy"`) yüklenir. Bunlar kendiliğinden olur, 3. bölümde kontrol edilir.

### 2.5 Paylaşım görseli (og:image)

Ürün sayfasının `og:image` etiketi ürünün ilk ilan görselidir (`<kimlik>-kapak.jpg`); `build.py` kendisi yazar. Ayrı bir şey yapma, 3. bölümde bu ürünün görseli olduğunu kontrol et (sitenin genel paylaşım görseli olmamalı).

### 2.6 Mağaza kapağı ayarı

`catalog/ayar.json` → `kapak` alanına bak.

- **`"etsy"` (varsayılan, şu anki ayar):** kapak, ürünün **Etsy ilan görsellerinin ilkidir**; vitrin aracı gerekmez. `catalog/img/<kimlik>/01.jpg` ilanın kapak görseli olmalı ve bütün görseller (`NN.jpg`, `NN_k.jpg`, `NN_m.webp`) yerinde olmalı. Etsy köprüsü Etsy'de değişen görselleri her sabah siteye kendisi taşır. Kesit gerekiyorsa (aşağıda 3. madde) yine üret, sonra 3. adıma geç.
- **`"vitrin"`:** mağaza kapağı ve sahneler vitrin görsel aracıyla üretilir (aşağıdaki maddeler).

1. **Aracı bul:**
   - `.claude/skills/` içinde adı "vitrin" geçen skill.
   - Yoksa `specialnstudio/tools/` içinde vitrin aracı ve `specialnstudio/README.md`'deki "Mağaza kapakları" bölümü.
2. **Aracı çalıştır:** aracın kendi talimatlarına göre bu ürünün kapağını (`kapak.jpg`, `kapak_o.webp`, `kapak_k.webp`, `kapak_m.webp`), sahnelerini ve `catalog/vitrin.json` kaydını üret.
3. **Kesit:** ürün ana sayfada kategori kutusunda ya da kampanyada kullanılacaksa `python3 tools/kesit_uret.py <kimlik>` ile zeminsiz kesiti de üret.
4. **Araç bulunamazsa ya da çalışmazsa:** Etsy kapağıyla devam et ve bunu raporda söyle. (Bu madde yalnızca `"vitrin"` ayarındaki mağaza kapağı içindir; 2.3'teki `vitrin_kart.py` her durumda zorunludur.)

## 3. Derle ve kendin kontrol et

1. `python3 build.py`: hata olmamalı.
2. `python3 -m http.server -d dist` ile aç. Şu ekran görüntülerini al (yalnızca sen bakacaksan deviceScaleFactor 1):
   - ürün sayfası (1440 ve 390 piksel);
   - ürünün kategori sayfasındaki kartı;
   - kapak görseli.
3. **Kontrol listesi:**
   - fiyat Etsy × 1,20 (Etsy köprüsünün açtığı taslakta fiyat zaten böyledir);
   - "Hemen al" düğmesi görünüyor (`teslim.json` dolu);
   - dört satırlık özet doğru;
   - galeride Etsy yazılı görsel yok;
   - galeride ürünün Etsy ilan görselleri Etsy'deki sırayla var; kartta `vkart.webp` görünüyor;
   - bütün görsellerde alt metin var: Türkçe, açıklayıcı ve birbirinden farklı (2.2'deki komut boş dönüyor);
   - görsel dosyaları anlamlı adlı; sayfada gösterilenler WebP. `<img>` etiketlerinde `width` ve `height` var; ilk görsel dışındakilerde `loading="lazy"` var (`grep -o '<img[^>]*/img/<kimlik>/[^>]*>' dist/urun/<kimlik>/index.html`; galerinin büyük görseli `fetchpriority="high"` taşır, küçük resimler `loading="lazy"`);
   - `og:image` bu ürünün kapak görseli;
   - adres `/urun/<kimlik>/` (ya da `adres`) kısa, Türkçe harfsiz ve ürünü anlatıyor;
   - sayfa metni (`giris`, "Teknik bilgiler", dört satırlık özet) içeriği, sayfa sayısını, boyutu, kime göre olduğunu ve nasıl kullanıldığını söylüyor; uydurma bilgi yok;
   - "Sık sorulanlar" bölümünde bu ürünün 3–5 sorusu var;
   - "Bunlara da bak" bölümünde 3–4 ilgili ürün var; uyan bir rehber yazısı varsa sayfanın altında görünüyor ve yazıdan ürüne bağlantı var;
   - ürün doğru kategoride: kategori sayfasında kartı görünüyor;
   - **SEO kontrolü:** `python3 build.py --seo-kontrol /urun/<kimlik>/` (birden fazla ürün eklendiyse hepsinin adresini ya da kimliğini boşlukla yaz) sonunda "SEO KONTROLÜ GEÇTİ." yazmalı. Bu komut şunlara bakar ve biri bozuksa hata verir:
     - derlenmiş `<title>` ek dâhil en çok 60 karakter. Bu aşamada başlık henüz otomatiktir (`ad` + " | Bastır Kullan"), çünkü `seo.json` başlığı 4. bölümde Nesli'nin önerisiyle yazılır. Bu yüzden 3. bölümde yalnızca başlık hatası çıkarsa bu normaldir; diğer hatalar düzeltilir;
     - açıklama 120–160 karakter ve yazılmış ("açıklama eksik" hatası: `ozet` ya da `tanim` boş);
     - açıklamada boş alan izi yok (": ." gibi);
     - başlık ve açıklama başka hiçbir sayfanınkiyle aynı değil.
     Ürün gizliyken (`"yayinda": false`) sayfası derlenmez ve kontrol "bu sayfa derlenmedi" der: bu adımda `yayinda` satırını geçici olarak kaldırıp derle, kontrol bitince geri koy (yayına alma 5. adımda). Komutun sonundaki "Sitenin geri kalanında … uyarı var" satırı eski sayfalar içindir, bu ürünü engellemez;
   - sayfada tek H1 var;
   - JSON-LD geçerli (Product, Offer, FAQPage, BreadcrumbList). `build.py` bunları kendisi üretir; doğru doldurulduklarını kontrol et: Product'ta `name`, `image` (bu ürünün görselleri), `description` (bu ürünün `giris` metni), `brand` (Bastır Kullan), Offer'da `price` (sitedeki fiyat), `priceCurrency` `TRY`, `availability` `InStock` (satıştaysa); BreadcrumbList'te Ana sayfa > kategori > ürün; FAQPage'de bu ürünün soruları. Hepsini `json.loads` ile ayrıştır, hata olmamalı:
     `python3 -c "import re,json,sys;t=open(sys.argv[1]).read();[print(json.loads(b)['@type']) for b in re.findall(r'<script type=\"application/ld\+json\">(.*?)</script>',t,re.S)]" dist/urun/<kimlik>/index.html`;
   - ürün site haritasında görselleriyle yer alıyor (`grep -c '/urun/<kimlik>/' dist/sitemap.xml`).

## 4. Kontroller: Ada, Nesli, Nazlı, SEO kontrolü (bu sırayla)

Ajanları **Agent** aracıyla çalıştır (`ada`, `nesli-urun`, `nazli`). Ajan türü listede yoksa `general-purpose` ajanını çalıştır ve ona önce `.claude/agents/<ad>.md` dosyasını okuyup oradaki role uymasını söyle. Ajanlar bu sohbeti görmez: görev metnine ürünün kimliğini, depodaki dosya yollarını ve ekran görüntülerinin tam yollarını yaz. Ajanlar commit ve push yapmaz.

**Hata bulunursa:** düzelt ve **o kontrolü yeniden çalıştır**. Düzeltme bir metni değiştirdiyse, sonraki kontroller değişmiş metne bakar. Nesli metin değiştirdiyse Nazlı zaten ondan sonra gelir.

1. **Ada (tasarım, görseller):** kapak, `vkart.webp`, sahneler, galerideki ilan görselleri, ürün sayfası ve kart ekran görüntüleri. Taşma, kayma, hizasızlık, çizgi kayması, kesilen yazı, ölçek ve tutarlılık. Kapak, aynı kategorideki diğer ürünlerin kapaklarıyla uyumlu mu? Ada dosya değiştirmez; bulgularını sen düzeltirsin.
2. **Nesli (SEO, `nesli-urun`, platform: kendi sitesi):** bu becerinin 1–3. bölümlerindeki listenin **tamamını madde madde** kontrol etsin ve her maddeye "tamam / sorun + somut düzeltme" yazsın:
   - görseller: Etsy ilan görselleri kullanılmış, kapak uyarlanmış (`vkart.webp`), dosya adları anlamlı, WebP, küçültülmüş, `width`/`height` var, ilk görsel dışındakiler lazy;
   - görsel alt metinleri: Türkçe, açıklayıcı, birbirinden farklı;
   - paylaşım görseli (og:image) bu ürünün;
   - başlık ve açıklamada aranan sözcükler;
   - `tanim` uzunluğu ve tıklatıcılığı;
   - **her yeni ürün için sayfa başlığı** (1. bölümün 6. maddesindeki kurallarla), uzunluğuna bakılmadan; Google arama önerilerine göre;
   - sınırlar: başlık **20–60 karakter**; açıklama **120–160 karakter**, yalnızca bu ürünün sayfasındaki bilgilerden ve başka hiçbir sayfanınkiyle aynı değil; aynı adlı ya da aynı türden ürünlerde her birinin başlığı farkını (renk, tema, sayfa sayısı, yaş) söylüyor. Bunlardan biri tutmuyorsa ya da açıklama başka bir ürününkine benziyorsa somut yeni metin (başlık için `seo.json` başlığı, açıklama için `tanim`) ve karakter sayısı;
   - adres (slug): kısa, Türkçe harfsiz, ürünü anlatıyor;
   - sayfa metni ürüne özgü (içerik, sayfa sayısı, boyut, kimin için, nasıl kullanılır) ve uydurma bilgi yok (üründen ve Etsy ilanından doğrulanıyor);
   - SSS: 3–5 soru, ürüne özgü;
   - yapısal veri: Product (ad, görsel, açıklama, fiyat TRY, stok, marka), BreadcrumbList, FAQPage doğru dolu;
   - kategori seçimi ve site haritası;
   - etiketler (sitedeki `etiketler` ve varsa Etsy ilanının 13 etiketi: siteye uyan aranan sözcükler başlıkta, açıklamada ya da etiketlerde var mı);
   - iç bağlantılar: 3–4 ilgili ürün, rehber bağlantısı.
   Önerilerini somut metin olarak versin. Sen uygula.
3. **Nazlı (dil):** `urunler.json`'daki `ad` ve `ozet`; `ozellik.json`'daki `tur`, `bakista` ve `hizli`; `site_metin.json`'daki `tanim`, `giris` ve SSS (ürüne özel SSS dâhil); `seo.json` başlığı; `teslim.json`'daki dosya adları; görsel alt metinleri; rehber yazısına eklenen bağlantı metni. Türkçe metinlerin dilini ve anlatımını kontrol etsin. Bu ürünün alanlarında yerinde düzeltsin, başka ürüne dokunmasın, değişiklikleri listelesin. Nazlı bir metnin uzunluğunu değiştirdiyse 4. adımdaki SEO kontrolü bunu yakalar.
4. **Başlığı yaz ve SEO kontrolü (derleme):** gizli üründe 3. bölümdeki gibi `yayinda` satırını geçici olarak kaldır (gizli ürünün sayfası derlenmez; iki araç da onu bulamaz).
   - Nesli'nin önerdiği ve Nazlı'nın baktığı başlığı `adres <TAB> başlık` satırı olarak bir dosyaya koy (örn. `/urun/<kimlik>/<TAB>Yeni başlık`). Sonra `python3 tools/seo_toplu.py <dosya>` çalıştır. Araç kuralları denetler, `catalog/seo.json`'a yazar, siteyi önce ve sonra derleyip yeni başlığın birebir tuttuğunu ve başka sayfanın değişmediğini kontrol eder. Aynı anda birden çok ürün ekleniyorsa hepsini tek dosyada ver. Araç hata verirse başlığı düzelt ya da Naz'a sor.
   - Ardından `python3 build.py --seo-kontrol /urun/<kimlik>/` çalıştır (birden fazla ürün eklendiyse hepsinin adresiyle). "SEO KONTROLÜ BAŞARISIZ" yazarsa **yayına alma**: düzelt, komutu yeniden çalıştır. Düzeltme metni değiştirdiyse değişen metni Nazlı'ya bir kez daha göster.
5. **Tur sınırı:** her kontrol için en çok iki düzeltme turu. Hâlâ yayını engelleyen bir bulgu varsa (yanlış bilgi, bozuk görsel, okunamayan yazı, geçmeyen SEO kontrolü) yayınlama ve Naz'a raporla.

## 5. Yayına al

1. `urunler.json`'da `"yayinda": false` satırını kaldır.
2. `python3 build.py --seo-kontrol /urun/<kimlik>/` çalıştır (birden fazla ürün eklendiyse hepsinin adresiyle). **"SEO KONTROLÜ BAŞARISIZ" yazarsa yayına alma:** hatayı düzelt (başlık için `tools/seo_toplu.py`, açıklama için `site_metin.json` → `tanim`), komutu yeniden çalıştır; düzeltemiyorsan Naz'a söyle. Geçince 3. bölümün kontrol listesine bir kez daha hızlıca bak. `python3 tools/seo_toplu.py --eksik` bu ürünü listelememeli.
3. **Kaydet ve gönder:**
   - Önce `git pull --rebase origin main`. Pano ve Etsy köprüsü de `main`'e yazar; onların kayıtlarını silme.
   - Yalnızca bu ürünün dosyalarını ve onun için değişen katalog satırlarını ekle.
   - Tek bir commit at, mesajı "Ürün eklendi: <ad>" olsun; sonra `main`'e push et. `main`'e gelen her kayıt Cloudflare'de kendiliğinden yayınlanır (yaklaşık 2 dakika).
4. Yaklaşık 3 dakika sonra `https://bastirkullan.com/urun/<kimlik>/` adresini kontrol et. **Canlı kontrol:**
   - sayfa açılıyor (HTTP 200): `curl -s -o /dev/null -w '%{http_code}\n' https://bastirkullan.com/urun/<kimlik>/`;
   - `<title>`, `meta description` ve `og:image` derlemedekiyle aynı: `curl -s https://bastirkullan.com/urun/<kimlik>/ | grep -oE '<title>[^<]*</title>|<meta (name="description"|property="og:image") content="[^"]*"'`;
   - galerideki görseller açılıyor (her biri için `curl -s -o /dev/null -w '%{http_code}'` 200 döner) ve alt metinleri kataloğa yazdıklarınla aynı (`curl -s … | grep -o 'alt="[^"]*"'`);
   - canlıda eski hâl görünüyorsa (önbellek) bunu not al, Naz'a önbellek temizliğini hatırlat (5. madde) ve temizlikten sonra yeniden bak.
   - Site şifre kapısının arkasındaysa sayfa şifre ister. Bunu raporda söyle, ürün yine de hazırdır.
   - Bu oturumun ağı siteye ulaşamıyorsa Naz'dan sayfayı açıp bakmasını iste: başlık, görseller ve fiyat doğru mu?
5. **Naz'a hatırlat:** Cloudflare önbelleğini temizlesin. Cloudflare panelinde bastirkullan.com → **Caching** → **Configuration** → **Purge Everything** (Önbellekteki her şeyi temizle) → onayla. Böylece yeni sayfa, kartlar ve görseller herkese hemen görünür.
6. `specialnstudio/PROJECT-STATUS.md`'ye tek satır ekle: tarih, ürün, kimlik.

## 6. Rapor (Türkçe, kısa)

- **Ne eklendi:** sayfa bağlantısı, fiyat, kategori; görsel sayısı, SSS soru sayısı, rehber bağlantısı (varsa).
- **Ekip kontrolleri:** Ada ne buldu ve ne düzeltildi, Nesli'nin madde madde sonucu ve hangi önerileri uygulandı, Nazlı neyi düzeltti; her kontrol geçti mi, kaç tur sürdü.
- **Test:** kontrol listesinin sonucu (geçti, başarısız, doğrulanamadı ve nedeni); `--seo-kontrol` çıktısındaki her ürünün başlığı ve açıklaması karakter sayısıyla.
- **Canlı kontrol:** sayfa açıldı mı; başlık, açıklama, görseller ve alt metinler doğru mu (ya da neden doğrulanamadı).
- **Naz'dan gerekenler:** her zaman Cloudflare önbellek temizliği (Caching → Purge Everything); başka bir şey varsa adım adım (hangi ekrana girecek, neye tıklayacak, ne görecek).
