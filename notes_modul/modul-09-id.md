# Modul 9: IPv4 Transmission Types & Addressing

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Konsep Inti

### 1. Jenis Transmisi IPv4

**Definisi:** Cara pengiriman paket dari sumber ke tujuan memengaruhi alamat IPv4 destination.

**Tipe Transmisi:**

| Tipe | Komunikasi | Destination Address | Penerima |
|------|------------|---------------------|----------|
| **Unicast** | One-to-One | Alamat IP spesifik | 1 perangkat |
| **Broadcast** | One-to-All | 255.255.255.255 atau x.x.x.255 | Semua perangkat di jaringan |
| **Multicast** | One-to-Many | 224.0.0.0 - 239.255.255.255 | Grup perangkat tertentu |

**Poin Penting:** 
- Source address **SELALU unicast** (paket hanya bisa dari 1 sumber)
- IPv6 **tidak menggunakan broadcast**

---

## 🎯 Unicast

**Definisi:** Transmisi dari satu perangkat ke satu perangkat (one-to-one).

**Contoh:**
```
Source:      172.16.4.1/24
Destination: 172.16.4.253/24
```

**Karakteristik:**
- Alamat tujuan = IP spesifik satu perangkat
- Switch meneruskan frame ke port tujuan saja
- **Rentang unicast:** 1.1.1.1 - 223.255.255.255 (dengan beberapa alamat reserved)

---

## 📡 Broadcast

**Definisi:** Transmisi dari satu perangkat ke semua perangkat di jaringan (one-to-all).

**Jenis Broadcast:**

| Jenis | Alamat | Scope | Contoh |
|-------|--------|-------|--------|
| **Limited Broadcast** | 255.255.255.255 | Jaringan lokal | DHCP Discover |
| **Directed Broadcast** | Network + semua bit host = 1 | Jaringan spesifik | 172.16.4.255/24 |

**Cara Kerja:**
1. Host mengirim paket ke 255.255.255.255
2. Switch forward ke **semua port** (kecuali port asal)
3. Semua perangkat di jaringan menerima dan memproses
4. Router **TIDAK meneruskan** broadcast ke jaringan lain

**Poin Penting:**
- Broadcast = semua bit host bernilai **1**
- Menggunakan resource jaringan → harus dibatasi
- Router memisahkan **broadcast domain**

---

## 🔀 Multicast

**Definisi:** Transmisi dari satu perangkat ke grup perangkat tertentu (one-to-many).

**Rentang Alamat:** 224.0.0.0 - 239.255.255.255

**Cara Kerja:**
- Host mengirim paket ke alamat multicast (misal: 224.0.0.5)
- Hanya perangkat yang **berlangganan grup multicast** yang memproses
- Perangkat lain mengabaikan paket

**Contoh Penggunaan:**

| Protokol | Alamat Multicast | Fungsi |
|----------|------------------|--------|
| **OSPF** | 224.0.0.5 | Routing protocol |
| **RIP v2** | 224.0.0.9 | Routing updates |
| **EIGRP** | 224.0.0.10 | Cisco routing |

**Keuntungan:** Mengurangi traffic jaringan (1 paket → banyak penerima)

---

## 🌐 Alamat IPv4 Privat vs Publik

### IPv4 Privat

**Definisi:** Alamat untuk jaringan internal, **tidak dirutekan di internet**.

**Rentang Alamat Privat:**

| Class | Rentang | Prefix | Total Host |
|-------|---------|--------|------------|
| **A** | 10.0.0.0 - 10.255.255.255 | /8 | ~16 juta |
| **B** | 172.16.0.0 - 172.31.255.255 | /12 | ~1 juta |
| **C** | 192.168.0.0 - 192.168.255.255 | /16 | ~65 ribu |

**Karakteristik:**
- Boleh digunakan **organisasi mana pun**
- Tidak perlu registrasi
- Butuh **NAT** untuk akses internet

---

### IPv4 Publik

**Definisi:** Alamat untuk komunikasi di internet, harus **unik secara global**.

**Karakteristik:**
- Harus didaftarkan via RIR/ISP
- Terbatas jumlahnya → **IPv4 exhaustion**
- Solusi: NAT + IPv6

---

## 🏛️ IANA dan RIR

### Struktur Pengelolaan IP Global

```
IANA (Internet Assigned Numbers Authority)
    ↓
RIR (Regional Internet Registry)
    ↓
ISP / LIR (Local Internet Registry)
    ↓
End Users / Organizations
```

**Regional Internet Registries:**

| RIR | Wilayah | Contoh Negara |
|-----|---------|---------------|
| **APNIC** | Asia-Pacific | Indonesia, Jepang, Australia |
| **ARIN** | Amerika Utara | USA, Kanada |
| **RIPE NCC** | Eropa | Jerman, UK, Rusia |
| **LACNIC** | Amerika Latin | Brasil, Argentina |
| **AFRINIC** | Afrika | Afrika Selatan, Kenya |

---

## 📋 Jenis Alamat IPv4 dalam Subnet

**Contoh Jaringan:** 192.168.1.0/24

| Jenis | Alamat | Bit Host | Fungsi | Boleh di-assign ke host? |
|-------|--------|----------|--------|---------------------------|
| **Network Address** | 192.168.1.0 | Semua 0 | Identifikasi jaringan | ❌ Tidak |
| **Host Address** | 192.168.1.1 - 192.168.1.254 | Campuran | Perangkat endpoint | ✅ Ya |
| **Broadcast Address** | 192.168.1.255 | Semua 1 | Broadcast dalam subnet | ❌ Tidak |

**Perhitungan:**
```
Network:    192.168.1.0/24
Total IP:   256 (2^8 host bits)
Usable:     254 (total - network - broadcast)
First Host: 192.168.1.1
Last Host:  192.168.1.254
Broadcast:  192.168.1.255
```

---

## 🎓 Rangkuman

**Transmisi:**
- **Unicast** = 1 ke 1 (normal communication)
- **Broadcast** = 1 ke semua (discovery, announcement)
- **Multicast** = 1 ke grup (streaming, routing protocols)

**Addressing:**
- **Privat** = internal network (10.x, 172.16-31.x, 192.168.x)
- **Publik** = internet-routable (managed by RIR)
- **Network** = bit host semua 0
- **Broadcast** = bit host semua 1

**IANA → RIR → ISP → End User**

---

**🎯 Status Modul:** Selesai
