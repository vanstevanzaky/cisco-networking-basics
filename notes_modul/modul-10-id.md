# Modul 10: IPv6 Addressing

**Modul:** 10 - IPv6 Addressing Formats and Rules  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **IPv4 habis** (4.3 miliar), **IPv6** = 340 undecillion alamat
- **IPv6 = 128 bit**, ditulis dalam 8 kelompok hexadecimal
- **2 aturan singkat:** Buang 0 di depan, ganti :0000: dengan ::
- **3 metode transisi:** Dual Stack, Tunneling, Translation

---

## 📚 Materi

### 1. Mengapa Perlu IPv6?

| Aspek | IPv4 | IPv6 |
|-------|------|------|
| Ukuran | 32-bit | 128-bit |
| Total Alamat | 4.3 miliar | 340 undecillion |
| Status | Habis (exhaustion) | Berlimpah |

**Kehabisan IPv4 per Region:**

| Region | Tanggal Habis |
|--------|--------------|
| APNIC | April 2011 |
| RIPE NCC | September 2012 |
| ARIN | Juli 2015 |
| AFRINIC | 2020 |

---

### 2. Format IPv6

**Struktur:** 8 kelompok x 16 bit = 128 bit total

```
Full:    2001:0db8:0000:1111:0000:0000:0000:0200
```

**Aturan Penyingkatan:**

| Aturan | Contoh |
|--------|--------|
| 1. Buang 0 di depan | 0db8 → db8 |
| 2. Ganti :0000: dengan :: | :0:0:0: → :: |

```
Full:       2001:0db8:0000:1111:0000:0000:0000:0200
Singkat:    2001:db8:0:1111::200
```

**Catatan:** :: hanya boleh dipakai **SEKALI** per alamat

---

### 3. Metode Transisi IPv4 ke IPv6

| Metode | Cara Kerja |
|--------|------------|
| **Dual Stack** | Device jalankan IPv4 DAN IPv6 bersamaan (recommended) |
| **Tunneling** | IPv6 packet dibungkus dalam IPv4 packet |
| **Translation** | NAT64 konversi antara IPv4 dan IPv6 |

---

### 4. Kelebihan IPv6

- Address space sangat besar (340 undecillion)
- Tidak perlu NAT
- ICMPv6 dengan autoconfiguration
- Header lebih efisien
- Mendukung peer-to-peer lebih baik

---

## 💡 Poin Penting

1. **IPv4 = 32-bit** (4.3 miliar), **IPv6 = 128-bit** (340 undecillion)
2. IPv6 ditulis dalam **8 kelompok hexadecimal**
3. **Aturan 1:** Buang leading zeros (0db8 → db8)
4. **Aturan 2:** Ganti :0000: dengan :: (sekali saja)
5. **Dual Stack** = metode transisi yang direkomendasikan
6. IPv6 **tidak menggunakan broadcast**
7. IPv6 tidak membutuhkan NAT
