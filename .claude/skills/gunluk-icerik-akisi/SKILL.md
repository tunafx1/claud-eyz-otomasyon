---
name: gunluk-icerik-akisi
description: Eğitimde yapay zeka haberlerini toplar, her haber değeri yüksek gelişme için ayrı Instagram carousel post taslağı ve görsel promptları hazırlar.
---

# Günlük İçerik Akışı

1. marka-kimligi.md dosyasını oku, tüm çıktıları buna göre üret.

2. Son 2-3 gün içindeki eğitimde yapay zeka haberlerini web'den ara (hem yerli hem yabancı kaynak), marka-kimligi.md'deki haber seçim kriterine göre değerlendir.

2a. REDDİT TARAMASI: Apify'ın `clearpath/reddit-subreddit-posts-scraper` actor'ünü çağır (mcp__apify__call-actor veya call-actor-widget ile). Girdi:
   - `subreddits`: ["ChatGPT", "OpenAI", "artificial", "education", "singularity"]
   - `sort`: "top"
   - `timeFilter`: "week" (actor'de 2-3 günlük bir seçenek yok; "week" çekip sonucu created/timestamp alanına göre son 2-3 güne filtrele)
   - `maxPostsPerSubreddit`: 25
   Dönen sonuçlardan skoru (upvote) en yüksek olanları öne çıkar, marka-kimligi.md'deki haber değeri kriteriyle değerlendir.

2b. TWITTER/X TARAMASI: Apify'ın `apidojo/tweet-scraper` (Tweet Scraper V2) actor'ünü çağır. Girdi:
   - `twitterHandles`: ["OpenAI", "AnthropicAI", "GoogleDeepMind"]
   - `searchTerms`: ["#AIinEducation"]
   - `sort`: "Latest"
   - `maxItems`: 40
   Dönen tweet'leri tarihe göre son 2-3 günle sınırla, ardından beğeni/retweet sayısına göre en popüler olanları seç ve marka-kimligi.md'deki haber değeri kriteriyle değerlendir.

3. YAPI: Günde tek bir "haftalık özet" carousel yapılmaz. Onun yerine, o gün bulunan HER haber-değeri-yüksek gelişme için AYRI bir carousel post hazırlanır. Çıktı "POST 1", "POST 2", "POST 3" gibi birden fazla, birbirinden bağımsız carousel olabilir — haber sayısına ve haber değerine göre günde 0-4 arası post. Hepsi haber değeri taşımıyorsa daha az post olabilir; hiçbiri taşımıyorsa post üretilmez.

4. HER POST kendi içinde 3-5 slayttan oluşur ve TEK bir habere odaklanır:
   1. Kapak/Hook slaytı
   2. Ne oldu (somut, net — sadece "X çıktı" deme, X'in NE yaptığını/sağladığını yaz)
   3. Eğitimde/sınıfta somut anlamı (gerekirse 1-2 slayt daha, haber derinse) — bir öğretmen/öğrenci/veli için GERÇEKTE nasıl bir işe yarayacağını elle tutulur bir örnekle anlat (kim, ne yapıyor, nasıl bir sonuç alıyor). Genel "eğitimi dönüştürecek" gibi klişe cümleler YASAK.
   4. Kapanış/CTA slaytı — okuyucuyu senaryo üzerinden düşündüren bir soru.

4a. FORMAT İLHAMI: Carousel taslağını hazırlarken, instagram-etkilesim-taramasi skill'inin bulduğu yüksek etkileşimli post formatlarından ilham al (başlık/hook tarzı, slayt sayısı, görsel stili) — bu hesapları veya postlarını birebir kopyalama, sadece hangi format ve tarzın etkileşim aldığını gözlemleyip kendi marka kimliğine uyarlamak için referans al.

5. GÖRSEL PROMPT KURALI: Her slaytın görsel promptu SADECE dekoratif sahneyi değil, görselin ÜZERİNE YAZILACAK METNİN TAMAMINI da içerir — o slaytta ekranda görünecek başlık, varsa alt metin/body text, varsa CTA metni gibi HER YAZI, prompt içinde birebir (kısaltılmadan, parafraze edilmeden) tırnak içinde geçmeli. Prompt içinde net ifadeler olmalı: "bold white headline text rendered on image reading '[başlık]'" ve varsa "body text below reading '[açıklama]'" gibi — ki görsel üretme aracı bu metni görselin üzerine gerçekten çizsin. Slaytın metin alanında ne yazılacaksa (örn. CTA slaytındaki soru cümlesi de dahil) o metin de aynı şekilde prompt'a eklenir; hiçbir slayt metni prompt dışında bırakılmaz. Prompt, haberin soyut bir simgesini (yıldız, sohbet balonu, soru işareti vb.) çizmez; onun yerine 3. maddedeki somut kullanım senaryosunu görselleştirir — sahnede gerçekten kim var, ne yapıyor, elinde/ekranında ne var, bunu tarif et. Marka kimliğindeki renk paleti ve stil her promptta korunur.

6. Sonucu düzenli bir özet olarak sun ve onay bekle: kaç post üretildiği, her postun kaç slayt olduğu ve neden o haberlerin seçildiği net olsun.

7. Taslak hazır olunca atuna.edu@gmail.com adresine, hazırlanan tüm post taslaklarını (her post kendi başlığıyla ayrılmış; slayt metinleri, caption, hashtagler, görsel promptları) düzenli bir özet halinde e-posta olarak gönder.

8. Mail gönderirken düz metin yerine HTML formatlı gönder. Format şöyle olsun:
   - Her post ayrı, net şekilde ayrılmış bir bölüm olsun (POST 1, POST 2, ... başlıklarıyla)
   - Post içindeki her slayt ayrı bir kart/bölüm gibi görünsün (başlık, arka plan rengiyle diğerlerinden ayrılsın)
   - Slayt başlığı ve gövde metni normal yazı tipinde
   - Her slaytın görsel promptu, ayrı bir kod bloğu (monospace font, açık gri arka plan, kenarlık) içinde gösterilsin ki tek tıkla/triple-click ile kolayca seçilip kopyalanabilsin
   - Kaynak linkleri tıklanabilir link olarak eklensin
   - Her postun caption ve hashtagleri kendi bölümünde, ayrı ve belirgin olsun
   - ÖNEMLİ: Gmail gönderimi `<style>` bloklarını ve `class="..."` özniteliklerini siliyor. Bu yüzden tüm biçimlendirmeyi (arka plan rengi, font, kenarlık, padding vb.) her elemente doğrudan `style="..."` inline attribute olarak yaz — merkezi bir `<style>` bloğuna veya CSS class'a güvenme.
   - ÖNEMLİ: Inline `style` içinde de `background:` (shorthand) özelliği Gmail tarafından siliniyor; arka plan rengi için mutlaka `background-color:` kullan, `background:` kullanma.
