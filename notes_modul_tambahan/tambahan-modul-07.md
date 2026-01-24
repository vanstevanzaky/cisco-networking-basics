# Tambahan Modul 7: Switch, MAC Address & ARP

**Pelengkap:** Modul 7 - Access Layer  
**Fokus:** Materi yang WAJIB untuk Cybersecurity  
**Status:** ✅ Selesai

---

## 📌 Ringkasan Konsep Utama

### Switch vs Hub = Kurir Pintar vs Tukang Teriak

**Hub (Zaman Dulu):**
```
Ada surat untuk Rumah 5

Hub: "ADA SURAT UNTUK RUMAH 5!!!" (teriak ke semua)

Rumah 1: "Bukan saya" ❌
Rumah 2: "Bukan saya" ❌
Rumah 3: "Bukan saya" ❌
Rumah 5: "Oh untuk saya!" ✅

TIDAK EFISIEN! Semua orang terganggu!
```

**Switch (Sekarang):**
```
Ada surat untuk Rumah 5

Switch: *cek daftar* "Rumah 5 di port 3"
        *kirim langsung ke port 3*

Rumah lain tidak tahu ada surat
Lebih efisien
```

### MAC Address = Nomor KTP (Permanen)

```
IP Address  = Alamat rumah (bisa pindah)
MAC Address = Nomor KTP (permanen dari lahir)

Contoh MAC: AA:BB:CC:11:22:33
- Diberikan dari PABRIK
- Tidak bisa diubah
- Unik di seluruh dunia

Lihat MAC kamu: ipconfig /all (Windows)
```

### Switch Belajar dari SIAPA YANG KIRIM

```
PC-A kirim data dari Port 1
Switch: "Oh, PC-A (MAC: AA:AA:AA) ada di Port 1!"
        *catat di tabel*

Lain kali ada yang cari AA:AA:AA?
Switch sudah tahu: "Kirim ke Port 1!"
```

### ARP = Tanya Alamat

```
Komputer tahu IP tujuan: 192.168.1.20
Tapi tidak tahu MAC-nya!

Komputer: "SIAPA YANG PUNYA IP 192.168.1.20?" (teriak/broadcast)
PC-B:     "SAYA! MAC saya BB:BB:BB" (jawab)
Komputer: "Oke, dicatat!" (simpan di ARP cache)

Lihat ARP cache: arp -a (Windows/Linux)
```

### ARP Spoofing = Pura-pura Jadi Orang Lain

```
Hacker: "Saya yang punya IP 192.168.1.1!" (BOHONG!)
Korban: "Oh oke, saya catat"
        
Sekarang semua data korban ke gateway...
...malah ke HACKER! 😱

Ini namanya Man-in-the-Middle Attack
```

---

## 📚 Apa itu ARP? (Detail Teknis)

**ARP = Address Resolution Protocol**

### Fungsi Utama:
Menerjemahkan **IP address** menjadi **MAC address**.

### Kenapa Perlu?
- Switch bekerja di **Layer 2** (MAC address)
- Komputer tahu **IP tujuan**, tapi tidak tahu **MAC tujuan**
- ARP menjembatani gap antara Layer 3 (IP) dan Layer 2 (MAC)

---

## 🔄 Cara Kerja ARP

### Skenario:
PC-A (192.168.1.10) ingin kirim data ke PC-B (192.168.1.20)

### Proses:

```
┌──────────────────────────────────────────────────────────────┐
│                        ARP PROCESS                            │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  PC-A                    Switch                    PC-B      │
│  192.168.1.10                                  192.168.1.20  │
│  AA:AA:AA:AA:AA:AA                            BB:BB:BB:BB:BB │
│      │                                              │        │
│      │                                              │        │
│  1.  │──── ARP Request (Broadcast) ────────────────>│        │
│      │   "Siapa punya IP 192.168.1.20?"            │        │
│      │   "MAC saya AA:AA:AA:AA:AA:AA"              │        │
│      │                                              │        │
│  2.  │<─────────── ARP Reply (Unicast) ─────────────│        │
│      │   "Saya 192.168.1.20"                        │        │
│      │   "MAC saya BB:BB:BB:BB:BB:BB"              │        │
│      │                                              │        │
│  3.  │  [Simpan di ARP Cache]                       │        │
│      │  192.168.1.20 = BB:BB:BB:BB:BB:BB           │        │
│      │                                              │        │
│  4.  │═══════════ DATA TRANSFER ═══════════════════>│        │
│      │                                              │        │
└──────────────────────────────────────────────────────────────┘
```

### Langkah-langkah:

1. **ARP Request (Broadcast)**
   - PC-A kirim broadcast: "Siapa punya IP 192.168.1.20?"
   - Dikirim ke **semua device** dalam jaringan

2. **ARP Reply (Unicast)**
   - PC-B yang punya IP tersebut menjawab
   - "Saya! MAC address saya BB:BB:BB:BB:BB:BB"

3. **ARP Cache**
   - PC-A simpan mapping IP→MAC di tabel ARP
   - Tidak perlu tanya lagi untuk beberapa waktu

4. **Data Transfer**
   - Sekarang PC-A tahu MAC tujuan
   - Data bisa dikirim

---

## 📋 ARP Cache / ARP Table

### Melihat ARP Table:

**Windows:**
```cmd
arp -a
```

**Linux/Mac:**
```bash
arp -n
```

### Contoh Output:
```
Interface: 192.168.1.10
  Internet Address      Physical Address      Type
  192.168.1.1           00-1A-2B-3C-4D-5E     dynamic
  192.168.1.20          BB-BB-BB-BB-BB-BB     dynamic
  192.168.1.255         ff-ff-ff-ff-ff-ff     static
```

### Tipe Entry:
| Type | Artinya |
|------|---------|
| **Dynamic** | Dipelajari via ARP, expire setelah timeout |
| **Static** | Dikonfigurasi manual, tidak expire |

---

## 🔴 ARP Spoofing / ARP Poisoning

### Apa itu?
**Serangan** di mana attacker mengirim **ARP Reply palsu** untuk mengasosiasikan **MAC attacker** dengan **IP korban/gateway**.

### Kenapa Bisa Terjadi?
- ARP **TIDAK ADA AUTENTIKASI**
- Siapa saja bisa kirim ARP Reply
- Device akan percaya ARP Reply tanpa verifikasi

---

### Skenario Attack: Man-in-the-Middle (MITM)

```
┌────────────────────────────────────────────────────────────────┐
│                    ARP SPOOFING ATTACK                         │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│   Victim                Attacker               Gateway         │
│   192.168.1.10         192.168.1.50           192.168.1.1      │
│   (AA:AA)              (CC:CC) ☠️              (GG:GG)          │
│       │                    │                      │            │
│       │                    │                      │            │
│  1.   │<── Fake ARP Reply ─┤                      │            │
│       │  "192.168.1.1 =    │                      │            │
│       │   MAC CC:CC" 🔴    │                      │            │
│       │                    │                      │            │
│  2.   │                    ├── Fake ARP Reply ───>│            │
│       │                    │  "192.168.1.10 =     │            │
│       │                    │   MAC CC:CC" 🔴      │            │
│       │                    │                      │            │
│       │                    │                      │            │
│  3.   │═══ Traffic ═══════>│═══════════════════>│            │
│       │    (via attacker!)  │                      │            │
│       │                    │                      │            │
│       │     ATTACKER BISA LIHAT SEMUA DATA! ☠️    │            │
│       │                                                        │
└────────────────────────────────────────────────────────────────┘
```

### Langkah Attack:

1. **Poison Victim's ARP Cache**
   - Attacker kirim ke Victim: "Gateway (192.168.1.1) punya MAC CC:CC (attacker)"
   - Victim percaya dan update ARP cache

2. **Poison Gateway's ARP Cache**
   - Attacker kirim ke Gateway: "Victim (192.168.1.10) punya MAC CC:CC (attacker)"
   - Gateway percaya dan update ARP cache

3. **Man-in-the-Middle**
   - Semua traffic antara Victim ↔ Gateway melewati Attacker
   - Attacker bisa:
     - **Sniff** (baca semua data)
     - **Modify** (ubah data)
     - **Drop** (block traffic)

---

## 🛡️ Cara Mencegah ARP Spoofing

### 1. Static ARP Entries
```cmd
# Windows - tambah static ARP
arp -s 192.168.1.1 00-1A-2B-3C-4D-5E
```
**Kekurangan:** Tidak praktis untuk jaringan besar

### 2. Dynamic ARP Inspection (DAI)
- Fitur di **managed switch**
- Switch memverifikasi ARP packets
- Drop ARP yang tidak valid

### 3. VLAN Segmentation
- Pisahkan network sensitif
- ARP spoofing hanya work di **broadcast domain yang sama**

### 4. Use Encryption
- **HTTPS** instead of HTTP
- **SSH** instead of Telnet
- Attacker bisa lihat traffic, tapi tidak bisa baca

### 5. ARP Monitoring Tools
- **arpwatch** (Linux)
- **XArp** (Windows)
- Detect perubahan ARP yang mencurigakan

---

## 🔧 Tools untuk ARP Attack (Educational)

| Tool | Platform | Fungsi |
|------|----------|--------|
| **arpspoof** | Linux | ARP spoofing |
| **ettercap** | Linux/Windows | MITM framework |
| **Cain & Abel** | Windows | ARP poisoning + password sniffing |
| **bettercap** | Linux | Modern MITM tool |

**⚠️ WARNING:** Hanya gunakan di lab sendiri atau dengan izin!

---

## 🔴 ARP-Related Attacks

### 1. ARP Spoofing / Poisoning
- MITM attack
- Sudah dijelaskan di atas

### 2. ARP Flood / MAC Flooding
```
Attacker kirim ribuan ARP dengan MAC random
→ Switch MAC table penuh
→ Switch jadi seperti hub (broadcast semua)
→ Attacker bisa sniff semua traffic
```

### 3. ARP Cache Poisoning untuk DoS
```
Attacker poison ARP cache victim
→ Arahkan ke MAC yang tidak ada
→ Victim tidak bisa komunikasi
→ Denial of Service
```

---

## 💡 Poin Penting

1. **ARP** = IP address → MAC address translation
2. **ARP Request** = Broadcast ("Siapa punya IP ini?")
3. **ARP Reply** = Unicast ("Saya! Ini MAC saya")
4. **ARP Cache** = Tabel mapping IP→MAC (lihat dengan `arp -a`)
5. **ARP TIDAK ADA AUTENTIKASI** = Vulnerability!
6. **ARP Spoofing** = Kirim fake ARP reply → MITM attack
7. **Defense:** Static ARP, DAI, VLAN, Encryption

---

## 📝 Quick Reference

```
┌─────────────────────────────────────┐
│           ARP CHEAT SHEET           │
├─────────────────────────────────────┤
│ Lihat ARP table:  arp -a            │
│ Clear ARP cache:  arp -d *          │
│ Add static:       arp -s IP MAC     │
├─────────────────────────────────────┤
│         ARP ATTACK CHAIN            │
│  1. Send fake ARP replies           │
│  2. Poison victim's ARP cache       │
│  3. Become man-in-the-middle        │
│  4. Sniff/modify traffic            │
├─────────────────────────────────────┤
│           PREVENTION                │
│  • Dynamic ARP Inspection (DAI)     │
│  • Static ARP entries               │
│  • VLAN segmentation                │
│  • Use encryption (HTTPS, SSH)      │
└─────────────────────────────────────┘
```

---

**Terkait:** Modul 7 (Switch/MAC), Modul 9 (Broadcast Domain)
