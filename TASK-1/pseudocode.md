Öğrenci Ad Soyad: Uğur Metin Karabulut
Öğrenci No: 250541103

BASLA

   bakiye ← 5000
   gunluk_limit ← 2000
   giris_hakki ← 3
   cekilen_toplam ← 0

   DÖNGÜ (giris_hakki > 0)
      YAZ "Lütfen PIN kodunuzu giriniz: "
      OKU pin

      EĞER pin = 1234 İSE
         YAZ "PIN doğru. Hoş geldiniz."
         ÇIK DÖNGÜ
      DEĞİLSE
         giris_hakki ← giris_hakki - 1
         YAZ "PIN hatalı. Kalan deneme hakkı: ", giris_hakki
         EĞER giris_hakki = 0 İSE
             YAZ "3 defa hatalı giriş yaptınız. Kart bloke edildi."(
             BİTİR
         SON
      SON
   SON DÖNGÜ


   DÖNGÜ (TRUE)
      YAZ "Mevcut bakiyeniz: ", bakiye, " TL"
      YAZ "Günlük limitinizden kalan: ", gunluk_limit - cekilen_toplam, " TL"
      YAZ "Çekmek istediğiniz tutarı giriniz: "
      OKU tutar

      EĞER tutar % 20 ≠ 0 İSE
          YAZ "Tutar 20 TL'nin katı olmalıdır."
      DEĞİLSE EĞER tutar > bakiye İSE
          YAZ "Yetersiz bakiye."
      DEĞİLSE EĞER (cekilen_toplam + tutar) > gunluk_limit İSE
          YAZ "Günlük para çekme limitinizi aştınız."
      DEĞİLSE
          bakiye ← bakiye - tutar
          cekilen_toplam ← cekilen_toplam + tutar
          YAZ tutar, " TL çekiliyor..."
          YAZ "İşlem tamamlandı. Yeni bakiyeniz: ", bakiye, " TL"
      SON

      YAZ "Başka bir işlem yapmak ister misiniz? (E/H)"
      OKU cevap

      EĞER cevap = "H" VEYA cevap = "h" İSE
          YAZ "Kartınızı almayı unutmayın. İyi günler."
          BİTİR
      SON
   SON DÖNGÜ

BİTİR