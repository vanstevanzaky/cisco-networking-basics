# Modul 14: Routing Between Networks

**Modul:** 14 - Routing Between Networks  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Routing** = proses menentukan jalur terbaik ke tujuan
- **Router** bekerja di Layer 3 (IP address), **Switch** di Layer 2 (MAC address)
- **Default Gateway** = IP router untuk akses ke network lain
- **IP address TETAP** end-to-end, **MAC address BERUBAH** setiap hop
- **Broadcast domain** dibatasi oleh router

---

## 📚 Materi

### 1. Kenapa Perlu Membagi Network?

| Alasan | Penjelasan |
|--------|------------|
| **Limit Broadcast** | Broadcast hanya ke satu segmen, tidak membanjiri semua device |
| **Security** | Pisahkan departemen (Accounting tidak perlu akses ke Sales) |
| **Geografis** | Departemen di gedung/lantai berbeda |
| **Troubleshooting** | Network kecil lebih mudah di-debug |

**Broadcast Domain:** Area yang menerima broadcast message

---

### 2. Router vs Switch

| Aspek | Switch | Router |
|-------|--------|--------|
| **Layer** | Layer 2 (Data Link) | Layer 3 (Network) |
| **Keputusan berdasarkan** | MAC Address | IP Address |
| **Fungsi** | Forward frame di LAN yang sama | Forward packet antar network berbeda |
| **Broadcast** | Diteruskan ke semua port | **TIDAK** diteruskan |

**Key:** Setiap interface router = network berbeda

---

### 3. Kapan Butuh Router?

| Kondisi | Aksi |
|---------|------|
| **Source & Dest di network SAMA** | Kirim langsung (via switch) |
| **Source & Dest di network BEDA** | Kirim ke router (default gateway) |

**Cara host menentukan:**
1. Bandingkan network portion IP tujuan dengan IP sendiri (pakai subnet mask)
2. Jika sama → kirim langsung
3. Jika beda → kirim ke default gateway

---

### 4. Proses Komunikasi

#### A. Same Network (192.168.1.10 → 192.168.1.20)

```
H1 (192.168.1.10) ──► Switch ──► H2 (192.168.1.20)
```

| Step | Aksi |
|------|------|
| 1 | H1 buat IP packet (Src: 192.168.1.10, Dst: 192.168.1.20) |
| 2 | H1 cek: tujuan di network sama? **YA** |
| 3 | H1 cari MAC H2 via ARP |
| 4 | H1 buat frame dengan Dst MAC = H2 |
| 5 | Switch forward langsung ke H2 |

#### B. Different Network (192.168.1.10 → 192.168.2.50)

```
H1 ──► Switch ──► Router ──► Switch ──► H3
(192.168.1.10)    (Gateway)        (192.168.2.50)
```

| Step | Aksi |
|------|------|
| 1 | H1 buat IP packet (Src: 192.168.1.10, Dst: 192.168.2.50) |
| 2 | H1 cek: tujuan di network sama? **TIDAK** |
| 3 | H1 kirim ke **default gateway** (router) |
| 4 | H1 cari MAC router via ARP |
| 5 | H1 buat frame dengan Dst MAC = **Router** |
| 6 | Router terima, de-encapsulate frame |
| 7 | Router baca IP tujuan, cek **routing table** |
| 8 | Router buat frame baru dengan MAC baru |
| 9 | Router forward ke network tujuan |
| 10 | H3 terima packet |

---

### 5. Yang Berubah vs Tetap

| Layer | Address | Perubahan |
|-------|---------|-----------|
| **Layer 3** | IP Address | **TETAP** dari source ke destination |
| **Layer 2** | MAC Address | **BERUBAH** di setiap hop/segment |

**Contoh perjalanan packet:**

| Hop | Src MAC | Dst MAC | Src IP | Dst IP |
|-----|---------|---------|--------|--------|
| H1 → R1 | H1 | **R1** | 192.168.1.10 | 192.168.2.50 |
| R1 → H3 | **R1** | **H3** | 192.168.1.10 | 192.168.2.50 |

IP tetap, MAC berubah!

---

### 6. Routing Table

**Isi routing table:**
- Network address (bukan host individual)
- Best path ke network tersebut
- Interface untuk forward

**Jenis entry:**

| Tipe | Kode | Penjelasan |
|------|------|------------|
| **Directly Connected** | C | Network yang langsung terhubung ke router |
| **Static Route** | S | Dikonfigurasi manual oleh admin |
| **Dynamic Route** | D/O/R | Dipelajari otomatis dari router lain |

**Contoh Routing Table:**
```
Type  Network         Interface
C     10.0.0.0/8      FastEthernet0/0
C     172.16.0.0/16   FastEthernet0/1
S*    0.0.0.0/0       FastEthernet0/1  ← Default Route
```

**Default Route (0.0.0.0/0):** Digunakan jika network tujuan tidak ada di routing table

---

### 7. Default Gateway

**Definisi:** IP address interface router yang terhubung ke network lokal host

**Konfigurasi host:**

| PC | IP Address | Subnet Mask | Default Gateway |
|----|------------|-------------|-----------------|
| H1 | 192.168.1.1 | 255.255.255.0 | 192.168.1.254 |
| H2 | 192.168.1.2 | 255.255.255.0 | 192.168.1.254 |
| H3 | 192.168.1.3 | 255.255.255.0 | 192.168.1.254 |

**Penting:**
- ✅ Default gateway HARUS dikonfigurasi dengan benar
- ❌ Tanpa default gateway → tidak bisa akses remote network
- ❌ Default gateway salah → packet tidak sampai tujuan

---

### 8. Menentukan Default Gateway

**Aturan:** Default gateway = IP router yang **satu network** dengan host

```
         Router
    ┌───────┴───────┐
    │172.16.0.50    │192.168.1.1    │10.0.0.1
    ▼               ▼               ▼
┌───────┐      ┌───────┐       ┌───────┐
│  H3   │      │  H1   │       │  H2   │
│172.16.│      │192.168│       │10.0.0.│
│0.10   │      │.1.3   │       │2      │
└───────┘      └───────┘       └───────┘
   ▲               ▲               ▲
Gateway:       Gateway:        Gateway:
172.16.0.50    192.168.1.1     10.0.0.1
```

---

## 💡 Poin Penting

1. **Router** = Layer 3 (IP), **Switch** = Layer 2 (MAC)
2. **Routing** = proses menentukan jalur terbaik ke tujuan
3. Network dibagi untuk: limit broadcast, security, geografis
4. **Same network** → kirim langsung, **Different network** → via router
5. **IP address TETAP** end-to-end
6. **MAC address BERUBAH** setiap hop
7. **Default gateway** = IP router di network lokal
8. **Default route** = jalur untuk destination yang tidak dikenal
9. Router **TIDAK** forward broadcast
10. Setiap interface router = broadcast domain berbeda

**Ingat untuk quiz:**
- Router forward packet berdasarkan → **Destination IP address**
- Host kirim ke default gateway → saat destination di **network berbeda**
- Default route digunakan → packet dengan destination **tidak ada di routing table**
