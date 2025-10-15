Öğrenci No: 250541103
Öğrenci Ad-Soyad: Uğur Metin Karabulut

BASLA Akıllı Ev Güvenlik Sistemi

DÖNGÜ Sonsuz (Sistem Aktif ise)  // Sürekli döngü
    // 1. Sensörleri Oku
    HareketDurumu = HareketSensörüOku()
    KapiDurumu = KapiPencereSensörüOku()
    CamDurumu = CamSensörüOku()
    
    // 2. Tehdit Algılama
    TEHDİT_SEVIYE = 0
    EGER HareketDurumu ALGILANDI ISE
        TEHDİT_SEVIYE = MAX(TEHDİT_SEVIYE, 2) // Orta seviyeli tehdit
    BITIR EGER

    EGER KapiDurumu ALGILANDI ISE
        TEHDİT_SEVIYE = MAX(TEHDİT_SEVIYE, 3) // Yüksek seviyeli tehdit
    BITIR EGER

    EGER CamDurumu ALGILANDI ISE
        TEHDİT_SEVIYE = MAX(TEHDİT_SEVIYE, 3) // Yüksek seviyeli tehdit
    BITIR EGER

    // 3. Alarm ve Bildirim
    EGER TEHDİT_SEVIYE > 0 ISE
        EGER TEHDİT_SEVIYE == 1 ISE
            Alarm = Düşük
        DEĞİLSE EGER TEHDİT_SEVIYE == 2 ISE
            Alarm = Orta
        DEĞİLSE
            Alarm = Yüksek
        BITIR EGER
        BildirimGonder(SMS, App, Email, Alarm)
    DEĞİLSE
        Alarm = Pasif
    BITIR EGER

    // 4. Bekle ve tekrar döngü
    Bekle(BelirliSüre)
BITIR DÖNGÜ

BITIR Sistem