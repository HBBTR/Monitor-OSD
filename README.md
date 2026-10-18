# Monitor OSD Control / Monitör OSD Kontrolü

A Windows application for controlling monitor settings (brightness, contrast, picture modes and more) directly through **DDC/CI**, with an automatic **software (gamma) fallback** when the monitor or graphics driver does not accept DDC writes.

Masaüstü üzerinden monitör ayarlarını (parlaklık, kontrast, görüntü modları ve daha fazlası) **DDC/CI** ile doğrudan kontrol eden bir Windows uygulaması. Monitör veya ekran kartı sürücüsü DDC yazmalarını kabul etmediğinde otomatik **yazılım (gamma) yedeğine** geçer.

---

## 🇹🇷 Türkçe

### Özellikler

- **Parlaklık ve Kontrast**: Kaydırıcılarla anında ayar; her yazma işlemi geri okumayla **doğrulanır** (sürücünün sessizce yuttuğu yazmalar tespit edilir), uygulanamadığında **yazılım (gamma ramp) yedeği** devreye girer
- **Görüntü Modu**: Monitörün OSD görüntü modu menüsünün DDC karşılığı; DDC çalışmadığında ekran geneli gamma ile uygulanan **yazılım modları** (Manzara, Standart, Sinema, Oyun, Gece Manzarası, sRGB)
- **Renk Kontrolleri**: Kırmızı/Yeşil/Mavi kazanç, kara seviyesi, ton (tint), renk sıcaklığı
- **Ses**: Hoparlör ses seviyesi ve sessize alma
- **Giriş Kaynağı**: Monitörün desteklediği girişler (HDMI, VGA vb.) arasında geçiş — listede monitörün kendi bildirdiği girişler görünür
- **Güç Kipi**: Monitörü kapatma / açma (DDC üzerinden)
- **Bilgi Kartları**: Dikey/yatay tarama frekansı, DDC/CI (MCCS) sürümü gibi salt-okunur değerler
- **Ham VCP Erişimi**: Hex kod ile herhangi bir VCP özelliğini okuma/yazma (ileri kullanıcılar için)
- **Ayar Kaydet / Sıfırlama**: Ayarları monitöre kaydetme, görüntü ayarlarını geri yükleme, fabrika ayarlarına dönme
- **Otomatik Monitör Tanıma**: Marka ve model her açılışta monitörden algılanır; sabit isim yok. Üreticiye özgü özellikler yalnızca o monitör destekliyorsa gösterilir
- **Çoklu Monitör Desteği**: Tüm monitörler taranır, her biri ayrı ayrı yapılandırılır
- **Çift Dil**: Arayüz **Türkçe / İngilizce** dil seçimiyle gelir; seçim hatırlanır

### Nasıl Çalışır

Uygulama, Windows'un DDC/CI API'si (`dxva2.dll`) üzerinden monitörle iletişim kurar. Bazı ekran kartı sürücüleri DDC/CI yazma komutlarını sessizce yutar: komut başarılı döner ama monitör değişikliği uygulamaz. Bu uygulama her yazma işleminden sonra değeri **geri okuyarak doğrular**; yazmanın uygulanmadığını algılarsa parlaklık, kontrast ve renk ayarlarını yazılım (gamma ramp) ile uygular. DDC yolu düzeldiğinde otomatik olarak tekrar DDC'ye döner.

### Çalıştırma

1. `Monitor.exe` dosyasını çalıştırın (kurulum gerekmez)
2. Monitörün OSD menüsünden **DDC/CI** seçeneğinin açık olduğundan emin olun

### Sistem Gereksinimleri

- Windows 10 / 11
- DDC/CI destekleyen bir monitör (menüde açık olmalı)
- Yönetici yetkisi gerekmez

### Sınırlamalar

- Bazı GPU sürücüleri DDC/CI yazma yolunu kilitler; bu durumda uygulama yazılım yedeğiyle çalışmaya devam eder ve kilit açıldığında otomatik DDC'ye döner
- Yazılım (gamma) modu ekran genelinde uygulanır; monitörün kendi OSD'sini değiştirmez

---

## 🇬🇧 English

### Features

- **Brightness & Contrast**: Instant slider control; every write is **verified by reading back** (detects writes silently swallowed by drivers) and falls back to **software (gamma ramp)** automatically when the monitor does not apply them
- **Picture Mode**: DDC equivalent of the monitor's OSD picture mode menu, plus **software modes** (Scenery, Standard, Theater, Game, Night View, sRGB) applied screen-wide via gamma when DDC is unavailable
- **Color Controls**: Red/Green/Blue gain, black level, tint, color temperature
- **Audio**: Speaker volume and mute
- **Input Source**: Switch between the monitor's supported inputs (HDMI, VGA, etc.) — the list comes from the monitor itself
- **Power Mode**: Turn the monitor off / on via DDC
- **Info Cards**: Read-only values such as vertical/horizontal scan frequency and DDC/CI (MCCS) version
- **Raw VCP Access**: Read/write any VCP feature by hex code (for advanced users)
- **Save / Reset**: Save settings to the monitor, restore image settings, factory reset
- **Automatic Monitor Detection**: Brand and model are detected from the monitor on every launch; nothing is hardcoded. Vendor-specific controls appear only if the connected monitor supports them
- **Multi-Monitor Support**: All monitors are scanned and configured independently
- **Bilingual UI**: Ships with a **Turkish / English** language toggle; the choice is remembered

### How It Works

The app communicates with the monitor through the Windows DDC/CI API (`dxva2.dll`). Some graphics drivers silently swallow DDC/CI write commands: the call reports success but the monitor never applies the change. This application **verifies every write by reading the value back**; if the write was not applied, brightness, contrast and color adjustments are applied via software (gamma ramp) instead. When the DDC path recovers, the app switches back to DDC automatically.

### Running

1. Run `Monitor.exe` (no installation required)
2. Make sure **DDC/CI** is enabled in the monitor's OSD menu

### Requirements

- Windows 10 / 11
- A DDC/CI-capable monitor (enabled in its OSD menu)
- No administrator rights required

### Limitations

- Some GPU drivers lock the DDC/CI write path; in that case the app keeps working via the software fallback and returns to DDC automatically once unlocked
- Software (gamma) mode is applied screen-wide; it does not change the monitor's own OSD settings
