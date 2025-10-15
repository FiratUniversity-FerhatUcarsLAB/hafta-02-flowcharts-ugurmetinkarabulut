Öğrenci No: 250541103
Öğrenci Ad-Soyad: Uğur Metin Karabulut

BASLA DersKayitSistemi

    // 1. Giriş
    YAZ "Kullanıcı adı giriniz:"
    KULLANICI_ADI = AL
    YAZ "Şifre giriniz:"
    SIFRE = AL

    EGER (GirisDogruMu(KULLANICI_ADI, SIFRE)) ISE
        YAZ "Giriş başarılı. Ders kayıt ekranına yönlendiriliyorsunuz."
    ISE
        YAZ "Hatalı kullanıcı adı veya şifre!"
        BITIR
    BITIR_EGER

    // 2. Ders Listesi
    DERS_LISTESI = DersleriGetir(OgrenciID)
    YAZ "Alabileceğiniz dersler:"
    DÖNGÜ HER DERS in DERS_LISTESI
        YAZ DERS.Kodu, DERS.Adi, DERS.Kredi, DERS.Saat, DERS.Kontenjan
    BITIR_DÖNGÜ

    // 3. Ders Seçimi
    SEÇİLEN_DERSLER = BOS_LISTE
    DÖNGÜ
        YAZ "Seçmek istediğiniz ders kodunu giriniz (bitirmek için '0'):"
        DERS_KODU = AL
        EGER (DERS_KODU == 0) ISE
            BITIR_DÖNGÜ
        BITIR_EGER

        DERS = DERS_LISTESI[DERS_KODU]

        // 4. Kontroller

        // 4.1 Kontenjan Kontrolü
        EGER (DERS.Kontenjan <= 0) ISE
            YAZ "Bu dersin kontenjanı dolu!"
            DEVAM_ET DÖNGÜ
        BITIR_EGER

        // 4.2 Ön Koşul Kontrolü
        EGER (ON_KOSUL_TAMAMLANMAMIŞ(DERS, OgrenciID)) ISE
            YAZ "Bu dersi almak için ön koşul dersleri tamamlamanız gerekiyor."
            DEVAM_ET DÖNGÜ
        BITIR_EGER

        // 4.3 Zaman Çakışması Kontrolü
        EGER (ZAMAN_CAKISMA(SEÇİLEN_DERSLER, DERS)) ISE
            YAZ "Bu ders mevcut programınızla çakışıyor!"
            DEVAM_ET DÖNGÜ
        BITIR_EGER

        // 4.4 Kredi Limiti Kontrolü
        TOPLAM_KREDI = KrediHesapla(SEÇİLEN_DERSLER) + DERS.Kredi
        EGER (TOPLAM_KREDI > MAX_KREDI) ISE
            YAZ "Kredi limitinizi aşıyorsunuz!"
            DEVAM_ET DÖNGÜ
        BITIR_EGER

        // 4.5 Danışman Onayı Kontrolü
        EGER (DERS_ICIN_DANISMAN_ONAYI_GEREKLI(DERS)) ISE
            YAZ "Bu ders için danışman onayı gerekmektedir."
            ONAY = AL "Danışman onayı verildi mi? (E/H)"
            EGER (ONAY != "E") ISE
                YAZ "Ders kaydı için onay alınmadı!"
                DEVAM_ET DÖNGÜ
            BITIR_EGER
        BITIR_EGER

        // Ders seçim başarılı
        SEÇİLEN_DERSLER.EKLE(DERS)
        DERS.Kontenjan = DERS.Kontenjan - 1
        YAZ DERS.Adi, "dersi seçildi."

    BITIR_DÖNGÜ

    // 5. Onaylama ve Kaydetme
    EGER (SEÇİLEN_DERSLER.BOS_MU() == HAYIR) ISE
        YAZ "Seçtiğiniz dersler:"
        DÖNGÜ HER DERS in SEÇİLEN_DERSLER
            YAZ DERS.Kodu, DERS.Adi, DERS.Kredi, DERS.Saat
        BITIR_DÖNGÜ
        YAZ "Ders kaydınızı onaylıyor musunuz? (E/H)"
        ONAY = AL
        EGER (ONAY == "E") ISE
            DersKaydet(SEÇİLEN_DERSLER, OgrenciID)
            YAZ "Ders kaydınız başarıyla tamamlandı."
        ISE
            YAZ "Ders kaydınız onaylanmadı."
        BITIR_EGER
    ISE
        YAZ "Hiç ders seçmediniz."
    BITIR_EGER

BITIR DersKayitSistemi