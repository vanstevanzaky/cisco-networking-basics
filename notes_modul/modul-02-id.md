# Modul 2: Network Components, Types, and Connections

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Konsep Inti

### 1. Client dan Server

| Peran | Fungsi | Contoh |
|-------|--------|--------|
| **Client** | Meminta layanan | Web browser, email client |
| **Server** | Menyediakan layanan | Web server, DNS server |
| **Peer** | Client + Server sekaligus | File sharing P2P |

**Model Jaringan:**
- **Client-Server** - server dedicated, scalable, secure
- **Peer-to-Peer (P2P)** - sederhana, tidak scalable, less secure

### 2. Komponen Jaringan

**Network Interface Card (NIC):**
- Menghubungkan device ke jaringan
- Memiliki MAC address (identitas hardware)

**Port & Interface:**
- **Physical port** - RJ-45, fiber connector
- **Interface** - titik koneksi pada device jaringan

**Kabel:**
- **Straight-through** - device berbeda (PC↔Switch)
- **Crossover** - device sejenis (PC↔PC, Switch↔Switch)
- **Rollover/Console** - konfigurasi router/switch

---

## 🔄 Network Devices

### Switch
- Layer 2 (Data Link)
- Forward frame berdasarkan MAC address
- Membuat collision domain terpisah per port

### Router
- Layer 3 (Network)
- Forward packet berdasarkan IP address
- Menghubungkan jaringan berbeda
- Menentukan best path

### Wireless Access Point (AP)
- Menghubungkan wireless client ke wired network
- Bridge antara wireless ↔ wired

### Firewall
- Filter traffic berdasarkan rules
- Stateful vs Stateless inspection
- Protect internal network

---

## 📊 Topologi Jaringan

| Topologi | Kelebihan | Kekurangan |
|----------|-----------|------------|
| **Star** | Mudah troubleshoot, 1 fail tidak affect lain | Central point of failure |
| **Bus** | Murah, sederhana | 1 break = semua down |
| **Ring** | Equal access | 1 fail = network down |
| **Mesh** | Redundant, reliable | Mahal, kompleks |

**Modern LAN:** Umumnya menggunakan **Star topology** dengan switch sebagai pusat

---

## 💡 Poin Penting

1. **Client meminta, Server menyediakan** layanan
2. **NIC** memiliki MAC address unik
3. **Switch = Layer 2 (MAC)**, **Router = Layer 3 (IP)**
4. **Star topology** paling umum di LAN modern
5. **Straight-through** untuk device berbeda, **crossover** untuk sejenis

---

**Konsep Terkait:** Wireless Networks (Modul 3), Access Layer (Modul 7)
