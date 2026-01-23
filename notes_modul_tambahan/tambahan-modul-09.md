# Tambahan Modul 9: DHCP Protocol & DHCP Attacks

**Pelengkap:** Modul 9 - IPv4 Addressing  
**Fokus:** Materi yang WAJIB untuk Cybersecurity  
**Status:** ✅ Selesai

---

## 🎯 Penjelasan Super Simpel (Baca Ini Dulu!)

### DHCP = Resepsionis Hotel

```
Kamu masuk hotel tanpa reservasi...

Kamu:       "Saya mau kamar!" (DHCP Discover)
Resepsionis: "Ada kamar 101, mau?" (DHCP Offer)
Kamu:       "Oke, saya ambil 101!" (DHCP Request)
Resepsionis: "Sip, ini kunci. Check-out 3 hari lagi ya!" (DHCP Ack)

IP = Nomor kamar
Lease Time = Durasi menginap
```

### DORA = 4 Langkah Dapat IP

```
D - Discover  "Halo? Ada DHCP server?" (teriak ke semua)
O - Offer     "Ada! Ini IP untukmu"
R - Request   "Oke saya mau IP itu!"
A - Acknowledge "Setuju! IP ini milikmu 24 jam"
```

### Kenapa IP Bisa Berubah?

```
Hari 1: Laptop kamu dapat IP 192.168.1.10
Hari 3: Lease habis, laptop minta perpanjang
        Kalau DHCP server setuju → IP tetap
        Kalau ada yang pakai → dapat IP baru

Makanya IP laptop kamu bisa beda-beda!
```

### DHCP Starvation Attack = Hacker Booking Semua Kamar

```
Hotel ada 100 kamar...

Hacker kirim 100x "Saya mau kamar!" (pakai MAC palsu)
Semua kamar habis dibooking hacker!

Tamu asli datang: "Maaf, kamar penuh" 😢

Ini = Denial of Service (DoS)
```

### DHCP Spoofing = Resepsionis Palsu

```
Ada resepsionis ASLI dan PALSU di lobby...

Tamu: "Saya mau kamar!"
Palsu: "Sini-sini, saya kasih kamar!" (jawab lebih cepat)
       "Gateway kamu = komputer saya ya~"

Semua data tamu lewat hacker!
= Man-in-the-Middle Attack
```

---

## 📚 Apa itu DHCP? (Detail Teknis)

**DHCP = Dynamic Host Configuration Protocol**

### Fungsi Utama:
Memberikan **IP address secara otomatis** ke device yang terhubung ke jaringan.

### Apa yang DHCP berikan?
| Informasi | Contoh |
|-----------|--------|
| **IP Address** | 192.168.1.100 |
| **Subnet Mask** | 255.255.255.0 |
| **Default Gateway** | 192.168.1.1 |
| **DNS Server** | 8.8.8.8 |
| **Lease Time** | 24 jam |

---

## 🔄 DHCP DORA Process

### DORA = Discover, Offer, Request, Acknowledge

```
┌────────────────────────────────────────────────────────────────┐
│                     DHCP DORA PROCESS                          │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│   Client                                         DHCP Server   │
│   (No IP yet)                                    192.168.1.1   │
│       │                                              │         │
│       │                                              │         │
│  D    │────── DHCP DISCOVER (Broadcast) ────────────>│         │
│       │   "Adakah DHCP server di sini?"              │         │
│       │   Src: 0.0.0.0                               │         │
│       │   Dst: 255.255.255.255                       │         │
│       │                                              │         │
│  O    │<───────── DHCP OFFER ────────────────────────│         │
│       │   "Saya ada! Ini tawaran IP untuk kamu:"     │         │
│       │   IP: 192.168.1.100                          │         │
│       │   Subnet: 255.255.255.0                      │         │
│       │   Gateway: 192.168.1.1                       │         │
│       │   DNS: 8.8.8.8                               │         │
│       │                                              │         │
│  R    │────── DHCP REQUEST (Broadcast) ─────────────>│         │
│       │   "Oke, saya mau IP 192.168.1.100"           │         │
│       │   (Broadcast agar server lain tahu)          │         │
│       │                                              │         │
│  A    │<───────── DHCP ACK ──────────────────────────│         │
│       │   "Setuju! IP 192.168.1.100 milikmu"         │         │
│       │   "Lease time: 24 jam"                       │         │
│       │                                              │         │
│       │                                              │         │
│   CLIENT SEKARANG PUNYA IP: 192.168.1.100           │         │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

### Penjelasan Detail:

#### 1. DISCOVER (Client → Broadcast)
- Client belum punya IP (0.0.0.0)
- Kirim broadcast ke 255.255.255.255
- Port: **UDP 67** (server) dan **UDP 68** (client)
- Pesan: "Ada DHCP server di sini?"

#### 2. OFFER (Server → Client)
- DHCP server merespons
- Menawarkan IP address dan konfigurasi
- Bisa ada multiple offer dari multiple server

#### 3. REQUEST (Client → Broadcast)
- Client memilih satu offer
- Broadcast agar semua server tahu pilihan client
- Server lain akan membatalkan offer mereka

#### 4. ACKNOWLEDGE (Server → Client)
- Server konfirmasi
- IP address resmi diberikan
- Lease time mulai dihitung

---

## ⏰ DHCP Lease

### Apa itu Lease?
**Waktu "sewa"** IP address. Setelah habis, client harus renew.

### Lease Lifecycle:

```
┌─────────────────────────────────────────────────────┐
│               DHCP LEASE TIMELINE                   │
├─────────────────────────────────────────────────────┤
│                                                     │
│  0%              50%              87.5%      100%   │
│  │               │                │          │      │
│  ├───────────────┼────────────────┼──────────┤      │
│  │               │                │          │      │
│  Start        T1 Renew        T2 Rebind   Expire   │
│                  │                │          │      │
│               Unicast          Broadcast   Lost    │
│               ke server        ke semua    IP      │
│               yang sama        server              │
│                                                     │
└─────────────────────────────────────────────────────┘
```

| Timer | Waktu | Aksi |
|-------|-------|------|
| **T1 (Renew)** | 50% lease | Client minta perpanjang ke server asal |
| **T2 (Rebind)** | 87.5% lease | Broadcast minta ke server mana saja |
| **Expire** | 100% lease | IP dikembalikan, client harus DORA lagi |

---

## 🔴 DHCP Attacks

### 1. DHCP Starvation Attack

**Apa itu?**
Attacker meminta **semua IP** di pool DHCP, sehingga tidak ada IP tersisa untuk client legitimate.

```
┌────────────────────────────────────────────────────┐
│            DHCP STARVATION ATTACK                  │
├────────────────────────────────────────────────────┤
│                                                    │
│  Attacker             DHCP Server                  │
│      │                    │                        │
│      │── DISCOVER ───────>│  (MAC: AA:AA:AA:01)   │
│      │<── OFFER: 192.168.1.100                     │
│      │── REQUEST ────────>│                        │
│      │<── ACK ────────────│                        │
│      │                    │                        │
│      │── DISCOVER ───────>│  (MAC: AA:AA:AA:02)   │
│      │<── OFFER: 192.168.1.101                     │
│      │── REQUEST ────────>│                        │
│      │<── ACK ────────────│                        │
│      │                    │                        │
│      │     ... ratusan request ...                 │
│      │                    │                        │
│      │── DISCOVER ───────>│  (MAC: AA:AA:AA:FF)   │
│      │<── NO IP AVAILABLE!│                        │
│      │                    │                        │
│   Legitimate Client       │                        │
│      │── DISCOVER ───────>│                        │
│      │    ❌ NO IP FOR YOU │                        │
│                                                    │
└────────────────────────────────────────────────────┘
```

**Cara kerja:**
1. Attacker generate banyak MAC address palsu
2. Kirim DHCP request untuk setiap MAC
3. Pool DHCP habis
4. Client baru tidak dapat IP → **Denial of Service**

**Tools:** `yersinia`, `dhcpstarv`

---

### 2. Rogue DHCP Server Attack

**Apa itu?**
Attacker memasang **DHCP server palsu** yang memberikan konfigurasi berbahaya.

```
┌────────────────────────────────────────────────────┐
│           ROGUE DHCP SERVER ATTACK                 │
├────────────────────────────────────────────────────┤
│                                                    │
│  Victim        Rogue DHCP ☠️      Real DHCP        │
│    │           (Attacker)         (Legit)          │
│    │                │                 │            │
│    │── DISCOVER ───>│<───────────────>│            │
│    │   (Broadcast)  │                 │            │
│    │                │                 │            │
│    │<── OFFER ──────│  (Lebih cepat!) │            │
│    │   Gateway: 192.168.1.50 (Attacker!)           │
│    │   DNS: 10.10.10.10 (Attacker's DNS!)          │
│    │                │                 │            │
│    │── REQUEST ────>│                 │            │
│    │<── ACK ────────│                 │            │
│    │                │                 │            │
│    │                                               │
│    │   Victim sekarang pakai:                      │
│    │   - Gateway ATTACKER → MITM                   │
│    │   - DNS ATTACKER → Phishing redirect          │
│                                                    │
└────────────────────────────────────────────────────┘
```

**Yang bisa attacker lakukan:**
| Setting | Attack |
|---------|--------|
| **Fake Gateway** | Man-in-the-Middle, sniff semua traffic |
| **Fake DNS** | Redirect ke phishing site |
| **Wrong Subnet** | Denial of Service |

---

## 🛡️ DHCP Security (Defense)

### 1. DHCP Snooping
- Fitur di **managed switch**
- Hanya port yang **trusted** boleh jadi DHCP server
- Untrusted port hanya boleh kirim DHCP request

```
Switch Configuration:
├── Port 1: Trusted (ke DHCP server)
├── Port 2-24: Untrusted (ke client)
│
│ Rogue DHCP di Port 5? → BLOCKED!
```

### 2. Port Security
- Batasi jumlah MAC address per port
- Mencegah MAC spoofing untuk DHCP starvation

### 3. Rate Limiting
- Batasi jumlah DHCP request per detik
- Mencegah starvation attack

### 4. Static IP untuk Server/Critical Device
- Device penting tidak bergantung DHCP
- Tidak terpengaruh DHCP attack

### 5. 802.1X Authentication
- Device harus autentikasi sebelum dapat akses
- Unauthorized device tidak bisa melakukan attack

---

## 💻 DHCP Commands

### Windows

```cmd
# Lihat konfigurasi IP
ipconfig /all

# Release IP (kembalikan ke DHCP)
ipconfig /release

# Request IP baru
ipconfig /renew

# Flush DNS cache
ipconfig /flushdns
```

### Linux

```bash
# Lihat konfigurasi IP
ip addr show

# Release dan renew
sudo dhclient -r          # Release
sudo dhclient             # Renew

# Atau dengan interface spesifik
sudo dhclient -r eth0
sudo dhclient eth0
```

---

## 📊 DHCP vs Static IP

| Aspek | DHCP | Static IP |
|-------|------|-----------|
| **Konfigurasi** | Otomatis | Manual |
| **Skalabilitas** | ✅ Mudah | ❌ Sulit untuk banyak device |
| **Maintenance** | ✅ Rendah | ❌ Tinggi |
| **Consistency** | ❌ IP bisa berubah | ✅ IP tetap |
| **Security** | ⚠️ Rentan attack | ✅ Lebih aman |
| **Use Case** | Workstation, Mobile | Server, Printer, Router |

---

## 💡 Poin Penting

1. **DHCP** = Automatic IP assignment
2. **DORA** = Discover → Offer → Request → Acknowledge
3. **Port:** UDP 67 (server), UDP 68 (client)
4. **Lease** = Waktu sewa IP (perlu renew)
5. **DHCP Starvation** = Habiskan semua IP di pool
6. **Rogue DHCP** = DHCP palsu → MITM, DNS redirect
7. **Defense:** DHCP Snooping, Port Security

---

## 📝 Quick Reference

```
┌─────────────────────────────────────┐
│         DHCP CHEAT SHEET            │
├─────────────────────────────────────┤
│  DORA Process:                      │
│  D - Discover (broadcast)           │
│  O - Offer (server responds)        │
│  R - Request (client accepts)       │
│  A - Acknowledge (confirmed!)       │
├─────────────────────────────────────┤
│  Windows Commands:                  │
│  ipconfig /release  - Lepas IP      │
│  ipconfig /renew    - Minta IP baru │
│  ipconfig /all      - Lihat detail  │
├─────────────────────────────────────┤
│  Attacks:                           │
│  • Starvation - Habiskan IP pool    │
│  • Rogue DHCP - Server palsu        │
├─────────────────────────────────────┤
│  Defense:                           │
│  • DHCP Snooping                    │
│  • Port Security                    │
│  • Rate Limiting                    │
└─────────────────────────────────────┘
```

---

**Terkait:** Modul 9 (IPv4 Addressing), Tambahan ARP (Layer 2 Attacks)
