İsim - Soy isim Şevval Bulut
Öğrenci No:240541125

sistemin kısa açıklaması (maks. 5-6 satır)
BAŞLAT

// Kullanıcıdan kart girişi beklenir
Kartı_Tak()
Eğer Kart_OKUNAMAZSA ise
    Hata_Mesajı("Kart okunamadı. Lütfen tekrar deneyiniz.")
    DURDUR
Son

// Kullanıcıdan PIN girişi istenir
PIN = PIN_Gir()

Eğer PIN_DOĞRU_DEĞİLSE ise
    Hata_Mesajı("Hatalı PIN. Lütfen tekrar deneyiniz.")
    PIN_GİRİŞ_HAKKI -= 1
    Eğer PIN_GİRİŞ_HAKKI == 0 ise
        Hata_Mesajı("Kart bloke edildi.")
        Kartı_İade_Et()
        DURDUR
    Son
    Tekrar PIN_Gir()
Son

// Giriş başarılı, ana menü gösterilir
Ana_Menüyü_Göster()
Seçim = Menüden_Seçim_Al()

Eğer Seçim == "Para Çekme" ise
    ParaMiktarı = Para_Miktarı_Gir()

    // Kullanıcının bakiyesi kontrol edilir
    Eğer ParaMiktarı > Kullanıcı_Bakiyesi ise
        Hata_Mesajı("Yetersiz bakiye.")
        Ana_Menüyü_Göster()
    Son

    // ATM'de yeterli nakit olup olmadığı kontrol edilir
    Eğer ParaMiktarı > ATM_Bakiyesi ise
        Hata_Mesajı("ATM'de yeterli nakit yok.")
        Ana_Menüyü_Göster()
    Son

    // İşlem onaylanır ve para verilir
    Para_Cek(ParaMiktarı)
    Kullanıcı_Bakiyesi -= ParaMiktarı
    ATM_Bakiyesi -= ParaMiktarı

    Mesaj_Göster("Lütfen paranızı alınız.")
    Makbuz_İster_Misiniz = SoruSor("Makbuz ister misiniz? (E/H)")

    Eğer Makbuz_İster_Misiniz == "E" ise
        Makbuz_Yazdır()
    Son

    Kartı_İade_Et()
    Mesaj_Göster("İyi günler dileriz.")
    DURDUR

Son

Eğer Seçim == "Bakiye Sorgulama" ise
    Bakiye_Göster(Kullanıcı_Bakiyesi)
    Ana_Menüyü_Göster()
Son

Eğer Seçim == "Çıkış" ise
    Kartı_İade_Et()
    Mesaj_Göster("İyi günler dileriz.")
    DURDUR
Son

DURDUR
