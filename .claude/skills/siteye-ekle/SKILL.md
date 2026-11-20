---
name: siteye-ekle
description: Etsy'deki (ya da Etsy'ye eklenmek üzere hazırlanan) Türkçe bir ürünü bastirkullan.com'a uygun hâle getirir ve sitede yayına alır. Vitrin görselini vitrin görsel aracıyla üretir; Nazlı (dil), Ada (tasarım) ve Nesli (SEO) kontrolünden geçirir, hatasız olunca yayınlar. Naz "/siteye-ekle" yazdığında, "bu ürünü siteye ekle", "sitede yayına al" dediğinde kullan.
argument-hint: "[Etsy ilan numarası, ürün klasörü ya da boş: oturumun ürünü]"
---

# /siteye-ekle: ürünü Bastır Kullan sitesine ekle ve yayına al

Naz bu skill'i çalıştırdığında **bu ürünün sitede yayına alınmasını onaylamış olur**. Yayın, aşağıdaki bütün kontroller geçtiyse yapılır. Bir kontrol kalırsa ya da bir bilgi eksikse yayınlama, Naz'a neyin eksik olduğunu söyle.

Naz ile Türkçe konuş. Her adımda kısa bilgi ver, sonunda tek bir rapor yaz. Token ve GitHub kullanımını az tut: dosyaları bir kez oku, ekran görüntüsünü yalnızca kontrol adımlarında al, sitenin deposuna tek kayıt ve tek push yap.

## 0. Hazırlık

1. **Site deposu:** `specialnstudio` (bastirkullan.com). Oturuma bağlı değilse `add_repo` ile ekle (`specialnstudio-cmyk/specialnstudio`, push yetkisiyle), `main` dalını çek. Bağlanamıyorsa dur ve Naz'a söyle.
2. Şunları oku, başka dosya okuma:
   - `specialnstudio/PROJECT-STATUS.md`
   - `specialnstudio/README.md`: "Ürün eklemek", "Mağaza kapakları", "Arama motorları (SEO)", "Yönetim panosu" ve "Sepet, ödeme ve teslim" bölümleri.
3. **Ürünün kaynağı (sırayla bak):**
   - Argümanda Etsy ilan numarası, klasör ya da dosya varsa o.
   - Yoksa oturumda üzerinde çalışılan ürün: ilan metni (`specialnstudio1/listings/` ya da oturumun ürün klasörü), satılan PDF/ZIP dosyaları, ilan görselleri.
   - `specialnstudio/catalog/etsy.json` ve `catalog/urunler.json`'da aynı Etsy numarasıyla gizli bir taslak varsa (Etsy köprüsü ekler), yeni ürün açma: o taslağı tamamla.
4. **Sürüm kontrolü:** `main`'de `catalog/site_metin.json` ve `tools/kesit_uret.py` yoksa yeni site tasarımı henüz yayına alınmamış demektir. Dur ve Naz'a söyle: önce yeni tasarım (`claude/quirky-gates-2o26rd` dalı) `main`'e alınmalı.
5. **Dil kuralı:** sitede yalnızca Türkçe ürünler satılır, iki dilli ürün olmaz. Ürün Türkçe değilse dur ve Naz'a söyle.

## 1. Ürünü kataloğa ekle (`specialnstudio` deposu)

Mevcut ürünlerin biçimini örnek al, alanları aynı adlarla yaz. `tools/etsyden_al.py` ÇALIŞTIRILMAZ (kataloğu baştan yazar, pano değişikliklerini siler).

1. **Kimlik:** kısa, Türkçe harfsiz, tireli (örn. `kina-gecesi-seti`). Taslak varsa onun kimliğini kullan.
2. **`catalog/urunler.json`:**
   - `ad`: Etsy başlığının kısa, okunur hâli; anahtar sözcük yığını olmaz.
   - `ozet`: tek satır, sonu noktasız.
   - `kategori`: var olan kategorilerden uygunu.
   - `fiyat`: Etsy fiyatı × 1,20 (KDV dâhil), 2 ondalığa yuvarla. Fiyat belli değilse Naz'a sor.
   - `aciklama`: Etsy metni.
   - `etiketler`, `gorseller` (ilan görselleri; `NN.jpg` 1400, `NN_k.jpg` 560, `NN_m.webp` 160, `catalog/img/<kimlik>/` içinde), `etsy` (ilan numarası).
   - `yayinda`: yayına alma adımına kadar `false` kalır.
3. **Satılan dosyalar:** `dosyalar/<kimlik>/` içine koy (tek dosya en çok 25 MB; büyükse böl ya da Naz'a söyle). `catalog/teslim.json`'a her dosya için `dosya`, `ad` (alıcının göreceği ad) ve `mb` yaz. Satılan dosya yoksa ürün yayına alınamaz: dur ve Naz'a hangi dosyanın gerektiğini söyle.
4. **`catalog/ozellik.json`:** `tur`, `ton`, `yazdir` (yalnızca yazdırılabilirde), `bakista` (5–8 satır, gerçek bilgiler) ve `hizli`: `icerik`, `format`, `uyum`, `teslim`. Boş bırakılanlar türetilir; yanlış olacaksa yaz.
5. **`catalog/site_metin.json`:** `urunler.<kimlik>`:
   - `tanim`: arama sonucu açıklaması, en çok 155 karakter; ürünün ne olduğu, kime göre olduğu, biçimi.
   - `giris`: 2 paragraf, Etsy metninden FARKLI, "sen" hitabıyla.
   - Kategorinin `sss` listesi yoksa 2–4 soru-cevap ekle.
6. **Etsy'ye özgü görseller:** üzerinde "Etsy" yazan ilan görselleri (Etsy'deki indirme adımları) sitede gösterilmez. `build.py` → `ETSY_YAZILI` listesine ekle.
7. **Rehber bağlantısı:** `pages/rehber/` içinde konusu bu ürüne uyan bir yazı varsa ürünü o yazının `urunler:` satırına ekle.

## 2. Vitrin görselleri

Mağaza kapağı ve galeri sahneleri **vitrin görsel aracıyla** üretilir. Bu araç Naz'ın ayrı bir oturumda hazırladığı araçtır.

1. **Aracı bul:**
   - `.claude/skills/` içinde adı "vitrin" geçen skill.
   - Yoksa `specialnstudio/tools/` içinde vitrin aracı ve `specialnstudio/README.md`'deki "Mağaza kapakları" bölümü.
2. **Aracı çalıştır:** aracın kendi talimatlarına göre bu ürünün kapağını (`kapak.jpg`, `kapak_o.webp`, `kapak_k.webp`, `kapak_m.webp`), sahnelerini ve `catalog/vitrin.json` kaydını üret.
3. **Kesit:** ürün ana sayfada kategori kutusunda ya da kampanyada kullanılacaksa `python3 tools/kesit_uret.py <kimlik>` ile zeminsiz kesiti de üret.
4. **Araç bulunamazsa ya da çalışmazsa:** dur ve Naz'a söyle. Vitrin görseli olmadan yayına alma.

## 3. Derle ve kendin kontrol et

1. `python3 build.py`: hata olmamalı.
2. `python3 -m http.server -d dist` ile aç. Şu ekran görüntülerini al (yalnızca sen bakacaksan deviceScaleFactor 1):
   - ürün sayfası (1440 ve 390 piksel);
   - ürünün kategori sayfasındaki kartı;
   - kapak görseli.
3. **Kontrol listesi:**
   - fiyat Etsy × 1,20;
   - "Hemen al" düğmesi görünüyor (`teslim.json` dolu);
   - dört satırlık özet doğru;
   - galeride Etsy yazılı görsel yok;
   - bütün görsellerde alt metin var;
   - başlık (`<title>`) 65 karakteri geçmiyor;
   - açıklama 155 karakteri geçmiyor;
   - sayfada tek H1 var;
   - JSON-LD geçerli (Product, Offer, FAQPage);
   - ürün site haritasında görselleriyle yer alıyor.

## 4. Ekip kontrolü: Nazlı, Ada, Nesli

Ajanları **Agent** aracıyla çalıştır (`nazli`, `ada`, `nesli-urun`). Ajan türü listede yoksa `general-purpose` ajanını çalıştır ve ona önce `.claude/agents/<ad>.md` dosyasını okuyup oradaki role uymasını söyle. Ajanlar bu sohbeti görmez: görev metnine ürünün kimliğini, depodaki dosya yollarını ve ekran görüntülerinin tam yollarını yaz. Ajanlar commit ve push yapmaz.

1. **Nazlı (dil):** `urunler.json`'daki `ad` ve `ozet`; `ozellik.json`'daki `tur`, `bakista` ve `hizli`; `site_metin.json`'daki `tanim`, `giris` ve SSS; `teslim.json`'daki dosya adları; görsel alt metinleri. Bu ürünün alanlarında yerinde düzeltsin, başka ürüne dokunmasın, değişiklikleri listelesin.
2. **Ada (tasarım):** kapak, sahneler, ürün sayfası ve kart ekran görüntüleri. Çizgi kayması, taşma, kesilen yazı, ölçek ve tutarlılık. Diğer ürünlerin kapaklarıyla aynı vitrin stilinde mi? Ada dosya değiştirmez; bulgularını sen düzeltirsin (gerekirse vitrin aracını yeniden çalıştırırsın).
3. **Nesli (SEO, `nesli-urun`, platform: kendi sitesi):**
   - başlık ve açıklamada aranan sözcükler;
   - `tanim` uzunluğu ve tıklatıcılığı;
   - etiketler;
   - görsel alt metinleri;
   - kategori seçimi;
   - rehber bağlantısı.
   Önerilerini somut metin olarak versin. Sen uygula.
4. Nesli metin değiştirdiyse değişen metinleri **Nazlı'ya bir kez daha** göster.
5. **Tur sınırı:** en çok iki düzeltme turu. Hâlâ yayını engelleyen bir bulgu varsa (yanlış bilgi, bozuk görsel, okunamayan yazı) yayınlama ve Naz'a raporla.

## 5. Yayına al

1. `urunler.json`'da `"yayinda": false` satırını kaldır.
2. `python3 build.py` çalıştır ve 3. adımın kontrol listesine bir kez daha hızlıca bak.
3. **Kaydet ve gönder:**
   - Önce `git pull --rebase origin main`. Pano ve Etsy köprüsü de `main`'e yazar; onların kayıtlarını silme.
   - Yalnızca bu ürünün dosyalarını ve onun için değişen katalog satırlarını ekle.
   - Tek bir commit at, mesajı "Ürün eklendi: <ad>" olsun; sonra `main`'e push et. `main`'e gelen her kayıt Cloudflare'de kendiliğinden yayınlanır (yaklaşık 2 dakika).
4. Yaklaşık 3 dakika sonra `https://bastirkullan.com/urun/<kimlik>/` adresini kontrol et.
   - Site şifre kapısının arkasındaysa sayfa şifre ister. Bunu raporda söyle, ürün yine de hazırdır.
   - Bu oturumun ağı siteye ulaşamıyorsa Naz'dan sayfayı açıp bakmasını iste.
5. `specialnstudio/PROJECT-STATUS.md`'ye tek satır ekle: tarih, ürün, kimlik.

## 6. Rapor (Türkçe, kısa)

- **Ürün:** sayfa bağlantısı, fiyat, kategori.
- **Ekip kontrolleri:** Nazlı neyi düzeltti, Ada ne buldu ve ne düzeltildi, Nesli'nin hangi önerileri uygulandı.
- **Test:** kontrol listesinin sonucu (geçti, başarısız, doğrulanamadı ve nedeni).
- **Naz'dan gerekenler:** varsa, adım adım (hangi ekrana girecek, neye tıklayacak, ne görecek).
