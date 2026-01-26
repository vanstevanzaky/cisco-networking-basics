# Modul 9: IPv4 Transmission & Addressing

**Modul:** 9 - IPv4 Transmission Types & Addressing  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **3 jenis transmisi:** Unicast (1-to-1), Broadcast (1-to-all), Multicast (1-to-group)
- **Source address selalu unicast** (paket hanya dari 1 sumber)
- **IPv4 Privat** untuk internal (10.x, 172.16-31.x, 192.168.x), tidak bisa di-route ke internet
- **IPv4 Publik** untuk internet, harus unik secara global

---

## 📚 Materi

### 1. Jenis Transmisi IPv4

| Tipe | Komunikasi | Destination Address | Penerima |
|------|------------|---------------------|----------|
| **Unicast** | One-to-One | IP spesifik | 1 perangkat |
| **Broadcast** | One-to-All | 255.255.255.255 atau x.x.x.255 | Semua di jaringan |
| **Multicast** | One-to-Many | 224.0.0.0 - 239.255.255.255 | Grup tertentu |

---

### 2. Broadcast

| Jenis | Alamat | Contoh |
|-------|--------|--------|
| **Limited Broadcast** | 255.255.255.255 | DHCP Discover |
| **Directed Broadcast** | Host bits = 1 | 172.16.4.255/24 |

**Catatan:** Router TIDAK meneruskan broadcast ke jaringan lain

---

### 3. Multicast

**Rentang:** 224.0.0.0 - 239.255.255.255

| Protokol | Alamat | Fungsi |
|----------|--------|--------|
| OSPF | 224.0.0.5 | Routing protocol |
| RIP v2 | 224.0.0.9 | Routing updates |
| EIGRP | 224.0.0.10 | Cisco routing |

---

### 4. IPv4 Privat vs Publik

**Alamat Privat (tidak di-route di internet):**

| Class | Rentang | Prefix |
|-------|---------|--------|
| A | 10.0.0.0 - 10.255.255.255 | /8 |
| B | 172.16.0.0 - 172.31.255.255 | /12 |
| C | 192.168.0.0 - 192.168.255.255 | /16 |

**Alamat Publik:** Unik global, dikelola RIR, butuh registrasi

---

### 5. Alamat IPv4 Khusus (Special Use)

| Alamat | Nama | Fungsi |
|--------|------|--------|
| **127.0.0.0/8** | Loopback | Tes koneksi ke diri sendiri (ping 127.0.0.1) |
| **169.254.0.0/16** | Link-Local / APIPA | Auto-assign jika DHCP gagal |
| **240.0.0.0 - 255.0.0.0** | Experimental | Reserved, tidak digunakan |

---

### 6. IANA dan RIR

```
IANA → RIR → ISP → End User
```

| RIR | Wilayah |
|-----|---------|
| APNIC | Asia-Pacific (Indonesia) |
| ARIN | Amerika Utara |
| RIPE NCC | Eropa |
| LACNIC | Amerika Latin |
| AFRINIC | Afrika |

---

### 7. Jenis Alamat dalam Subnet

**Contoh: 192.168.1.0/24**

| Jenis | Alamat | Host Bits | Assign ke Host? |
|-------|--------|-----------|-----------------|
| Network | 192.168.1.0 | Semua 0 | Tidak |
| Host | 192.168.1.1-254 | Campuran | Ya |
| Broadcast | 192.168.1.255 | Semua 1 | Tidak |

**Usable hosts = Total - 2** (kurangi network dan broadcast)

---

## 💡 Poin Penting

1. **Unicast** = 1 ke 1, **Broadcast** = 1 ke semua, **Multicast** = 1 ke grup
2. **Source address selalu unicast**
3. **IPv6 tidak punya broadcast**
4. **Privat:** 10.x, 172.16-31.x, 192.168.x (butuh NAT untuk internet)
5. **Publik:** Harus unik global, dikelola RIR
6. **Network address:** Host bits = 0
7. **Broadcast address:** Host bits = 1
8. **IANA → RIR → ISP → End User**
