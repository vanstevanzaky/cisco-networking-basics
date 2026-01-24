# Modul 8: Internet Protocol

**Modul:** 8 - The Internet Protocol  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **IPv4 = 32 bit**, ditulis dalam dotted-decimal (4 oktet, 0-255)
- IPv4 terdiri dari **network portion** + **host portion**
- **Subnet mask** menentukan pembagian network/host
- Host dengan network portion sama bisa komunikasi langsung, berbeda butuh router

---

## 📚 Materi

### 1. IPv4 Address

**Format:** 32 bit → 4 oktet → dotted-decimal

```
Binary:  11010001.10100101.11001000.00000001
Decimal: 209.165.200.1
```

**Syarat IPv4:**

| Komunikasi | Syarat |
|------------|--------|
| Lokal (LAN) | Unik dalam LAN |
| Remote (Internet) | Unik di dunia |

**Di mana IPv4 di-assign:** Network Interface Card (NIC)

**Setiap packet punya:** Source IP + Destination IP

---

### 2. Network vs Host Portion

**IPv4 address terdiri dari 2 bagian:**

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

---

### 3. Subnet Mask

**Fungsi:** Menentukan mana network portion, mana host portion

| IP Address | Subnet Mask | Network Address |
|------------|-------------|-----------------|
| 10.5.4.100 | 255.255.255.0 | 10.5.4.0 |
| 172.16.4.100 | 255.255.0.0 | 172.16.0.0 |
| 192.168.1.50 | 255.255.255.0 | 192.168.1.0 |

---

### 4. Komunikasi Antar Host

| Kondisi | Aksi |
|---------|------|
| Network portion **SAMA** | Komunikasi langsung |
| Network portion **BERBEDA** | Butuh router |

**Contoh:**
- 10.5.4.100 dan 10.5.4.99 → Network sama (10.5.4.0) → Langsung
- 10.5.4.100 dan 10.5.0.1 → Network beda → Butuh router

---

## 💡 Poin Penting

1. **IPv4 = 32 bit**, ditulis dalam dotted-decimal (4 oktet)
2. **IPv4 harus unik** - lokal untuk LAN, global untuk Internet
3. IPv4 di-assign ke **NIC** (Network Interface Card)
4. Setiap packet punya **source IP** dan **destination IP**
5. IPv4 terdiri dari **network portion** + **host portion**
6. **Subnet mask** menentukan pembagian network/host
7. Host dengan **network portion sama** → komunikasi langsung
8. Host dengan **network portion berbeda** → butuh router
