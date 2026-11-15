# Go Kids Play — Operasyon Yönetimi Proje İncelemesi

[English version](README.md) · [Mimari](docs/architecture.md) · [Görsel notu](docs/screenshots/README.md)

Go Kids Play, çocuk oyun alanı işletmesinin günlük operasyonlarını tek bir akışta yönetmek için geliştirilmiş özel ve ticari bir uygulamadır. Müşteri kayıtları, üyelikler, süreli oyun oturumları, ödemeler, personel yetkileri ve operasyonel raporlama aynı sistem içinde ele alınır.

> **Portföy kapsamı:** Bu depo kaynak kod içermeyen bir proje incelemesidir. Özel uygulama kodu, Git geçmişi, kimlik bilgileri, müşteri verileri ve altyapı ayrıntıları yayımlanmamıştır. Depo kurulabilir bir açık kaynak uygulama değildir.

## Çözülen işletme problemi

Bir oyun alanında aile kaydı, çocukların giriş ve süre takibi, paket/üyelik kullanımı, ödeme alma, iptal ve iade, doğum günü organizasyonları ile gün sonu mutabakatı eş zamanlı ilerler. Ayrı araçlarla yürütülen bu süreçler güncel operasyon durumunu izlemeyi ve geçmiş işlemleri incelemeyi zorlaştırabilir.

Uygulama, ön büro ve yönetim işlerini ortak operasyon kayıtları üzerinde birleştirirken rol ve şube bazlı erişim sınırları sağlar.

## Doğrulanan iş akışları

### Müşteri ve üyelik yönetimi

- Müşteri/çocuk profilleri, arama, hareket geçmişi, not, etiket ve cüzdan görünümleri
- Üyelik paketleri, satış, kullanım takibi, duraklatma/devam ettirme ve iptal
- Kişiye özel haklar, kampanyalı paketler ve üyelik raporları
- Müşteri işlem geçmişi ve CSV odaklı raporlama desteği

### Oyun süresi takibi

- Süreli ve sınırsız oyun oturumları
- Filtre, geri sayım, yoğun kart ve tablo görünümleri içeren canlı oturum ekranı
- Duraklatma, devam ettirme, süre uzatma, iptal ve nedenli oturum kapatma
- Realtime senkronizasyon ve tamamlanan oturum geçmişi

### Kasa ve ödeme

- Nakit, kart ve cüzdan arasında bölünebilen ödemeler
- Süre uzatma, iptal/iade kayıtları ve iade geçmişi
- Kasa açılışı, beklenen tutar hesabı, kapanış ve kapanış geçmişi
- Atomik perakende satış/iptal ve stok iş akışları

### Doğum günü organizasyonları

- Doğum günü paketleri ve organizasyon kayıtları
- Durum, katılımcı, zaman çizelgesi, paket ve ödeme yönetimi
- Yaklaşan etkinlik görünümü ve organizasyon raporları

### Personel ve yetkilendirme

- Rol bazlı sayfa ve modül erişimi
- Kullanıcı bazında yetki istisnaları
- Personel dizini, vardiya kayıtları ve hesap yaşam döngüsü
- Çok şubeli kullanım için şube kapsamlı erişim temeli

### Raporlama

- Dönemsel gelir ve ödeme yöntemi dağılımı
- Katılım, günlük trafik ve yoğun saat analizi
- Müşteri, paket, organizasyon ve personel içgörüleri
- Perakende, fire, indirim, gün sonu ve operasyon notu raporları

### Mobil ve masaüstü kullanım

- Standalone kullanım için PWA manifesti
- Duyarlı navigasyon ve mobil operasyon ekranları
- Ebeveyn ve TV/kiosk yüzeyleri için ayrı rotalar
- macOS, Windows ve Linux için Electron paketleme yapılandırması

## Teknolojiler

- **Uygulama:** Next.js 14 App Router, React 18, TypeScript
- **Arayüz:** Tailwind CSS, Radix UI, shadcn bileşenleri, Lucide, Recharts
- **Backend ve veri:** Supabase, PostgreSQL, SQL migration'ları, RPC fonksiyonları, Row Level Security
- **Canlı güncelleme:** Supabase Realtime
- **Dağıtım yüzeyleri:** PWA ve Electron

## Teknik kararlar

- Arayüz ile Supabase sorgu/RPC çağrıları arasında servis katmanı bulunur.
- Çok adımlı finansal ve operasyonel değişiklikler için veritabanı fonksiyonları kullanılır.
- Şube kimlikleri, RLS politikaları ve rol kontrolleri konuma bağlı erişimin temelini oluşturur.
- Oturum deposu ilk yükleme, realtime olayları, yeniden bağlanma sonrası senkronizasyon ve yerel geri sayımı birlikte yönetir.
- Retry, güvenli RPC, ağ durumu, audit log ve realtime gözetimi için ayrı güvenilirlik yardımcıları vardır.
- Aynı Next.js arayüzü web/PWA ve Electron masaüstü paketleri için yapılandırılmıştır.

Ayrıntılar için [docs/architecture.md](docs/architecture.md) dosyasına bakın.

## Mevcut durum ve sınırlar

- İnceleme kod yollarını ve şema tanımlarını doğrular; üretim dağıtımı, üretim güvenliği, ticari sonuçlar veya kullanıcı sayıları doğrulanmamıştır.
- İncelenen proje yapısında otomatik test paketi veya test komutu tespit edilmedi; bu çalışma geçen testler ya da temiz bir kalite kapısı iddia etmez.
- Ödeme terminali soyutlaması varsayılan olarak mock sağlayıcı kullanıyor.
- Bazı panel bileşenleri örnek veri, diğerleri servis destekli veri kullanıyor.
- Ebeveyn telefon/OTP akışında demo odaklı davranış bulunuyor; üretim kimlik doğrulaması olarak sunulmuyor.

## Görseller

Bu sürümde uygulama ekran görüntüsü yayımlanmadı. Mevcut demo veri üreticisi yapılandırılmış Supabase istemcisi üzerinden yazma yapıyor; çevrimdışı mod ise istenen tüm operasyon ekranlarını izole sentetik veriyle beslemiyor. Üretim sistemine bağlanma riski almak veya yalnızca görsel için ayrı bir sahte ürün geliştirmek yerine görsel adımı bilinçli olarak atlandı. Ayrıntı: [docs/screenshots/README.md](docs/screenshots/README.md).

Bu depoda uygulama kaynak kodu, veritabanı yedeği, ortam dosyası, kimlik bilgisi veya özel Git geçmişi bulunmaz.

