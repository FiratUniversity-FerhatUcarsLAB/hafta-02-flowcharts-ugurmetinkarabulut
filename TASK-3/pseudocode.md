Öğrenci No: 250541103
Öğrenci Ad-Soyad: Uğur Metin Karabulut

BASLA Hastane Sistemi Ana Menü

    BASLA Kimlik Doğrulama
        KULLANICIDAN kimlik_numarası al
        EGER-ISE kimlik_numarası doğrulanıyorsa
            EKRANA "Giriş Başarılı" yaz
        Aksi halde
            EKRANA "Kimlik Hatalı, tekrar deneyin" yaz
            TEKRAR Kimlik Doğrulama
    BITIR Kimlik Doğrulama

    BASLA Ana Menü
        EKRANA "1. Randevu Sistemi" yaz
        EKRANA "2. Tahlil Sonucu Görüntüleme" yaz
        KULLANICIDAN seçim al

        EGER-ISE seçim = 1 ise
            BASLA Hastane Randevu Sistemi
                // Daha önce yazdığımız Randevu Sistemi pseudocode'u buraya gelir
            BITIR Hastane Randevu Sistemi

        EGER-ISE seçim = 2 ise
            BASLA Tahlil Sonucu Görüntüleme Sistemi
                // Daha önce yazdığımız Tahlil Sistemi pseudocode'u buraya gelir
            BITIR Tahlil Sonucu Görüntüleme Sistemi

        Aksi halde
            EKRANA "Geçersiz seçim, lütfen tekrar deneyin" yaz
            TEKRAR Ana Menü
    BITIR Ana Menü

BITIR Hastane Sistemi Ana Menü





BASLA Hastane Randevu Sistemi

    BASLA Kimlik Doğrulama
        KULLANICIDAN kimlik_numarası al
        EGER-ISE kimlik_numarası doğrulanıyorsa
            EKRANA "Giriş Başarılı" yaz
        Aksi halde
            EKRANA "Kimlik Hatalı, tekrar deneyin" yaz
            TEKRAR Kimlik Doğrulama
    BITIR Kimlik Doğrulama

    BASLA Poliklinik Seçimi
        EKRANA Poliklinik listesini göster
        KULLANICIDAN poliklinik seçimi al
    BITIR Poliklinik Seçimi

    BASLA Doktor Listesi Görüntüleme
        Seçilen polikliniğe ait doktor listesini göster
        KULLANICIDAN doktor seçimi al
    BITIR Doktor Listesi Görüntüleme

    BASLA Uygun Saatleri Gösterme
        Seçilen doktora ait uygun randevu saatlerini getir
        EKRANA uygun saatleri göster
        KULLANICIDAN saat seçimi al
    BITIR Uygun Saatleri Gösterme

    BASLA Randevu Onaylama
        EKRANA seçilen poliklinik, doktor ve saat bilgilerini göster
        KULLANICIDAN onay al
        EGER-ISE onaylandıysa
            Randevuyu kaydet
            BASLA SMS Gönderme
                Seçilen saat ve doktor bilgisi ile SMS oluştur
                SMS gönder
            BITIR SMS Gönderme
            EKRANA "Randevu Başarıyla Alındı" yaz
        Aksi halde
            EKRANA "Randevu İptal Edildi" yaz
    BITIR Randevu Onaylama

BITIR Hastane Randevu Sistemi





BASLA Tahlil Sonucu Görüntüleme Sistemi

    BASLA Kimlik Doğrulama
        KULLANICIDAN kimlik_numarası al
        EGER-ISE kimlik_numarası doğrulanıyorsa
            EKRANA "Giriş Başarılı" yaz
        Aksi halde
            EKRANA "Kimlik Hatalı, tekrar deneyin" yaz
            TEKRAR Kimlik Doğrulama
    BITIR Kimlik Doğrulama

    BASLA Tahlil Varlığı Kontrolü
        KULLANICIDAN tahlil_id al
        EGER-ISE tahlil mevcutsa
            EKRANA "Tahlil bulundu" yaz
        Aksi halde
            EKRANA "Tahlil bulunamadı" yaz
            BITIR Sistem
    BITIR Tahlil Varlığı Kontrolü

    BASLA Sonuç Hazır mı Kontrolü
        EGER-ISE tahlil sonucu hazırsa
            BASLA Görüntüleme
                EKRANA tahlil sonucunu göster
            BITIR Görüntüleme

            BASLA PDF İndirme
                KULLANICIDAN PDF indirilsin mi onayı al
                EGER-ISE onaylandıysa
                    PDF oluştur ve indir
                    EKRANA "PDF Başarıyla İndirildi" yaz
            BITIR PDF İndirme
        Aksi halde
            EKRANA "Tahlil sonucu henüz hazır değil. Lütfen daha sonra tekrar deneyin." yaz
    BITIR Sonuç Hazır mı Kontrolü

BITIR Tahlil Sonucu Görüntüleme Sistemi

