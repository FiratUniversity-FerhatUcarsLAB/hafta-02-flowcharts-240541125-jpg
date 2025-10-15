BAŞLA HastaneRandevuSistemi

    // Temel veri yapıları
    TANIMLA KullaniciListesi ← hasta hesaplarını içeren liste
    TANIMLA DoktorListesi ← doktor bilgilerini içeren liste
    TANIMLA RandevuListesi ← tüm randevuları içeren liste

    // Fonksiyon: Kullanıcı girişi
    FONKSİYON GirisYap(kullaniciAdi, sifre)
        HER kullanıcı İÇİN KullaniciListesi
            EĞER kullanıcı.kullaniciAdi == kullaniciAdi VE kullanıcı.sifre == sifre İSE
                DÖNDÜR kullanıcı
        SON
        YAZDIR "Hatalı kullanıcı adı veya şifre"
        DÖNDÜR NULL
    SON

    // Fonksiyon: Doktorları listele
    FONKSİYON DoktorlariListele()
        YAZDIR "--- Doktor Listesi ---"
        HER doktor İÇİN DoktorListesi
            YAZDIR "ID:", doktor.id, "Ad:", doktor.ad, "Branş:", doktor.brans
        SON
    SON

    // Fonksiyon: Doktorun uygun saatlerini göster
    FONKSİYON UygunSaatleriListele(doktorId, tarih)
        TANIMLA mevcutRandevular ← Belirtilen doktor ve tarihteki randevuları RandevuListesi'nden filtrele
        TANIMLA tumSaatler ← ["09:00", "10:00", ..., "17:00"]
        TANIMLA uygunSaatler ← tumSaatler - mevcutRandevular.saat
        YAZDIR "Uygun saatler:"
        HER saat İÇİN uygunSaatler
            YAZDIR saat
        SON
    SON

    // Fonksiyon: Randevu al
    FONKSİYON RandevuAl(kullanici, doktorId, tarih, saat)
        EĞER doktorId, tarih ve saat kombinasyonu RandevuListesi'nde ZATEN VARSA
            YAZDIR "Bu saat dolu. Lütfen başka bir saat seçin."
        DEĞİLSE
            YENİ_RANDEVU ← {
                hastaId: kullanici.id,
                doktorId: doktorId,
                tarih: tarih,
                saat: saat
            }
            RandevuListesi'ne YENİ_RANDEVU EKLE
            YAZDIR "Randevunuz oluşturuldu:", tarih, saat
        SON
    SON

    // Fonksiyon: Kullanıcının randevularını listele
    FONKSİYON RandevularimiGoster(kullanici)
        YAZDIR "--- Randevularınız ---"
        HER randevu İÇİN RandevuListesi
            EĞER randevu.hastaId == kullanici.id
                doktor ← doktorId'ye göre DoktorListesi'nden doktoru bul
                YAZDIR randevu.tarih, randevu.saat, "Doktor:", doktor.ad
        SON
    SON

    // Fonksiyon: Randevu iptal et
    FONKSİYON RandevuIptalEt(kullanici, randevuId)
        randevu ← randevuId'ye sahip randevuyu BUL
        EĞER randevu VARSA VE randevu.hastaId == kullanici.id İSE
            RandevuListesi'nden randevuyu SİL
            YAZDIR "Randevu iptal edildi."
        DEĞİLSE
            YAZDIR "Randevu bulunamadı veya size ait değil."
        SON
    SON

    // Ana Menü
    FONKSİYON AnaMenu(kullanici)
        İKEN TRUE
            YAZDIR "\n--- Ana Menü ---"
            YAZDIR "1. Doktorları Listele"
            YAZDIR "2. Randevu Al"
            YAZDIR "3. Randevularımı Görüntüle"
            YAZDIR "4. Randevu İptal Et"
            YAZDIR "5. Çıkış"
            SECIM AL

            EĞER SECIM == 1
                DoktorlariListele()

            EĞER SECIM == 2
                DoktorlariListele()
                doktorId AL
                tarih AL
                UygunSaatleriListele(doktorId, tarih)
                saat AL
                RandevuAl(kullanici, doktorId, tarih, saat)

            EĞER SECIM == 3
                RandevularimiGoster(kullanici)

            EĞER SECIM == 4
                RandevularimiGoster(kullanici)
                randevuId AL
                RandevuIptalEt(kullanici, randevuId)

            EĞER SECIM == 5
                YAZDIR "Çıkış yapılıyor..."
                ÇIK
        SON
    SON

    // Giriş ekranı
    YAZDIR "Hastane Randevu Sistemine Hoş Geldiniz"
    kullanıcıAdı AL
    sifre AL
    kullanıcı ← GirisYap(kullanıcıAdı, sifre)

    EĞER kullanıcı ≠ NULL
        AnaMenu(kullanıcı)
    DEĞİLSE
        YAZDIR "Sistem sonlandırılıyor."
    SON

BİTİR HastaneRandevuSistemi
