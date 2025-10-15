PROGRAM ATM_Para_Cekme

BAŞLA

    // 1. Gerekli değişkenleri tanımla
    DEĞİŞKEN kullanıcı_adı, şifre, girilen_ad, girilen_şifre
    DEĞİŞKEN bakiye ← 5000 // Varsayılan kullanıcı bakiyesi
    DEĞİŞKEN cekilecek_tutar

    // 2. Kullanıcı bilgileri
    kullanıcı_adı ← "kullanici1"
    şifre ← "1234"

    // 3. Kullanıcı girişi
    EKRANA_YAZ "Kullanıcı adınızı girin: "
    girilen_ad ← KULLANICIDAN_VERİ_AL

    EKRANA_YAZ "Şifrenizi girin: "
    girilen_şifre ← KULLANICIDAN_VERİ_AL

    // 4. Kimlik doğrulama
    EĞER girilen_ad = kullanıcı_adı VE girilen_şifre = şifre İSE

        // 5. Para çekme işlemi
        EKRANA_YAZ "Giriş başarılı."
        EKRANA_YAZ "Çekmek istediğiniz tutarı girin: "
        cekilecek_tutar ← KULLANICIDAN_VERİ_AL

        // 6. Bakiye kontrolü
        EĞER cekilecek_tutar > 0 VE cekilecek_tutar ≤ bakiye İSE
            bakiye ← bakiye - cekilecek_tutar
            EKRANA_YAZ cekilecek_tutar & " TL başarıyla çekildi."
            EKRANA_YAZ "Kalan bakiyeniz: " & bakiye & " TL"
        DEĞİLSE
            EKRANA_YAZ "Yetersiz bakiye veya geçersiz tutar!"
        SON

    DEĞİLSE
        EKRANA_YAZ "Giriş başarısız. Kullanıcı adı veya şifre yanlış!"
    SON

BİTİR
