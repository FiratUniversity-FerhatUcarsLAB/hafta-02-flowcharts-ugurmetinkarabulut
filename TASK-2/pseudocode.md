Öğrenci No:250541103
Öğrenci Ad-Soyad: Uğur Metin Karabulut

BASLA  // E-Ticaret Sistemi Başlangıcı

// 1. Kullanıcı Girişi
BASLA Kullanıcı_Girişi
    GİRİŞ bilgilerini al (e_posta, şifre)
    EGER veritabanında kullanıcı varsa VE şifre doğruysa ISE
        Oturumu başlat
        Kullanıcı sepetini yükle
    DEGILSE
        "Hatalı giriş!" mesajı göster
        GİRİŞ ekranına geri dön
    SON
BITIR Kullanıcı_Girişi


// 2. Ürün Ekleme
BASLA Ürün_Ekleme
    Kullanıcı ürün listesinden ürün seçer
    Seçilen ürünün ID ve adet bilgilerini al
    EGER ürün stokta varsa ISE
        Ürünü sepete ekle
    DEGILSE
        "Stokta yeterli ürün yok" mesajı göster
    SON
BITIR Ürün_Ekleme


// 3. Sepet Görüntüleme ve Güncelleme
BASLA Sepet_Yönetimi
    DÖNGÜ kullanıcı sepetini görüntülemek istedikçe
        Sepetteki ürünleri listele
        Kullanıcı isterse adet veya ürün çıkarabilir
        Her değişiklikte toplam tutarı güncelle
    SON
BITIR Sepet_Yönetimi


// 4. İndirim Kodu Kontrolü
BASLA Indirim_Kodu
    Kullanıcıdan indirim kodu al
    EGER kod boş değilse ISE
        EGER kod veritabanında geçerli VE süresi dolmamışsa ISE
            Toplam_tutar = Toplam_tutar - (İndirim oranı uygulanmış tutar)
            "İndirim uygulandı" mesajı göster
        DEGILSE
            "Geçersiz indirim kodu" mesajı göster
        SON
    SON
BITIR Indirim_Kodu


// 5. Kargo Hesaplama
BASLA Kargo_Hesaplama
    Kullanıcı adres bilgilerini girer
    Kargo_tutari = Mesafe * Ağırlık katsayısı
    EGER Toplam_tutar >= 1000 TL ISE
        Kargo_tutari = 0
        "Ücretsiz kargo uygulandı" mesajı göster
    SON
    Toplam_tutar = Toplam_tutar + Kargo_tutari
BITIR Kargo_Hesaplama


// 6. Ödeme Aşaması
BASLA Ödeme
    Kullanıcıdan ödeme yöntemi seçmesini iste (Kart, Kapıda, Havale)
    EGER yöntem = Kart ISE
        Kart bilgilerini al
        Ödeme sağlayıcısına istek gönder
        EGER ödeme başarılıysa ISE
            Sipariş_durumu = "Ödeme Alındı"
        DEGILSE
            "Ödeme başarısız" mesajı göster
            Ödeme ekranına geri dön
        SON
    DEGILSE EGER yöntem = Kapıda ISE
        Sipariş_durumu = "Kapıda Ödeme"
    DEGILSE EGER yöntem = Havale ISE
        Sipariş_durumu = "Havale Bekleniyor"
    SON
BITIR Ödeme


// 7. Sipariş Onayı
BASLA Sipariş_Onayı
    EGER Sipariş_durumu uygun ISE
        Stok miktarını güncelle
        Fatura oluştur
        Kargo firması bilgilendir
        Kullanıcıya onay mesajı gönder
        "Siparişiniz alındı" ekranını göster
    SON
BITIR Sipariş_Onayı


// 8. Sistem Sonu
BITIR  // E-Ticaret Sistemi Bitişi

