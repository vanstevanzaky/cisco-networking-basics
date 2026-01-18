# Modul 4: Build a Home Network

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Konsep Inti

### 1. Home Network Components

**Integrated Router (Wireless Router):**
Menggabungkan beberapa fungsi dalam 1 device:
- **Router** - koneksi ke Internet (WAN)
- **Switch** - port LAN (biasanya 4 port)
- **Access Point** - wireless connectivity
- **Firewall** - basic security (NAT)
- **DHCP Server** - auto IP assignment

### 2. Koneksi Home Router

| Port/Interface | Fungsi |
|----------------|--------|
| **WAN/Internet** | Koneksi ke modem ISP |
| **LAN (1-4)** | Koneksi wired devices |
| **Wireless** | Koneksi Wi-Fi clients |
| **USB** | Shared storage/printer |

---

## ⚙️ Konfigurasi Dasar

### Setup Wizard
1. Koneksi ke router (kabel/Wi-Fi)
2. Akses web interface (192.168.1.1 atau 192.168.0.1)
3. Login dengan default credentials
4. Jalankan setup wizard

### Konfigurasi Penting

| Setting | Rekomendasi |
|---------|-------------|
| **Admin password** | Ubah dari default! |
| **SSID** | Ubah, jangan gunakan info personal |
| **Wi-Fi password** | Minimal 12 karakter, kompleks |
| **Security mode** | WPA2-PSK atau WPA3 |
| **Firmware** | Update ke versi terbaru |

---

## 🌐 DHCP & IP Addressing

**DHCP (Dynamic Host Configuration Protocol):**
- Router sebagai DHCP server
- Auto assign IP ke clients
- Default range: 192.168.1.100 - 192.168.1.254

**Static IP:**
- Assign manual untuk server/printer
- Di luar DHCP range atau reservation

**NAT (Network Address Translation):**
- Translate private IP ↔ public IP
- Menyembunyikan internal network
- 1 public IP untuk banyak private devices

---

## 🔒 Home Network Security

**Konfigurasi penting (dari Lab 4.4.4):**
- Ubah **admin password** default
- Set **SSID** (jangan biarkan default)
- Gunakan **WPA2 Personal** dengan passphrase kuat
- Konfigurasi **DHCP** range sesuai kebutuhan

---

## 💡 Poin Penting

1. **Home router = router + switch + AP + firewall**
2. **SELALU ubah default password** (admin & Wi-Fi)
3. **WPA2/WPA3** wajib, WEP/WPA jangan digunakan
4. **NAT** menyembunyikan internal network dari Internet
5. **DHCP** auto-assign IP, static untuk server/printer
6. **Firmware update** penting untuk patch vulnerability

---

**Konsep Terkait:** Wireless Security (Modul 3), NAT (Modul 12), DHCP (Modul 11)
