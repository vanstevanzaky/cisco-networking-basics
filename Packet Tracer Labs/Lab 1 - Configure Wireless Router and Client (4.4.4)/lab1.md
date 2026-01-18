# Lab 1: Konfigurasi Router Nirkabel dan Klien

**Module:** 4 (Build a Home Network)  
**Topik:** 4.4 Set Up a Home Router  
**Tanggal Selesai:** 18 Januari 2026  
**Status:** ✅ SELESAI

---

## 📝 Summary (TL;DR)

**Quick Overview:**
- ✅ Setup home wireless network dari cable modem sampai client devices
- ✅ Konfigurasi: SSID "MyHome", WPA2 Personal, DHCP max 10 users
- ✅ 3 clients berhasil terhubung (1 wireless + 2 wired)
- ✅ Router password changed: MyPassword1!
- ✅ Web connectivity test: skillsforall.srv → SUCCESS
- ✅ IP addressing: 192.168.0.1 (gateway), clients 192.168.0.2-11
- ✅ Completion: 100%

**Key Learning:** Physical topology setup, wireless security configuration, DHCP management, dan web-based connectivity testing.

---

## �📌 Tujuan Lab

Melakukan konfigurasi dasar home wireless router dan client devices dengan menggunakan Packet Tracer:

- **Bagian 1:** Hubungkan perangkat secara fisik
- **Bagian 2:** Konfigurasi router nirkabel (SSID, wireless standards)
- **Bagian 3:** Konfigurasi IP addressing dan uji konektivitas

---

## �️ Perangkat & Komponen yang Digunakan

### End Devices (Perangkat Akhir)
| Nama Alat | Fungsi | Spesifikasi |
|-----------|--------|-------------|
| **Home Wireless Router** | Menghubungkan perangkat lokal ke internet, DHCP server, wireless access point | 2.4 GHz, 802.11b/g/n, 4 port Gigabit Ethernet |
| **Office PC** | Client wired untuk initial setup & testing | Fast Ethernet NIC |
| **Laptop** | Client wireless untuk testing wireless connectivity | Wireless NIC (802.11n compatible) |
| **Bedroom PC** | Client wired/wireless tambahan | Ethernet/Wireless NIC |
| **TV** | Display device (simulasi layanan TV dari ISP) | Coaxial input |

### Intermediary Devices (Perangkat Perantara)
| Nama Alat | Fungsi | Port/Interface |
|-----------|--------|----------------|
| **Cable Modem** | Konversi sinyal coaxial dari ISP ke Ethernet | 1x Coaxial port, 1x Ethernet port |
| **Cable Splitter** | Membagi sinyal coaxial untuk TV dan Cable Modem | 1x Input, 2x Output (Coaxial) |

### Media Transmisi (Kabel)
| Jenis Kabel | Warna di PT | Digunakan Untuk | Konektor |
|-------------|-------------|-----------------|----------|
| **Coaxial Cable** | Hitam putus-putus | Cable Splitter ↔ Cable Modem, Cable Splitter ↔ TV | BNC connector |
| **Copper Straight-Through** | Garis hitam solid | Cable Modem ↔ Router (Internet port), Office PC ↔ Router (LAN port) | RJ-45 (Ethernet) |
| **Wireless Connection** | Garis hijau gelombang | Laptop ↔ Router (2.4 GHz) | N/A (Radio waves) |

### External Network
| Komponen | Fungsi |
|----------|--------|
| **The Internet (Cloud)** | Simulasi koneksi ke internet publik |
| **skillsforall.srv** | Web server untuk testing connectivity |

---

## 🔧 Hasil Praktik & Konfigurasi

### Part 1: Koneksi Perangkat ✅

**Topologi yang dibangun:**
- 1x Home Wireless Router (gateway + DHCP + AP)
- 1x Cable Modem (ISP connection)
- 1x Cable Splitter (signal distribution)
- 1x TV (coaxial service)
- 3x Client devices (1 laptop wireless, 2 PCs wired)
- Internet connection ke skillsforall.srv

**Physical Connections:**
1. **Internet → Cable Splitter:** Coaxial cable
2. **Cable Splitter → Cable Modem:** Coaxial cable (Port 1)
3. **Cable Splitter → TV:** Coaxial cable (Port 2)
4. **Cable Modem → Router:** Copper straight-through (Internet port)
5. **Office PC → Router:** Copper straight-through (GigabitEthernet 1)
6. **Bedroom PC → Router:** Copper straight-through (GigabitEthernet 2)
7. **Laptop → Router:** Wireless (2.4 GHz, 802.11n)

**Link Verification:**
- ✅ Semua kabel connections menunjukkan green light
- ✅ Wireless connection established (signal waves)
- ✅ NIC link lights menunjukkan "connected"
- ✅ Semua perangkat terdeteksi dalam network

### Part 2: Konfigurasi Router Nirkabel ✅

| Setting | Konfigurasi |
|---------|------------|
| **SSID** | MyHome |
| **SSID Broadcast** | Enabled |
| **Wireless Standard** | 802.11b/g/n (2.4 GHz Network) |
| **Channel** | 6 (2.4 GHz) |
| **Security** | WPA2 Personal |
| **WPA2 Passphrase** | MyPassPhrase1! |
| **DHCP** | Enabled |
| **DHCP Max Users** | 10 |
| **Default Gateway** | 192.168.0.1 |
| **Router Admin Password** | MyPassword1! |

**Langkah Konfigurasi:**
1. Akses router melalui web browser (http://192.168.0.1)
2. Login dengan kredensial default (admin/admin)
3. Setup → Limit DHCP max users ke 10 → Save Settings
4. Administration → Change router password ke MyPassword1! → Save Settings
5. Wireless → Enable 2.4 GHz network, set SSID "MyHome" → Save Settings
6. Wireless Security → Set WPA2 Personal, passphrase "MyPassPhrase1!" → Save Settings
7. Connect laptop via PC Wireless app dengan passphrase MyPassPhrase1!
8. Test connectivity ke skillsforall.srv

### Part 3: IP Addressing & Konektivitas ✅

**Hasil Konfigurasi IP:**

| Device | IP Address | Subnet Mask | Gateway | DHCP |
|--------|-----------|-------------|---------|------|
| Router | 192.168.0.1 | 255.255.255.0 | - | Server |
| Office PC | 192.168.0.2-10 | 255.255.255.0 | 192.168.0.1 | ✅ |
| Laptop (Wireless) | 192.168.0.2-10 | 255.255.255.0 | 192.168.0.1 | ✅ |
| Bedroom PC | 192.168.0.2-10 | 255.255.255.0 | 192.168.0.1 | ✅ |

**Connectivity Tests:**

✅ **Web Connectivity Test - Berhasil**
```
Laptop → skillsforall.srv: "Welcome to Skills For All"
Office PC → skillsforall.srv: "Welcome to Skills For All"
Bedroom PC → skillsforall.srv: "Welcome to Skills For All"
```

✅ **Wireless Connection Status**
- Laptop terhubung ke SSID "MyHome" dengan WPA2 Personal
- Passphrase: MyPassPhrase1!
- Signal strength: Excellent
- IP assigned via DHCP: 192.168.0.x

---

## 💡 Pemahaman & Learning Outcomes

### Konsep yang Dipahami:

1. **Router Physical Ports**
   - **LAN Ports:** Menghubungkan perangkat lokal ke network
   - **Internet Port:** Koneksi ke modem (tidak digunakan di lab ini)
   - Pentingnya membedakan port agar tidak misconfigure

2. **Wireless Standards & Compatibility**
   - 802.11b/g/n adalah standar mixed mode yang kompatibel dengan device lama maupun baru
   - Legacy mode diperlukan jika ada device lama yang hanya support 802.11b/g
   - Channel selection penting untuk menghindari interference

3. **DHCP Server Benefits**
   - Otomatis assign IP addresses → menghilangkan manual configuration
   - Lease management → device bisa mendapat IP berbeda saat reconnect
   - Gateway dan DNS info otomatis dikonfigurasi

4. **Network Security Basics**
   - SSID name harus generic (tidak mengungkap model router)
   - WPA2 encryption melindungi wireless traffic
   - Default router credentials harus diganti
   - Guest network bisa digunakan untuk isolasi traffic

5. **DHCP Configuration & Limits**
   - Router IP: 192.168.0.1 (default gateway)
   - DHCP range: 192.168.0.2-11 (max 10 users)
   - Membatasi DHCP users mencegah network overload
   - Subnet mask: 255.255.255.0 (Class C private network)

---

## 🔐 Security Best Practices Diterapkan

✅ **Wireless Security:**
- WPA2-PSK encryption aktif
- SSID menggunakan nama generik
- Broadcast SSID enabled untuk kemudahan (home network)

✅ **Network Access:**
- DHCP enabled untuk security (auto-config lebih aman dari manual)
- Gateway properly configured
- Default credentials dipahami risiko keamanannya

✅ **Recommendations untuk Production:**
1. Disable default admin account
2. Ubah DHCP range sesuai kebutuhan
3. Enable firewall pada router
4. Setup guest network jika ada visitor
5. Regular firmware updates

---

## 📸 Dokumentasi Lab

**File Packet Tracer:** `Configure a Wireless Router and Client.pka`

**Screenshots** (folder: `screenshots/`)

### Physical Setup
- `01-topology.png` - Network topology lengkap (cable modem, splitter, TV, router, PCs)

### Router Configuration
- `02-router-login.png` - Web browser login screen (192.168.0.1)
- `03-dhcp-setup.png` - Setup tab: DHCP maximum users = 10
- `04-admin-password.png` - Administration tab: router password change
- `05-wireless-ssid.png` - Wireless tab: 2.4GHz enabled, SSID "MyHome"
- `06-wireless-security.png` - Wireless Security: WPA2 Personal + passphrase

### Client Connection
- `07-laptop-wireless.png` - PC Wireless app: connection successful
- `08-ip-config.png` - IP Configuration: DHCP assigned 192.168.0.x

### Testing & Verification
- `09-web-tes.png` - Browser test ke skillsforall.srv: "Welcome" message
- `10-completion.png` - Activity completion: 100%

**Total: 10 screenshots** dokumentasi lengkap dari awal sampai selesai.

---

## ✅ Verification Checklist

- [x] Router connected to power & ethernet port
- [x] Client devices dapat detect SSID
- [x] Clients dapat join wireless network
- [x] Clients receive IP dari DHCP (192.168.0.2-11, max 10 users)
- [x] Router password changed ke MyPassword1!
- [x] Web connectivity test ke skillsforall.srv berhasil
- [x] Wireless security (WPA2) aktif
- [x] DHCP server responds to clients

---

## 🎯 Key Learnings

1. **Home network setup membutuhkan planning:** SSID naming, device compatibility, IP addressing
2. **DHCP adalah essential:** Saves time dan mengurangi errors
3. **Wireless standards harus dipilih dengan hati-hati:** Kompatibilitas dengan semua devices
4. **Security from the start:** Tidak ada alasan untuk leave network unprotected
5. **Testing adalah bagian penting:** Verify setiap konfigurasi dengan ping & connectivity tests

---

## 📚 Topik Terkait untuk Review

- Module 3: Wireless Standards (802.11 families)
- Module 11: DHCP Server Configuration
- Module 4: Basic Network Concepts

---

**Catatan Pribadi:**

Lab ini memberikan pengalaman hands-on yang sangat valuable dalam memahami home network setup dari nol. Beberapa insight penting:

- **Configuration sequence matters:** Harus setup DHCP dulu sebelum wireless agar client bisa auto-assign IP
- **Security layering:** Password router + WPA2 passphrase = defense in depth
- **Wireless convergence:** Perlu patience saat connect wireless devices, tidak instant seperti wired
- **Web testing lebih comprehensive:** Ping hanya test connectivity, web test membuktikan full stack working
- **Documentation is key:** Screenshot setiap step memudahkan troubleshooting dan learning review

Lab ini menjadi foundation penting untuk memahami network security concepts di level yang lebih kompleks nanti.
