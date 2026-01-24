# Modul 4: Build a Home Network

**Modul:** 4 - Build a Home Network  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- Wireless Router = Router + Switch + AP + DHCP Server (all-in-one)
- Konfigurasi penting: Ubah password default, set SSID, gunakan WPA2/WPA3
- DHCP otomatis assign IP, NAT translate private ↔ public IP

---

## 📚 Materi

### 1. Home Network Components

**Wireless Router (All-in-One):**
| Fungsi | Penjelasan |
|--------|------------|
| Router | Koneksi ke Internet (WAN) |
| Switch | Port LAN (biasanya 4 port) |
| Access Point | Wireless connectivity |
| DHCP Server | Auto IP assignment |
| Firewall | Basic security (NAT) |

---

### 2. Port pada Wireless Router

| Port | Fungsi |
|------|--------|
| **WAN/Internet** | Ke modem ISP |
| **LAN (1-4)** | Ke PC, printer (wired) |
| **Wireless** | Ke laptop, HP (Wi-Fi) |

---

### 3. Konfigurasi Dasar

**Akses Router:**
1. Hubungkan PC ke router (kabel/Wi-Fi)
2. Buka browser → `192.168.1.1` atau `192.168.0.1`
3. Login: `admin` / `admin` (default)

**Settings yang WAJIB Diubah:**
| Setting | Nilai |
|---------|-------|
| Admin password | Ubah dari default! |
| SSID | Nama jaringan (jangan default) |
| Wi-Fi password | Minimal 12 karakter |
| Security mode | WPA2 atau WPA3 |

---

### 4. DHCP dan NAT

**DHCP:**
- Router = DHCP server
- Client dapat IP otomatis
- Range contoh: 192.168.1.100 - 192.168.1.254

**NAT:**
- Translate private IP ↔ public IP
- Banyak device share 1 public IP
- Menyembunyikan internal network

---

## 💡 Poin Penting

1. **Wireless Router** = 5 fungsi dalam 1 device
2. **WAN port** ke modem, **LAN port** ke PC
3. **UBAH password default** router (keamanan!)
4. **WPA2/WPA3** untuk keamanan Wi-Fi
5. **DHCP** = IP otomatis untuk client
6. **NAT** = share 1 public IP untuk banyak device

---

**Praktik:** [Lab 1 - Configure Wireless Router](../Packet%20Tracer%20Labs/Lab%201%20-%20Configure%20Wireless%20Router%20and%20Client%20(4.4.4)/lab1.md)
