# Modul 12: Gateways to Other Networks

**Modul:** 12 - Gateways to Other Networks  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Default Gateway** = "pintu keluar" untuk mengirim traffic ke network lain
- **Router** berperan sebagai gateway antara network yang berbeda
- Host perlu: **IP Address + Subnet Mask + Default Gateway** untuk komunikasi ke luar
- **Binary ANDing** digunakan untuk menentukan apakah tujuan lokal atau remote
- **NAT** mengubah private IP menjadi public IP agar bisa akses internet

---

## 📚 Materi

### 1. Apa Itu Gateway?

**Analogi:** Gateway = pintu keluar dari ruangan
- Kalau mau keluar ruangan → harus lewat pintu
- Kalau mau kirim data keluar network → harus lewat gateway

| Situasi | Yang Terjadi |
|---------|--------------|
| Tujuan di **network yang sama** | Kirim langsung ke tujuan |
| Tujuan di **network berbeda** | Kirim ke default gateway dulu |

---

### 2. Bagaimana Host Menentukan Tujuan?

**Binary ANDing Process:**
1. Host ambil **destination IP** dan **subnet mask**
2. Lakukan operasi AND binary
3. Bandingkan **network portion** dari:
   - IP address pengirim
   - IP address tujuan
4. **Sama** → tujuan di local network
5. **Berbeda** → tujuan di remote network → kirim ke gateway

```
Contoh:
Host IP:        192.168.1.10  / 255.255.255.0
Tujuan A:       192.168.1.50  → Network sama (192.168.1.0) → LOKAL
Tujuan B:       10.0.0.5      → Network beda (10.0.0.0) → REMOTE → ke Gateway
```

---

### 3. Konfigurasi Minimum Host

| Parameter | Wajib? | Fungsi |
|-----------|--------|--------|
| **IP Address** | ✅ Ya | Identitas host di network |
| **Subnet Mask** | ✅ Ya | Menentukan network vs host portion |
| **Default Gateway** | ⚡ Untuk remote | Alamat router untuk keluar network |

**Catatan:** Tanpa default gateway, host **hanya bisa** komunikasi dalam local network!

---

### 4. Router sebagai Gateway

**Karakteristik:**
- Setiap **interface router** terhubung ke network berbeda
- Setiap interface punya **IP address sendiri**
- IP address interface = **default gateway** untuk host di network tersebut

```
┌─────────────────────────────────────────────────────┐
│                      ROUTER                         │
│   Interface Gi0/0          Interface Gi0/1          │
│   192.168.1.1              10.0.0.1                 │
└───────┬─────────────────────────────┬───────────────┘
        │                             │
   Network A                     Network B
   192.168.1.0/24               10.0.0.0/24
   Gateway: 192.168.1.1         Gateway: 10.0.0.1
```

**Penting:** Host di network yang berbeda punya **default gateway yang berbeda**!

---

### 5. Proses ARP untuk Gateway

Ketika host ingin kirim ke remote network:
1. Host tentukan tujuan = **remote** (via binary ANDing)
2. Host perlu MAC address **default gateway** (bukan MAC tujuan akhir!)
3. Host kirim **ARP request** untuk default gateway
4. Router reply dengan MAC address-nya
5. Packet dikirim ke router dengan:
   - **Destination MAC** = MAC router
   - **Destination IP** = IP tujuan akhir

---

### 6. Kesalahan Umum Konfigurasi

| Kesalahan | Akibat |
|-----------|--------|
| Default gateway **tidak di network yang sama** | ARP gagal, tidak bisa kirim traffic keluar |
| Subnet mask salah | Salah menentukan lokal vs remote |
| Typo di gateway address | Traffic tidak bisa keluar network |

**Contoh Error:**
```
Host IP:      192.168.1.10 / 255.255.255.0
Gateway:      192.168.11.1  ❌ (Salah! Beda network)
Seharusnya:   192.168.1.1   ✅
```

---

### 7. Router sebagai Network Boundary

**Wireless Router = 2 Peran:**

| Sisi | Fungsi | Tipe IP |
|------|--------|---------|
| **Internal (LAN)** | DHCP Server | Private IP (192.168.x.x) |
| **External (WAN)** | DHCP Client | Public IP (dari ISP) |

```
┌───────────────────────────────────────────────────────────┐
│                         INTERNET                          │
│                     (ISP DHCP Server)                     │
└───────────────────────────┬───────────────────────────────┘
                            │
                    External: 192.150.45.3 (Public)
                    ┌───────┴───────┐
                    │ Wireless      │ ← Network Boundary
                    │ Router        │
                    └───────┬───────┘
                    Internal: 192.168.1.1 (Private)
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
   192.168.1.2         192.168.1.3         192.168.1.4
   (DHCP Client)       (DHCP Client)       (DHCP Client)
```

---

### 8. Internal vs External Network

| Aspek | Internal Network | External Network |
|-------|------------------|------------------|
| Lokasi | Di dalam router (LAN side) | Di luar router (WAN/Internet side) |
| Tipe IP | **Private** (192.168.x.x, 10.x.x.x) | **Public** (dari ISP) |
| DHCP | Router = Server | Router = Client |
| Akses Internet | Tidak langsung | Langsung |

**DHCP yang diberikan router ke client:**
- IPv4 Address
- Subnet Mask  
- Default Gateway (IP internal router)

---

##  Poin Penting

1. **Default Gateway** = router interface untuk keluar dari local network
2. Host butuh **IP + Subnet Mask + Gateway** untuk komunikasi remote
3. **Binary ANDing** menentukan apakah tujuan lokal atau remote
4. Host di network berbeda → **default gateway berbeda**
5. Untuk kirim ke remote → ARP untuk **MAC address gateway** (bukan tujuan)
6. Gateway address **harus di network yang sama** dengan host
7. Wireless router = **boundary** antara internal (private) dan external (public)
8. Router bisa jadi **DHCP client** (dari ISP) dan **DHCP server** (untuk LAN) sekaligus

