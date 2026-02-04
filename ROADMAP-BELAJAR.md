# 🗺️ Roadmap Belajar Cisco Networking Basics
## Untuk Persiapan Magang Cybersecurity

**Dibuat:** Januari 2026  
**Tujuan:** Menguasai dasar networking untuk cybersecurity  
**Status:** 🏆 **COURSE COMPLETED - 03 Februari 2026**

---

## 📊 Peta Prioritas Modul

### 🔴 WAJIB PAHAM BANGET (Ulangi sampai hafal!)

| Modul | Topik | Kenapa Penting untuk CyberSec |
|-------|-------|-------------------------------|
| **5** | OSI & TCP/IP Model | Dasar analisis serangan per layer |
| **8** | IPv4 Structure & Subnetting | Firewall rules, network scanning |
| **9** | Unicast/Broadcast/Multicast + Private IP | Network enumeration, segmentation |
| **15** | TCP & UDP, Port Numbers, Sockets | Protocol analysis, port scanning, netstat |

**Tanda kamu sudah paham:**
- [ ] Bisa jelaskan 7 layer OSI tanpa lihat catatan
- [ ] Bisa hitung network address dari IP + subnet mask
- [ ] Bisa bedakan private IP vs public IP langsung
- [ ] Tahu kenapa broadcast berbahaya untuk security
- [ ] Bisa jelaskan perbedaan TCP vs UDP dan kapan pakai masing-masing
- [ ] Hafal well-known ports (21, 22, 23, 25, 53, 80, 443)

---

### 🟡 HARUS PAHAM KONSEP (Review 2-3x)

| Modul | Topik | Kenapa Penting untuk CyberSec |
|-------|-------|-------------------------------|
| **13** | MAC & IP Addresses, ARP | ARP spoofing, MITM attacks |
| **14** | Routing Between Networks | Network segmentation, routing attacks |
| **16** | Application Layer (DNS, HTTP, FTP, SSH) | Application-layer attacks, service exploitation |
| **11** | DHCP (Dynamic Addressing) | DHCP starvation, rogue DHCP server |
| **10** | IPv6 Addressing & Format | Dual stack, tunneling attacks, IPv6 recon |
| **7** | Switch & MAC Address Table | MAC flooding, ARP spoofing |
| **3** | Wireless Security (WEP/WPA/WPA2) | Wireless hacking, evil twin |

**Tanda kamu sudah paham:**
- [ ] Bisa jelaskan proses DORA pada DHCP
- [ ] Bisa jelaskan cara switch belajar MAC address
- [ ] Tahu perbedaan WEP vs WPA vs WPA2 vs WPA3
- [ ] Paham kenapa hub lebih tidak aman dari switch
- [ ] Bisa jelaskan proses ARP dan kenapa bisa di-spoofing
- [ ] Paham perbedaan router vs switch (Layer 3 vs Layer 2)
- [ ] Tahu kenapa SSH lebih aman dari Telnet
- [ ] Bisa jelaskan proses DNS resolution

---

### 🟢 CUKUP PAHAM DASAR (Baca 1x, review kalau perlu)

| Modul | Topik | Catatan |
|-------|-------|---------|
| **2** | Client-Server, Network Devices | Konsep dasar, tidak terlalu kritis |
| **4** | Home Network Setup | Berguna untuk lab, bukan untuk interview |
| **6** | Network Media (Kabel) | Physical security, jarang ditanya |

---

### ⚪ AMAN KALAU TIDAK TERLALU PAHAM

| Modul | Topik | Catatan |
|-------|-------|---------|
| **1** | Intro (PAN/LAN/WAN) | Sangat basic, pasti sudah paham |

---

## 📚 Modul Tambahan yang WAJIB Dipelajari

Ini topik yang **TIDAK ADA di Cisco Networking Basics** tapi **WAJIB untuk CyberSec**:

| Topik | File | Status | Prioritas |
|-------|------|--------|-----------|
| TCP/UDP & 3-Way Handshake | `tambahan-modul-05.md` | ✅ Selesai | 🔴 WAJIB |
| Common Ports | `tambahan-modul-05.md` | ✅ Selesai | 🔴 WAJIB |
| ARP Protocol & ARP Spoofing | `tambahan-modul-07.md` | ✅ Selesai | 🔴 WAJIB |
| DHCP Process (DORA) | `tambahan-modul-09.md` | ✅ Selesai | 🟡 PENTING |
| DNS & DNS Attacks | `tambahan-dns.md` | ✅ Selesai | 🟡 PENTING |

---

## 📅 Jadwal Belajar yang Disarankan

### Minggu 1: Foundation (Modul Utama)
| Hari | Aktivitas | Durasi |
|------|-----------|--------|
| 1-2 | Review **Modul 5** (OSI/TCP-IP) + Tambahan TCP/UDP | 2-3 jam |
| 3-4 | Review **Modul 8** (IPv4) + Latihan subnetting | 2-3 jam |
| 5-6 | Review **Modul 9** (Transmission types, Private IP) | 2 jam |
| 7 | **QUIZ DIRI SENDIRI** - tanpa buka catatan | 1 jam |

### Minggu 2: Intermediate
| Hari | Aktivitas | Durasi |
|------|-----------|--------|
| 1-2 | Review **Modul 7** (Switch/MAC) + Tambahan ARP | 2 jam |
| 3-4 | Review **Modul 3** (Wireless) + Wireless attacks | 2 jam |
| 5-6 | Pelajari **DHCP & DNS** dari modul tambahan | 2 jam |
| 7 | **QUIZ DIRI SENDIRI** | 1 jam |

### Minggu 3: Modul Lanjutan Cisco (10-17)
- Kirim konten Inggris → dapat terjemahan Indonesia
- Fokus pada modul yang relevan untuk security

### Minggu 4: Review & Practice
- Review semua modul
- Latihan dengan TryHackMe "Pre-Security" path
- Simulasi pertanyaan interview

---

## ✅ Checklist Sebelum Interview

### Konsep yang HARUS bisa dijelaskan:

**Networking Basics:**
- [ ] Apa itu OSI model? Jelaskan 7 layer
- [ ] Apa bedanya TCP dan UDP?
- [ ] Apa itu subnet mask? Cara pakainya?
- [ ] Apa bedanya private IP dan public IP?
- [ ] Bagaimana switch bekerja?
- [ ] Apa itu broadcast domain?

**Security Context:**
- [ ] Serangan apa yang bisa terjadi di Layer 2? (ARP spoofing, MAC flooding)
- [ ] Kenapa broadcast bisa berbahaya?
- [ ] Kenapa WEP tidak aman?
- [ ] Apa itu port? Sebutkan 5 port penting dan fungsinya

**Practical:**
- [ ] Bisa baca output `ipconfig` / `ifconfig`
- [ ] Tahu cara pakai `ping` dan `traceroute`
- [ ] Paham dasar Wireshark (baca packet)

---

## 🎯 Tips Belajar Efektif

### 1. Jangan Cuma Baca, Praktekkan!
```
❌ Baca → Lupa
✅ Baca → Tulis ulang → Jelaskan ke orang lain → Praktek
```

### 2. Gunakan Packet Tracer
Kamu sudah punya lab Packet Tracer! Gunakan untuk:
- Lihat cara broadcast menyebar
- Lihat MAC address table di switch
- Simulasi network scanning

### 3. Test Diri Sendiri
Setiap selesai 1 modul, tutup catatan dan jawab:
- Apa 3 poin penting dari modul ini?
- Bagaimana ini relevan untuk cybersecurity?
- Bisa jelaskan ke orang awam?

### 4. Fokus "WHY" bukan cuma "WHAT"
```
❌ "Broadcast address = 255.255.255.255"
✅ "Broadcast address = 255.255.255.255, dan ini bisa dieksploitasi 
    untuk network discovery atau amplification attack"
```

---

## 📈 Progress Tracker

### Modul Utama (1-9)
| Modul | Status | Pemahaman | Terakhir Review |
|-------|--------|-----------|-----------------|
| 1 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 2 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 3 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 4 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 5 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 6 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 7 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 8 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 9 | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |

**Cara isi pemahaman:** ⬛⬛⬛⬛⬛ = 100% paham

### Modul Lanjutan (10-17)
| Modul | Topik | Status | Pemahaman | Terakhir Review |
|-------|-------|--------|-----------|-----------------|
| 10 | IPv6 Addressing | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 11 | Dynamic Addressing (DHCP) | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 12 | Gateways to Other Networks | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 13 | The ARP Process | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 14 | Routing Between Networks | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 15 | TCP and UDP | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 16 | Application Layer Services | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |
| 17 | Network Testing Utilities | ✅ Selesai | ⬜⬜⬜⬜⬜ | - |

### Modul Tambahan
| Topik | File | Pemahaman |
|-------|------|-----------|
| TCP/UDP & Ports | `tambahan-modul-05.md` | ⬜⬜⬜⬜⬜ |
| ARP Protocol | `tambahan-modul-07.md` | ⬜⬜⬜⬜⬜ |
| DHCP (DORA) | `tambahan-modul-09.md` | ⬜⬜⬜⬜⬜ |
| DNS | `tambahan-dns.md` | ⬜⬜⬜⬜⬜ |

---

## 🚀 Next Steps

### 🏆 Course Completed! (03 Feb 2026)

1. **Review:** Ulangi modul prioritas 🔴 untuk persiapan interview
2. **Practice:** Lanjut ke TryHackMe "Pre-Security" path
3. **Hands-on:** Praktik dengan Wireshark untuk packet analysis
4. **Target:** Apply cybersecurity internship (Mid-2026)

### Rekomendasi Course Selanjutnya:
- Cisco CyberOps Associate
- CompTIA Security+ (Study)
- TryHackMe Pre-Security Path

---

*"Networking adalah fondasi cybersecurity."*

🎉 **Selamat! Kamu sudah menyelesaikan Cisco Networking Basics!**
