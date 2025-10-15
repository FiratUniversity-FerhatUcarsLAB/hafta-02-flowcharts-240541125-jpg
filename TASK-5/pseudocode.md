BAŞLA AkilliEvGuvenlikSistemi

    // Veri yapıları
    TANIMLA KullaniciListesi ← sistem kullanıcıları (şifre, izinler vb.)
    TANIMLA GuvenlikDurumu ← "Kapalı" veya "Açık" (Alarm durumu)
    TANIMLA SensorDurumlari ← kapı, pencere, hareket sensörlerinin durumu (Açık/Kapalı, Hareket Algılandı/Algılanmadı)
    TANIMLA AlarmDurumu ← "Pasif" veya "Aktif"
    TANIMLA BildirimListesi ← kullanıcılara gönderilecek uyarılar

    // Fonksiyon: Kullanıcı girişi
    FONKSİYON GirisYap(kullaniciAdi, sifre)
        HER kullanıcı İÇİN KullaniciListesi
            EĞER kullanıcı.kullaniciAdi == kullaniciAdi VE kullanıcı.sifre == sifre
                DÖNDÜR kullanıcı
        SON
        YAZDIR "Hatalı kullanıcı adı veya şifre"
        DÖNDÜR NULL
    SON

    // Fonksiyon: Güvenlik sistemini aktif et
    FONKSİYON GuvenligiAktifEt()
        GuvenlikDurumu ← "Açık"
        AlarmDurumu ← "Pasif"
        YAZDIR "Güvenlik sistemi aktif edildi."
    SON

    // Fonksiyon: Güvenlik sistemini devre dışı bırak
    FONKSİYON GuvenligiPasifEt()
        GuvenlikDurumu ← "Kapalı"
        AlarmDurumu ← "Pasif"
        YAZDIR "Güvenlik sistemi devre dışı bırakıldı."
    SON

    // Fonksiyon: Sensör durumu kontrol et
    FONKSİYON SensorlariKontrolEt()
        EĞER GuvenlikDurumu == "Açık"
            HER sensor İÇİN SensorDurumlari
                EĞER sensor durumu "Açık" veya "Hareket Algılandı" İSE
                    AlarmDurumu ← "Aktif"
                    BildirimListesi'ne "Alarm! Sensör tetiklendi: " + sensor adı EKLE
                    YAZDIR "Alarm durumu: Aktif"
                SON
            SON
        SON
    SON

    // Fonksiyon: Alarmı kapat
    FONKSİYON AlarmKapat(kullanici)
        EĞER AlarmDurumu == "Aktif" VE kullanıcı yetkili İSE
            AlarmDurumu ← "Pasif"
            BildirimListesi'ne "Alarm kapatıldı." EKLE
            YAZDIR "Alarm kapatıldı."
        DEĞİLSE
            YAZDIR "Alarm kapatılamadı. Yetkiniz yok veya alarm aktif değil."
        SON
    SON

    // Fonksiyon: Bildirim gönder
    FONKSİYON BildirimGonder()
        HER bildirim İÇİN BildirimListesi
            YAZDIR "Bildirim Gönderildi: " + bildirim
        SON
        BildirimListesi TEMIZLE
    SON

    // Ana Menü
    FONKSİYON AnaMenu(kullanici)
        İKEN TRUE
            YAZDIR "\n--- Akıllı Ev Güvenlik Sistemi Menü ---"
            YAZDIR "1. Güvenlik Sistemini Aktif Et"
            YAZDIR "2. Güvenlik Sistemini Devre Dışı Bırak"
            YAZDIR "3. Sensör Durumlarını Kontrol Et"
            YAZDIR "4. Alarmı Kapat"
            YAZDIR "5. Çıkış"
            SECIM AL

            EĞER SECIM == 1
                GuvenligiAktifEt()
            EĞER SECIM == 2
                GuvenligiPasifEt()
            EĞER SECIM == 3
                SensorlariKontrolEt()
                BildirimGonder()
            EĞER SECIM == 4
                AlarmKapat(kullanici)
            EĞER SECIM == 5
                YAZDIR "Sistemden çıkılıyor..."
                ÇIK
        SON
    SON

    // Program başlangıcı
    YAZDIR "Akıllı Ev Güvenlik Sistemine Hoş Geldiniz"
    kullaniciAdi AL
    sifre AL
    kullanici ← GirisYap(kullaniciAdi, sifre)

    EĞER kullanici ≠ NULL
        AnaMenu(kullanici)
    DEĞİLSE
        YAZDIR "Giriş başarısız. Sistem kapatılıyor."

BİTİR AkilliEvGuvenlikSistemi
