BAŞLA AlışverişSepetiSistemi

    TANIMLA Sepet BOŞ LİSTE OLARAK
    TANIMLA ÜrünListesi mevcut ürünlerden oluşan LİSTE OLARAK

    FONKSİYON AnaMenüyüGöster()
        YAZDIR "1. Ürünleri Listele"
        YAZDIR "2. Sepete Ürün Ekle"
        YAZDIR "3. Sepetten Ürün Çıkar"
        YAZDIR "4. Sepeti Görüntüle"
        YAZDIR "5. Ödeme Yap"
        YAZDIR "6. Çıkış"

    FONKSİYON ÜrünleriListele()
        HER ürün İÇİN ürün ÜrünListesi'nde
            YAZDIR ürün.id, ürün.ad, ürün.fiyat

    FONKSİYON SepeteÜrünEkle(ürünId, adet)
        ürün ← ÜrünListesi'nde ürün.id == ürünId OLAN ürünü BUL
        EĞER ürün BOŞ DEĞİLSE
            sepetÜrünü ← Sepet'te item.product.id == ürünId OLAN ürünü BUL
            EĞER sepetÜrünü VARSA
                sepetÜrünü.adet ← sepetÜrünü.adet + adet
            DEĞİLSE
                { ürün: ürün, adet: adet } öğesini Sepet'e EKLE
            SON
            YAZDIR "Ürün sepete eklendi."
        DEĞİLSE
            YAZDIR "Ürün bulunamadı."
        SON

    FONKSİYON SepettenÜrünÇıkar(ürünId)
        sepetÜrünü ← Sepet'te item.product.id == ürünId OLAN ürünü BUL
        EĞER sepetÜrünü VARSA
            sepetÜrünü'nü Sepet'ten KALDIR
            YAZDIR "Ürün sepetten çıkarıldı."
        DEĞİLSE
            YAZDIR "Ürün sepetinizde bulunamadı."
        SON

    FONKSİYON SepetiGörüntüle()
        EĞER Sepet BOŞSA
            YAZDIR "Sepetiniz boş."
        DEĞİLSE
            toplam ← 0
            HER item İÇİN item Sepet'te
                araToplam ← item.adet * item.product.fiyat
                YAZDIR item.product.ad, item.adet, item.product.fiyat, araToplam
                toplam ← toplam + araToplam
            SON
            YAZDIR "Toplam Tutar:", toplam
        SON

    FONKSİYON ÖdemeYap()
        EĞER Sepet BOŞSA
            YAZDIR "Sepetiniz boş. Ödeme yapılamaz."
        DEĞİLSE
            SepetiGörüntüle()
            YAZDIR "Ödeme işlemi başlatılıyor..."
            // Buraya ödeme işlemleri entegre edilebilir
            YAZDIR "Ödeme başarılı!"
            Sepet'i TEMİZLE
        SON

    // Ana Döngü
    İKEN DOĞRU
        AnaMenüyüGöster()
        SEÇİMİ AL choice

        EĞER choice == 1 İSE
            ÜrünleriListele()
        DEĞİLSE EĞER choice == 2 İSE
            ürünId VE adet AL
            SepeteÜrünEkle(ürünId, adet)
        DEĞİLSE EĞER choice == 3 İSE
            ürünId AL
            SepettenÜrünÇıkar(ürünId)
        DEĞİLSE EĞER choice == 4 İSE
            SepetiGörüntüle()
        DEĞİLSE EĞER choice == 5 İSE
            ÖdemeYap()
        DEĞİLSE EĞER choice == 6 İSE
            YAZDIR "Çıkış yapılıyor..."
            ÇIK
        DEĞİLSE
            YAZDIR "Geçersiz seçim. Lütfen tekrar deneyin."
        SON
    SON

BİTİR AlışverişSepetiSistemi
