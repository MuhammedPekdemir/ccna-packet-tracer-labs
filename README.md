# CCNA Packet Tracer Labs

Cisco Packet Tracer üzerinde kurduğum ağ senaryoları. Her senaryo gerçek bir ağ problemini ele alıyor.Farklı ağları birbirine bağlamak, aynı switch üzerindeki kullanıcıları ayırmak, switch'leri uzaktan yönetmek, VLAN'ları birden fazla switch'e taşımak ve VLAN yönetimini merkezileştirmek.

Her klasörde Packet Tracer dosyası, cihaz yapılandırmaları, test adımları ve karşılaştığım hatalar yer alıyor.

## Senaryolar

### 01 – Statik Yönlendirme
**Problem:** İki farklı ağdaki (10.0.0.0/8 ve 30.0.0.0/8) bilgisayarlar birbirine ulaşamıyor; router'lar yalnızca kendilerine doğrudan bağlı ağları tanıyor.
**Çözüm:** İki router seri hat (PPP) ile bağlandı, her router'a karşı taraftaki ağ için statik rota eklendi.
**Test:** PC0'dan PC1'e ping başarılı.
**Konular:** Router arayüz yapılandırması, DCE/DTE ve `clock rate`, PPP, `ip route`, `show ip route`

### 02 – VLAN
**Problem:** Aynı switch'e bağlı farklı departmanların trafiğinin birbirinden ayrılması gerekiyor.
**Çözüm:** Switch iki VLAN'a bölündü (VLAN 10 ve VLAN 20), portlar access modda ilgili VLAN'a atandı.
**Test:** Aynı VLAN'daki cihazlar haberleşiyor, farklı VLAN'dakiler haberleşemiyor.
**Konular:** VLAN oluşturma, access port, `show vlan brief`

### 03 – Telnet ile Uzaktan Yönetim
**Problem:** Switch'i yapılandırmak için her seferinde konsol kablosuyla başına gitmek gerekiyor.
**Çözüm:** Switch'e yönetim IP'si verildi (SVI), yerel kullanıcı ve şifreler tanımlandı, VTY hatları açıldı.
**Test:** PC'den `telnet` ile switch'e bağlanıp ayrıcalıklı moda geçildi.
**Konular:** `interface vlan 1`, `line vty`, `login local`, `enable secret` ile `enable password` farkı

### 04 – Trunk, DTP ve Native VLAN
**Problem:** VLAN'lar iki ayrı switch'e yayılmış durumda; aynı VLAN'daki ama farklı switch'teki cihazların haberleşmesi gerekiyor. Ayrıca iki switch arasındaki hatta VLAN etiketini anlamayan bir hub ve ona bağlı bir bilgisayar var.
**Çözüm:** Switch'ler arası bağlantı DTP ile trunk yapıldı. Hub'daki bilgisayarın etiketsiz trafiği VLAN 10'a düşsün diye native VLAN iki tarafta da 10 olarak ayarlandı.
**Test:** Farklı switch'lerdeki aynı VLAN cihazları ve hub'daki bilgisayar birbirine ping atabiliyor; native VLAN uyuşmazlığı hatası gözlemlenip giderildi.
**Konular:** DTP (`dynamic auto` / `dynamic desirable`), 802.1Q, native VLAN, allowed VLAN, CDP

### 05 – VTP
**Problem:** Altı switch'li bir ağda her VLAN'ı her switch'e tek tek elle yazmak zahmetli ve hataya açık.
**Çözüm:** VLAN'lar yalnızca server switch'te oluşturuldu; VTP ile client switch'lere otomatik dağıtıldı. Bir switch transparent moda alınarak kendi yerel VLAN'larını tutması sağlandı.
**Test:** Client switch'lerde, transparent switch'in arkasındakiler dahil, VLAN 10–40 otomatik göründü; client'ta VLAN oluşturma denemesi reddedildi.
**Konular:** VTP domain, server / client / transparent modları, revision number

## Klasör yapısı

```
NN-senaryo/
├── README.md     # Topoloji, adresleme, yapılandırma, test ve sorun giderme
├── configs/      # Her cihazın komutları
└── *.pkt         # Packet Tracer dosyası
```
