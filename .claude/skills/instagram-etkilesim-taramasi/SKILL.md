---
name: instagram-etkilesim-taramasi
description: Verilen Instagram hesap listesindeki son postları Apify Instagram Scraper ile çeker, en yüksek etkileşimli olanları bulur ve format/başlık tarzlarını özetler.
---

# Instagram Etkileşim Taraması

## Taranacak hesap listesi

Kullanıcı ayrıca bir liste vermediği sürece varsayılan olarak aşağıdaki hesaplar taranır:

- **@ai_foreducation** — "AI for Education": öğretmen ve okulların AI ile potansiyelini açığa çıkarmaya odaklı, doğrudan edtech temalı hesap.
- **@ai4teachers** — "AI for Teachers | Practical Classroom AI": pratik AI ipuçları, araçları ve öğretmen iş akışlarını paylaşıyor.
- **@aiforteachers** — "AI For Teachers": K-12 eğitimde AI'ın temel kullanımını anlatan hesap.
- **@teachyeducation** — "Teachy Education": eğitim teknolojisi ve öğretmenlere yönelik içerik üreten hesap.
- **@jasminetonia_abang** — AI eğitimci / dijital içerik üreticisi; marka içerik stratejisti kimliğiyle AI konularını eğitim odaklı carousel'lara dönüştürüyor.
- **@futurepedia_io** — AI araçları ve haberlerini tanıtan, ~89K takipçili büyük hesap; doğrudan eğitim odaklı değil ama öğretmenlerin/içerik üreticilerinin keşfettiği AI araç haberlerini takip ediyor, format ilhamı için güçlü.
- **@bernard.marr** — Fütürist/yazar Bernard Marr'ın hesabı; iş ve teknoloji dünyasında AI trendlerini sade carousel'larla anlatıyor, geniş kitleye hitap ediyor.
- **@turkiye.ai** — Türkiye Yapay Zeka İnisiyatifi: Türkiye AI ekosistemini bir araya getiren, danışmanlık/eğitim/üyelik odaklı Türkçe hesap.
- **@yapayzekaveteknolojiakademisi** — Yapay Zeka ve Teknoloji Akademisi: Türkçe AI ve teknoloji eğitimi içerikleri üreten hesap.

Bu liste zamanla değişebilir (hesaplar kapanabilir/formatını değiştirebilir); tarama öncesi kullanıcıya listeyi güncel tutmak isteyip istemediği sorulabilir, ama varsayılan akış için ek onay gerekmez.

1. Kullanıcı farklı bir hesap listesi vermediyse yukarıdaki varsayılan listeyi kullan; verdiyse onun listesini kullan (kullanıcı adı veya profil URL'si olarak).

2. Apify'ın `apify/instagram-post-scraper` actor'ünü çağır (mcp__apify__call-actor veya call-actor-widget ile). Girdi:
   - `username`: kullanıcının verdiği hesap listesi (dizi)
   - `resultsLimit`: hesap başına 12 (daha fazla/az istenirse ayarla)
   - `onlyPostsNewerThan`: kullanıcı bir zaman aralığı belirtmediyse "30 days"
   - `dataDetailLevel`: "detailedData" (beğeni/yorum/görüntülenme gibi etkileşim metriklerinin tam gelmesi için)

3. Dönen postları hesap bazında beğeni + yorum sayısına göre sırala (video/reel ise görüntülenme sayısını da dikkate al). Her hesap için en yüksek etkileşimli 3-5 postu belirle.

4. Öne çıkan postları analiz et ve özetle:
   - Ortak format kalıpları (carousel mi, tekli görsel mi, reel mi; kaç slayt/karede olduğu)
   - Başlık/caption tarzı (uzunluk, ton, soru mu-iddia mı, emoji kullanımı, CTA var mı)
   - Kapak görseli/hook deseni (metin mi, yüz mü, ürün görseli mi öne çıkıyor)
   - Hashtag ve paylaşım zamanlaması gözlemleri (varsa)

5. Sonucu hesap bazında ayrılmış, düzenli bir özet olarak sun: her hesap için en etkileşimli postların linki, etkileşim sayıları ve yukarıdaki desen analizi. Bu özeti gunluk-icerik-akisi skill'indeki carousel taslaklarına ilham kaynağı olarak kullanılabilecek şekilde net tut.
