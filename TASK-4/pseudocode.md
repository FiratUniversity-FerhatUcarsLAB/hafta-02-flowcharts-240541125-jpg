BAŞLA UniversiteDersKayitSistemi

    // VERİ YAPILARI
    TANIMLA OgrenciListesi ← öğrenci bilgilerini içeren liste
    TANIMLA DersListesi ← tüm dersleri içeren liste
    TANIMLA Kayitlar ← öğrenci-ders eşleşmelerini içeren liste (kayıtlar)

    // FONKSİYON: Giriş yapma
    FONKSİYON GirisYap(ogrenciNumarasi, sifre)
        HER ogrenci İÇİN OgrenciListesi
            EĞER ogrenci.numara == ogrenciNumarasi VE ogrenci.sifre == sifre
                DÖNDÜR ogrenci
        SON
        YAZDIR "Hatalı numara veya şifre"
        DÖNDÜR NULL
    SON

    // FONKSİYON: Tüm dersleri listele
    FONKSİYON DersleriListele()
        YAZDIR "--- Açılan Dersler ---"
        HER ders İÇİN DersListesi
            YAZDIR "Kod:", ders.kod, "Ad:", ders.ad, "Kredi:", ders.kredi, "Kontenjan:", ders.kontenjan
        SON
    SON

    // FONKSİYON: Dersin uygunluğu kontrol et
    FONKSİYON DersUygunMu(ders, ogrenci)
        EĞER ders.kontenjan <= 0
            DÖNDÜR FALSE
        HER kayit İÇİN Kayitlar
            EĞER kayit.ogrenciId == ogrenci.id VE kayit.dersId == ders.id
                DÖNDÜR FALSE  // Zaten kayıtlı
        SON
        DÖNDÜR TRUE
    SON

    // FONKSİYON: Ders kaydı yap
    FONKSİYON DerseKaydol(ogrenci, dersKod)
        ders ← DersListesi'nde ders.kod == dersKod olanı BUL
        EĞER ders YOKSA
            YAZDIR "Ders bulunamadı."
            DÖNDÜR
        SON

        EĞER DersUygunMu(ders, ogrenci) == FALSE
            YAZDIR "Derse kayıt mümkün değil (kontenjan dolu veya zaten kayıtlı)."
            DÖNDÜR
        SON

        YENİ_KAYIT ← { ogrenciId: ogrenci.id, dersId: ders.id }
        Kayitlar' a EKLE YENİ_KAYIT
        ders.kontenjan ← ders.kontenjan - 1
        YAZDIR "Ders kaydı başarıyla yapıldı:", ders.ad
    SON

    // FONKSİYON: Öğrencinin kayıtlı derslerini listele
    FONKSİYON KayitliDersleriListele(ogrenci)
        YAZDIR "--- Kayıtlı Dersler ---"
        HER kayit İÇİN Kayitlar
            EĞER kayit.ogrenciId == ogrenci.id
                ders ← dersId'ye göre DersListesi'nden BUL
                YAZDIR ders.kod, ders.ad, ders.kredi
        SON
    SON

    // FONKSİYON: Ders kaydı sil
    FONKSİYON DersiSil(ogrenci, dersKod)
        ders ← DersListesi'nde ders.kod == dersKod olanı BUL
        EĞER ders YOKSA
            YAZDIR "Ders bulunamadı."
            DÖNDÜR
        SON

        kayit ← Kayitlar'da ogrenci.id ve ders.id eşleşen kayıt BUL
        EĞER kayit VARSA
            Kayitlar'dan KAYDI SİL
            ders.kontenjan ← ders.kontenjan + 1
            YAZDIR "Ders kaydı silindi:", ders.ad
        DEĞİLSE
            YAZDIR "Bu derse kayıtlı değilsiniz."
    SON

    // FONKSİYON: Ana Menü
    FONKSİYON AnaMenu(ogrenci)
        İKEN TRUE
            YAZDIR "\n--- Ders Kayıt Menüsü ---"
            YAZDIR "1. Dersleri Listele"
            YAZDIR "2. Derse Kayıt Ol"
            YAZDIR "3. Kayıtlı Dersleri Gör"
            YAZDIR "4. Ders Kaydını Sil"
            YAZDIR "5. Çıkış"
            SECIM AL

            EĞER SECIM == 1
                DersleriListele()
            EĞER SECIM == 2
                DersleriListele()
                dersKod AL
                DerseKaydol(ogrenci, dersKod)
            EĞER SECIM == 3
                KayitliDersleriListele(ogrenci)
            EĞER SECIM == 4
                KayitliDersleriListele(ogrenci)
                dersKod AL
                DersiSil(ogrenci, dersKod)
            EĞER SECIM == 5
                YAZDIR "Çıkış yapılıyor..."
                ÇIK
        SON
    SON

    // Giriş ve başlangıç
    YAZDIR "Üniversite Ders Kayıt Sistemine Hoş Geldiniz"
    ogrenciNumara AL
    sifre AL
    ogrenci ← GirisYap(ogrenciNumara, sifre)

    EĞER ogrenci ≠ NULL
        AnaMenu(ogrenci)
    DEĞİLSE
        YAZDIR "Sistemden çıkılıyor."

BİTİR UniversiteDersKayitSistemi

