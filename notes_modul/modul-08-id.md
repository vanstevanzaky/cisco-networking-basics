# Modul 8: The Internet Protocol

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 8.1 Purpose of an IPv4 Address

### 8.1.1 The IPv4 Address

**Mengapa butuh IPv4?**
- Host membutuhkan IPv4 address untuk **berpartisipasi di internet** dan hampir semua LAN
- IPv4 adalah **logical network address** yang mengidentifikasi host tertentu

**Syarat IPv4 Address:**
| Komunikasi | Syarat |
|------------|--------|
| **Lokal (LAN)** | Harus dikonfigurasi dengan benar dan **unik dalam LAN** |
| **Remote (Internet)** | Harus dikonfigurasi dengan benar dan **unik di dunia** |

**Di mana IPv4 di-assign?**
- Ke **network interface connection** (biasanya NIC - Network Interface Card)
- Contoh device dengan NIC: workstation, server, network printer, IP phone
- Server bisa punya lebih dari satu NIC, masing-masing punya IPv4 sendiri
- Router interface juga punya IPv4 address

**Setiap packet di internet punya:**
- **Source IPv4 address** - alamat pengirim
- **Destination IPv4 address** - alamat tujuan

Informasi ini diperlukan agar data sampai ke tujuan dan reply kembali ke source.

---

### 8.1.2 Octets and Dotted-Decimal Notation

**IPv4 = 32 bits**

```
Binary:     11010001101001011100100000000001
            (sulit dibaca!)
```

**Dibagi menjadi 4 oktet (masing-masing 8 bit):**
```
Binary:     11010001.10100101.11001000.00000001
            (masih sulit)
```

**Dikonversi ke Dotted-Decimal:**
```
Decimal:    209.165.200.1
            (mudah dibaca!)
```

**Kesimpulan:**
- 32 bit → dibagi 4 oktet → setiap oktet dikonversi ke decimal (0-255)
- Format penulisan: **dotted-decimal notation** (dipisah titik)

---

## 📚 8.2 The IPv4 Address Structure

### 8.2.2 Networks and Hosts

**IPv4 address terdiri dari 2 bagian (hierarchical):**

| Bagian | Fungsi |
|--------|--------|
| **Network Portion** | Identifikasi jaringan |
| **Host Portion** | Identifikasi device dalam jaringan |

**Contoh:**
```
IPv4 Address: 192.168.5.11
Subnet Mask:  255.255.255.0

Network Portion: 192.168.5   (3 oktet pertama)
Host Portion:    .11         (oktet terakhir)
```

**Subnet Mask:**
- Digunakan untuk **mengidentifikasi network** tempat host terhubung
- Menentukan mana network portion, mana host portion

---

### Hierarchical Addressing

**Konsep:**
- Network portion menunjukkan **network mana** host berada
- Router hanya perlu tahu cara reach **setiap network**, bukan setiap individual host

**Analogi:** Seperti sistem telepon
- Country code + area code + exchange = network address
- Remaining digits = local phone number (host)

---

### Multiple Logical Networks

**Satu physical network bisa punya multiple logical networks:**

```
Physical Network (1 LAN)
├── Logical Network 1: 192.168.18.0
│   ├── 192.168.18.11
│   ├── 192.168.18.22
│   └── 192.168.18.33
│
└── Logical Network 2: 192.168.5.0
    ├── 192.168.5.11
    ├── 192.168.5.22
    └── 192.168.5.33
```

**Aturan komunikasi:**
- Host dengan **network number SAMA** → bisa komunikasi langsung
- Host dengan **network number BERBEDA** → butuh **routing**

---

## 📝 Quiz Summary (8.2.3)

**Cara menentukan network address:**
- Lihat subnet mask untuk tahu berapa oktet = network portion
- Host portion diganti dengan **0**

| IP Address | Subnet Mask | Network Address |
|------------|-------------|-----------------|
| 10.5.4.100 | 255.255.255.0 | **10.5.4.0** |
| 172.16.4.100 | 255.255.0.0 | **172.16.0.0** |
| 192.168.1.50 | 255.255.255.0 | **192.168.1.0** |

**Host di network yang sama:**
- Network portion harus **identik**
- Contoh: 10.5.4.100 dan 10.5.4.99 → SAMA (network 10.5.4.0)
- Contoh: 10.5.4.100 dan 10.5.0.1 → BEDA (network berbeda)

---

## 💡 Poin Penting

1. **IPv4 = 32 bit**, ditulis dalam **dotted-decimal** (4 oktet)
2. **IPv4 harus unik** - lokal untuk LAN, global untuk Internet
3. IPv4 di-assign ke **NIC** (Network Interface Card)
4. Setiap packet punya **source IP** dan **destination IP**
5. IPv4 terdiri dari **network portion** + **host portion**
6. **Subnet mask** menentukan pembagian network/host
7. Host dengan **network portion sama** bisa komunikasi langsung
8. Host dengan **network portion berbeda** butuh **router**

---

**Konsep Terkait:** Access Layer (Modul 7), DHCP (Modul 11), Routing (Modul 14)
