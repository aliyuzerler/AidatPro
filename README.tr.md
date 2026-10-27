# AidatPro

**Apartmanlar, siteler ve toplu yaşam alanları için ücretsiz ve açık kaynaklı aidat yönetim paneli.**

AidatPro; site yöneticilerinin daireleri, sakinleri, aidat tahakkuklarını, ödemeleri, giderleri, duyuruları, raporları ve banka hareketlerini tek panelden yönetmesini sağlar. Laravel, Vite ve Tabler UI altyapısı üzerine kuruludur ve MIT lisansı ile yayımlanmıştır.

Dil seçenekleri: [Türkçe (bu dosya)](README.md) | [English](README.en.md)

Canlı demo: [https://aidat.halilcan.dev](https://aidat.halilcan.dev)

---

## İçindekiler

- [Ekran Görüntüleri](#ekran-görüntüleri)
- [Özellikler](#özellikler)
- [Teknoloji Yığını](#teknoloji-yığını)
- [Kurulum](#kurulum)
- [Demo Hesabı](#demo-hesabı)
- [VakıfBank Entegrasyonu](#vakıfbank-entegrasyonu)
- [Zamanlayıcı](#zamanlayıcı)
- [Güvenlik](#güvenlik)
- [Bilinen Sınırlamalar](#bilinen-sınırlamalar)
- [Test](#test)
- [Katkı](#katkı)
- [Lisans](#lisans)

---

## Ekran Görüntüleri

Tüm ekran görüntüleri `docs/screenshots/` klasöründe bulunur.

### Giriş

[![Giriş ekranı](docs/screenshots/01-login.png)](docs/screenshots/01-login.png)

E-posta ve şifre ile klasik giriş ekranı. 5 hatalı denemeden sonra hesap 15 dakika kilitlenir.

### Dashboard

[![Dashboard](docs/screenshots/02-dashboard.png)](docs/screenshots/02-dashboard.png)

Site seçildikten sonra gelir, gider, tahsilat, bekleyen borç ve genel durum özetleri tek ekranda.

### Site Yönetimi

[![Siteler](docs/screenshots/03-sites.png)](docs/screenshots/03-sites.png)
[![Yeni site](docs/screenshots/04-site-create.png)](docs/screenshots/04-site-create.png)

Birden fazla site tanımlanabilir; her sitenin adı ve adresi tutulur.

### Daire Yönetimi

[![Daireler](docs/screenshots/05-apartments.png)](docs/screenshots/05-apartments.png)
[![Yeni daire](docs/screenshots/06-apartment-create.png)](docs/screenshots/06-apartment-create.png)

Site → Blok → Daire hiyerarşisi. Her dairenin blok, numara, kat ve doluluk durumu (dolu/boş) takip edilir.

### Sakin Yönetimi

[![Sakinler](docs/screenshots/07-residents.png)](docs/screenshots/07-residents.png)

Daire bazlı sakin kayıtları: ad soyad, telefon, e-posta, sakin tipi (mal sahibi / kiracı) ve aktiflik durumu.

### Aidat Tahakkuku

[![Aidatlar](docs/screenshots/09-dues.png)](docs/screenshots/09-dues.png)
[![Yeni aidat](docs/screenshots/10-due-create.png)](docs/screenshots/10-due-create.png)

Dönem (yıl + ay), tutar, son ödeme tarihi ve not ile aidat tanımlama. Aynı daireye aynı dönem için mükerrer tahakkuk engellenir.

### Ödemeler ve Makbuzlar

[![Ödemeler](docs/screenshots/11-payments.png)](docs/screenshots/11-payments.png)
[![Ödeme alma](docs/screenshots/12-payment-create.png)](docs/screenshots/12-payment-create.png)
[![Makbuz](docs/screenshots/13-receipt.png)](docs/screenshots/13-receipt.png)

Banka / EFT / kart / nakit yöntemleriyle ödeme kaydı. Kısmi ödeme desteklenir; girilen tutar kalan borcu aşamaz. Her ödeme için ekranda görüntülenebilen, PDF olarak indirilebilen ve WhatsApp mesajı olarak gönderilebilen numaralı makbuz üretilir.

### Giderler

[![Giderler](docs/screenshots/14-expenses.png)](docs/screenshots/14-expenses.png)
[![Yeni gider](docs/screenshots/15-expense-create.png)](docs/screenshots/15-expense-create.png)

Site bazlı gider kayıtları: kategori, açıklama, tutar ve tarih.

### Duyurular

[![Duyurular](docs/screenshots/16-announcements.png)](docs/screenshots/16-announcements.png)
[![Duyuru gönderimi](docs/screenshots/17-announcement-send.png)](docs/screenshots/17-announcement-send.png)

Duyuru hazırlama, sakinlere toplu e-posta gönderimi ve WhatsApp Web aktarımı.

### Raporlar

[![Raporlar](docs/screenshots/18-reports.png)](docs/screenshots/18-reports.png)

Aylık tahsilat ve gider dökümleri, dönem filtreleri ve PDF çıktısı. Bu ekran MySQL/MariaDB gerektirir (aşağıdaki [Bilinen Sınırlamalar](#bilinen-sınırlamalar) bölümüne bakın).

### VakıfBank Entegrasyonu

[![VakıfBank hareketleri](docs/screenshots/19-vakifbank-transactions.png)](docs/screenshots/19-vakifbank-transactions.png)
[![VakıfBank ayarları](docs/screenshots/20-vakifbank-settings.png)](docs/screenshots/20-vakifbank-settings.png)

Hesap hareketi izleme ekranı, manuel eşleştirme ve entegrasyon ayarları. Ayrıntılar için [VakıfBank Entegrasyonu](#vakıfbank-entegrasyonu) bölümü.

### Ayarlar

[![Telegram ayarları](docs/screenshots/21-settings.png)](docs/screenshots/21-settings.png)
[![Genel ayarlar](docs/screenshots/22-settings-general.png)](docs/screenshots/22-settings-general.png)

Telegram bildirim ayarları (bot token'ı veritabanında şifreli saklanır) ve genel sistem ayarları.

### Yetkili Kullanıcılar

[![Yetkililer](docs/screenshots/23-authorities.png)](docs/screenshots/23-authorities.png)

Yönetici hesapları ve süreli daire sahibi rapor bağlantılarının yönetimi.

### Korunmuş İndirme Ekranı

[![İndirmeler](docs/screenshots/24-downloads.png)](docs/screenshots/24-downloads.png)

Ortam değişkenleriyle yapılandırılabilen şifre korumalı proje paketi indirme ekranı (`/downloads`).

---

## Özellikler

### 1. Çoklu Site Desteği
- Sınırsız site, blok ve daire tanımlama
- Site bazlı filtreleme: tüm listeleme ekranlarında site, blok, yıl, ay ve ödeme kaynağı filtreleri
- Doluluk durumu takibi (dolu / boş daire)

### 2. Aidat Tahakkuku
- Dönem bazlı (yıl + ay) aidat tanımlama
- Daire + dönem tekilliği: aynı daireye aynı dönemde çift tahakkuk engellenir
- Son ödeme tarihi ve not alanları
- Borçlu daire listesi ve kalan bakiye takibi

### 3. Ödeme Yönetimi
- Banka, EFT, kart ve nakit yöntemleri
- **Kısmi ödeme desteği**: aidat birden fazla ödemeye bölünebilir
- Tutar doğrulaması: girilen ödeme kalan borcu aşamaz
- Otomatik makbuz numarası üretimi (`MAK-` ve banka eşleştirmesinde `BNK-` önekli)
- Ödeme kaynağı filtresi: panelden girilen, bankadan otomatik eşleşen ve manuel eşleştirilen ödemeler ayrı görüntülenebilir
- Silinen/güncellenen tüm ödemeler denetim kaydına yazılır

### 4. Makbuz Sistemi
- Ekran görünümlü makbuz sayfası
- Dompdf ile A4 PDF makbuz indirme
- Sakine gönderilebilecek hazır WhatsApp mesaj metni

### 5. Gider Takibi
- Kategori bazlı gider kayıtları (elektrik, su, asansör bakımı vb.)
- Tarih ve tutar ile gider geçmişi
- Dashboard'da dönem gider özeti

### 6. Duyuru Sistemi
- Duyuru oluşturma ve düzenleme
- Sakinlere toplu e-posta gönderimi (Laravel Mail)
- Duyuru metnini WhatsApp Web üzerinden paylaşma

### 7. Raporlama
- Aylık tahsilat ve gider dökümleri
- Gelir/gider dengesi ve bekleyen borç raporları
- PDF yönetim raporu çıktısı

### 8. VakıfBank Hesap Hareketi Entegrasyonu (altyapı)
- Hesap hareketi izleme ekranı (gelen / eşleşen / bekleyen sekmeleri)
- Manuel eşleştirme: banka hareketini seçilen aidata bağlama
- Akıllı eşleştirme yardımı: gönderici adı benzerlik analizi (Türkçe karakterler normalize edilir) ve havale açıklamasından daire + dönem + tutar çıkarma
- Test / üretim ortamı ayarları, senkronizasyon aralığı (1-60 dk)
- Kurumsal banka şifresi veritabanında şifreli saklanır
- `bank:sync-vakifbank` artisan komutu ve dakikalık zamanlayıcı

### 9. Yetkili Kullanıcı Yönetimi
- Yönetici hesapları oluşturma, düzenleme, devre dışı bırakma
- Brute-force koruması: 5 hatalı girişte 15 dakikalık hesap kilidi
- Süreli daire sahibi rapor bağlantıları (token tabanlı public link)

### 10. Denetim İzi (Audit Log)
- Giriş/çıkış, ödeme/gider/aidat CRUD, entegrasyon ve ayar değişiklikleri
- Kullanıcı, IP adresi, tablo ve kayıt bilgisiyle kayıt

### 11. Bildirim ve Entegrasyon Ayarları
- Telegram bot ayarları (token veritabanında şifreli)
- Genel ayarlar: genel URL ve destek e-postası
- Korumalı paket indirme ekranı yapılandırması

---

## Teknoloji Yığını

| Katman | Teknoloji |
|---|---|
| Sunucu tarafı | PHP 8.3+, Laravel 13 |
| Ön yüz | Blade, Vite 8, Tailwind CSS 4, Tabler UI + Tabler ikonları |
| Veritabanı | MySQL / MariaDB (tam özellik) veya SQLite (bkz. sınırlamalar) |
| PDF üretimi | Dompdf 3.x |
| Oturum / Önbellek / Kuyruk | Veritabanı sürücüsü |
| Kimlik doğrulama | Oturum tabanlı, özel AuthController (hesap kilitlemeli) |
| Test | PHPUnit 12 |

---

## Kurulum

### Gereksinimler

- PHP 8.3 veya üzeri (openssl, mbstring, pdo_sqlite/pdo_mysql, curl, zip, fileinfo eklentileriyle)
- Composer
- Node.js ve npm
- MySQL/MariaDB (önerilir) veya SQLite

### Adımlar

```bash
# 1. Bağımlılıkları kur
composer install
npm install

# 2. Ortam dosyasını hazırla ve anahtar üret
cp .env.example .env
php artisan key:generate

# 3. Veritabanını yapılandır (.env)
#    MySQL önerilir:
#      DB_CONNECTION=mysql
#      DB_HOST=127.0.0.1
#      DB_PORT=3306
#      DB_DATABASE=aidatpro
#      DB_USERNAME=root
#      DB_PASSWORD=
#    Ya da hızlı deneme için SQLite:
#      DB_CONNECTION=sqlite   (database/database.sqlite otomatik kullanılır)

# 4. Tabloları kur ve örnek veriyi yükle
php artisan migrate --seed

# 5. Ön yüz varlıklarını derle
npm run build

# 6. Sunucuyu başlat
php artisan serve
```

Uygulama http://127.0.0.1:8000 adresinde çalışır.

Ayrıntılı kurulum rehberleri: [KURULUM.md](KURULUM.md) (Türkçe) · [INSTALLATION.md](INSTALLATION.md) (İngilizce)

> **Not:** Raporlar ekranı MySQL'e özgü `MONTH()` / `YEAR()` SQL fonksiyonları kullandığından yalnızca MySQL/MariaDB üzerinde çalışır. SQLite ile hızlı deneme yapacaksanız Raporlar ekranının hata vereceğini unutmayın.

### Geliştirme ortamı

Kod izleme, kuyruk dinleme ve Vite geliştirme sunucusunu tek komutla çalıştırın:

```bash
composer run dev
```

---

## Demo Hesabı

Seed sonrası hazır gelen örnek yönetici hesabı:

```text
E-posta: skulloger@gmail.com
Şifre:   asdasdasd
```

İlk girişten sonra bu şifreyi mutlaka değiştirin ve gerçek kullanıma geçmeden önce demo verilerini temizleyin.

Örnek veri içeriği: 1 site (Nilüfer Sitesi), 3 blok, 12 daire, sakinler, 2025-2026 dönemlerine ait aidatlar, ödemeler, giderler ve duyurular.

---

## VakıfBank Entegrasyonu

Arayüz, ayarlar, veri modeli, zamanlayıcı ve manuel eşleştirme akışı **hazırdır**; ancak gerçek hesap hareketlerini çeken SOAP çağrısı henüz bağlanmamıştır (`VakifbankSyncService` içinde placeholder vardır). Canlı kullanım için:

1. VakıfBank **Online Hesap Hareketleri** hizmetinin kurum hesabı için açılması gerekir.
2. Entegrasyon ayarları ekranından müşteri no, 17 haneli hesap no, kurumsal kullanıcı adı/şifre ve SOAP servis adresi girilir.
3. Şifreler Laravel `encrypted` cast ile veritabanında şifreli tutulur.

Bankadan hareket gelene kadar ekran demo verisiyle çalışır; yönetici hareketleri manuel eşleştirme ile aidatlara bağlayabilir. Eşleştirme yardımcısı; havale açıklamasındaki daire kodu (55 puan), dönem (20 puan), sakin adı (15 puan) ve tutar (10 puan) ile puanlama yapar ve belirsiz durumları otomatik onaya düşürür.

Bu projede **online ödeme (sanal POS) yoktur**; model, sakinin banka havalesiyle ödemesi ve yöneticinin bunu aidata işlemesidir.

---

## Zamanlayıcı

Banka kontrolünün zamanlaması Laravel Schedule ile yönetilir:

```bash
php artisan schedule:work   # geliştirme
# ya da sunucuda tek cron girişi:
* * * * * cd /proje/yolu && php artisan schedule:run >> /dev/null 2>&1
```

`bank:sync-vakifbank` komutu her dakika çalışır, entegrasyonun `sync_interval_minutes` değeri gelmişse kontrol tetiklenir ve `withoutOverlapping` ile üst üste binme engellenir.

---

## Güvenlik

- Banka kurumsal şifresi ve Telegram bot token'ı veritabanında şifreli saklanır
- 5 hatalı girişte 15 dakikalık hesap kilidi
- CSRF koruması ve oturum yeniden oluşturma (Laravel varsayılanları)
- Denetim kayıtları: kritik tüm işlemler kullanıcı + IP ile loglanır
- İndirme endpoint'inde hız limiti (6 istek/dk)
- Süreli, token tabanlı daire sahibi rapor bağlantıları

Ayrıntılar için [SECURITY.md](SECURITY.md).

---

## Bilinen Sınırlamalar

- **Raporlar ekranı SQLite'ta çalışmaz**: sorgular MySQL'e özgü `MONTH()` / `YEAR()` fonksiyonları kullanır. Tam deneyim için MySQL/MariaDB kullanın.
- **VakıfBank SOAP bağlantısı henüz canlı değildir**: senkronizasyon servisi altyapı seviyesindedir; canlı hesap hareketi akışı banka hizmeti açıldığında aktifleştirilir.
- **Online ödeme yoktur**: sanal POS / kredi kartı entegrasyonu bulunmaz; ödemeler yönetici tarafından kaydedilir.
- **Şifre sıfırlama akışı yoktur**: unutulan şifre için veritabanından müdahale gerekir.

---

## Test

```bash
composer test
# veya
php artisan test
```

Mevcut test kapsamı minimaldir (örnek testler + indirme ekranı testi); katkı beklenir.

---

## Katkı

Hata bildirimi, özellik önerisi ve pull request göndermekten çekinmeyin. Başlamadan önce [CONTRIBUTING.md](CONTRIBUTING.md) dosyasını okuyun.

## Lisans

AidatPro MIT lisansı ile yayımlanır. Ayrıntılar için [LICENSE](LICENSE) dosyasına bakın.

## Bağış

Projeye destek olmak isterseniz:

```text
USDT TRC20: 0x9368198ad43a66aa837759a062bfe8b472b984c3
```
