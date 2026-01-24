# Modul 10: IPv6 Addressing Formats and Rules

**Judul:** IPv6 Addressing Formats and Rules  
**Tujuan:** Menjelaskan fitur-fitur dari IPv6 addressing  
**Status:** ✅ Selesai

---

## 📌 Ringkasan Konsep Utama

### IPv6 = Apartemen Baru dengan Banyak Unit

```
IPv4 = Perumahan lama dengan 4.3 miliar rumah
      Sekarang PENUH! Tidak ada rumah kosong!

IPv6 = Apartemen super besar dengan 340 undecillion unit
      (340 diikuti 36 angka 0)
      
Analogi: Setiap butir pasir di bumi bisa punya alamat sendiri
```

### Kenapa Perlu IPv6?

```
🏠 IPv4 habis (4.3 miliar alamat saja)
📱 Smartphone makin banyak
🚗 Mobil pintar butuh IP
🏠 Smart home, IoT devices
⌚ Smartwatch, smart TV

Semua butuh alamat internet!
```

### Format IPv6 = 8 Kelompok Hexadecimal

```
IPv4: 192.168.1.1 (4 bagian, angka 0-255)
IPv6: 2001:0db8:0000:1111:0000:0000:0000:0200 (8 bagian, hex 0-F)

Hexadecimal = 0 1 2 3 4 5 6 7 8 9 A B C D E F
```

### 2 Aturan Mempersingkat IPv6

```
Aturan 1: Buang 0 di depan
2001:0db8:0000:1111 → 2001:db8:0:1111

Aturan 2: Ganti 0000:0000 dengan ::
2001:db8:0:1111:0:0:0:200 → 2001:db8:0:1111::200

:: hanya boleh dipakai SEKALI per alamat!
```

---

## 📚 10.1 IPv4 Issues (Masalah IPv4)

### 10.1.1 Kebutuhan IPv6

**Mengapa IPv4 Habis?**
- IPv4 maksimal: **4.3 miliar alamat**
- Perangkat internet terus bertambah
- 4 dari 5 RIR (Regional Internet Registry) sudah kehabisan IPv4

**Tanggal Kehabisan IPv4 per Region:**
| Region | Tanggal Habis |
|--------|--------------|
| LACNIC | April 2011 |
| RIPE NCC | September 2012 |
| APNIC | Juni 2014 |
| ARIN | Juli 2015 |
| AfriNIC | 2020 |

**Kelebihan IPv6:**
- **128-bit address space** (vs IPv4 32-bit)
- **340 undecillion** alamat yang tersedia
- **ICMPv6** dengan address resolution dan autoconfiguration
- Tidak perlu NAT (mengurangi latency)
- Mendukung peer-to-peer communication lebih baik

**Internet of Things (IoT):**
```
Bukan hanya komputer yang butuh IP:
🚗 Mobil pintar
🏥 Perangkat medis
🏠 Smart home devices
🌿 Sensor ekosistem
⌚ Wearable devices
```

**Statistik Adopsi:**
- Provider mobile AS: >90% traffic IPv6
- Comcast (2018): 65% deployment
- British Sky: 86% deployment

---

### 10.1.2 Koeksistensi IPv4 dan IPv6

Tidak ada tanggal pasti untuk migrasi ke IPv6. **Keduanya akan berjalan bersamaan bertahun-tahun.**

**3 Metode Transisi:**

#### 1. **Dual Stack** (Recommended)
```
Device menjalankan IPv4 DAN IPv6 bersamaan
┌─────────────┐
│   Device    │
│ IPv4 + IPv6 │ ← Native IPv6
│   Stack     │
└─────────────┘
```

#### 2. **Tunneling**
```
IPv6 packet "dibungkus" dalam IPv4 packet

IPv6-only ←→ [Dual Stack Router] ←→ IPv4-only ←→ [Dual Stack Router] ←→ IPv6-only
              │                                │
              └─── IPv6 over IPv4 Tunnel ────┘
```

#### 3. **Translation (NAT64)**
```
Translasi antara IPv6 ↔ IPv4

IPv6-only Network ←→ [NAT64 Router] ←→ IPv4-only Network
```

**⚠️ Catatan:** Tunneling dan Translation hanya untuk transisi. Tujuan akhir adalah **native IPv6** end-to-end.

---

## 📚 10.2 IPv6 Addressing (Pengalamatan IPv6)

### 10.2.1 Hexadecimal Number System

IPv6 menggunakan **base 16 (hexadecimal):**
```
Decimal:     0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
Hexadecimal: 0 1 2 3 4 5 6 7 8 9  A  B  C  D  E  F
```

### 10.2.2 Format Alamat IPv6

**Struktur Dasar:**
- **128-bit** total length
- Ditulis dalam **hexadecimal**
- Terbagi menjadi **8 hextet** (16-bit segments)
- Format: `x:x:x:x:x:x:x:x`
- Setiap "x" = 4 digit hexadecimal = 16 bit = 1 hextet

**Contoh Preferred Format:**
```
2001:0db8:0000:1111:0000:0000:0000:0200
2001:0db8:0000:00a3:abcd:0000:0000:1234
fe80:0000:0000:0000:0123:4567:89ab:cdef
```

**Terminologi:**
- **Octet** (IPv4) = 8 bits
- **Hextet** (IPv6) = 16 bits = 4 hex digits

---

### 10.2.4 Rule 1 – Omit Leading Zeros

**Aturan:** Buang angka 0 di **depan** setiap hextet.

```
Before: 01ab → After: 1ab
Before: 09f0 → After: 9f0
Before: 0a00 → After: a00
Before: 00ab → After: ab
```

**⚠️ Penting:** Hanya buang 0 di depan, BUKAN di belakang!
```
✅ Benar:  "abc0" tetap "abc0"
❌ Salah:  "abc0" jadi "abc" (ini mengubah nilai!)
```

**Contoh Lengkap:**
```
Before: 2001:0db8:0000:1111:0000:0000:0000:0200
After:  2001:db8:0:1111:0:0:0:200
```

---

### 10.2.5 Rule 2 – Double Colon

**Aturan:** Double colon `::` dapat menggantikan **satu atau lebih hextet berisi 0000**.

```
Before: 2001:db8:0:1111:0:0:0:200
After:  2001:db8:0:1111::200

Before: 2001:db8:0000:0000:0000:0000:0000:1234
After:  2001:db8::1234
```

**⚠️ ATURAN PENTING:**
- `::` hanya boleh digunakan **SEKALI** dalam satu alamat
- Jika tidak, alamat menjadi ambiguous

**Contoh Salah:**
```
❌ 2001:db8::abcd::1234
   
Bisa jadi:
- 2001:db8:abcd:0000:0000:0000:0000:1234
- 2001:db8:0000:0000:abcd:0000:0000:1234  
- 2001:db8:0000:0000:0000:abcd:0000:1234
(Tidak jelas yang mana!)
```

**Best Practice untuk Multiple Zero Groups:**
- Gunakan `::` untuk **grup 0000 terpanjang**
- Jika sama panjang, gunakan untuk **grup pertama**

**Contoh Kompresi Maksimal:**
```
Full:        2001:0db8:0000:0000:0000:0000:0000:0001
Rule 1:      2001:db8:0:0:0:0:0:1
Rule 2:      2001:db8::1
```

---

## 🔍 Contoh Praktis

### Format Alamat IPv6:

| Format | Contoh |
|--------|--------|
| **Full Format** | `2001:0db8:0000:1111:0000:0000:0000:0200` |
| **Leading Zeros Omitted** | `2001:db8:0:1111:0:0:0:200` |
| **Compressed** | `2001:db8:0:1111::200` |

### Alamat IPv6 Khusus:

```
Loopback:     ::1
             (sama seperti 127.0.0.1 di IPv4)

Unspecified:  ::
             (sama seperti 0.0.0.0 di IPv4)

Link-Local:   fe80::/10
             (untuk komunikasi local segment)
```

---

## 💡 Poin Penting

1. **IPv4 habis** → Perlu IPv6 untuk IoT dan pertumbuhan internet
2. **IPv6 = 128-bit** vs IPv4 32-bit
3. **340 undecillion alamat** yang tersedia
4. **Coexistence:** Dual Stack, Tunneling, Translation
5. **Hexadecimal:** 0-9, A-F
6. **8 hextet** masing-masing 16-bit
7. **Rule 1:** Buang leading zeros
8. **Rule 2:** `::` untuk consecutive zeros (sekali saja per alamat)
9. **ICMPv6** lebih baik dari ICMPv4
10. **Native IPv6** adalah tujuan akhir

---

## 📝 Quick Reference

```
┌─────────────────────────────────────┐
│         IPv6 CHEAT SHEET            │
├─────────────────────────────────────┤
│  Length: 128-bit                    │
│  Format: x:x:x:x:x:x:x:x             │
│  Base:   Hexadecimal (0-F)          │
│  Hextet: 16-bit = 4 hex digits      │
├─────────────────────────────────────┤
│  Rule 1: Omit Leading Zeros         │
│  01ab → 1ab                         │
│  0000 → 0                           │
├─────────────────────────────────────┤
│  Rule 2: Double Colon              │
│  :0000:0000:0000: → ::             │
│  (Hanya sekali per alamat!)         │
├─────────────────────────────────────┤
│  Transition Methods:                │
│  • Dual Stack (Recommended)        │
│  • Tunneling                       │
│  • Translation (NAT64)             │
├─────────────────────────────────────┤
│  Special Addresses:                 │
│  Loopback:   ::1                    │
│  Unspecified: ::                    │
│  Link-Local: fe80::/10              │
└─────────────────────────────────────┘
```

---

**Terkait:** Modul 8 (IPv4), Modul 9 (Network Addressing), Modul 11 (Dynamic Addressing)