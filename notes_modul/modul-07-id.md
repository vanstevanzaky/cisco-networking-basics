# Modul 7: Access Layer

**Modul:** 7 - Access Layer  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Access layer** = tempat end device (PC, printer) terhubung ke jaringan
- **Encapsulation** = proses membungkus data (Packet → Frame)
- **Switch** menggunakan MAC address table untuk forward frame
- MAC table dibangun dari **source MAC**, forward berdasarkan **destination MAC**

---

## 📚 Materi

### 1. Encapsulation

**Definisi:** Proses membungkus pesan ke dalam format lain

**Contoh:** Paket IP dibungkus ke dalam frame Ethernet

---

### 2. Ethernet Frame

| Field | Ukuran | Fungsi |
|-------|--------|--------|
| Destination MAC | 6 bytes | Alamat tujuan |
| Source MAC | 6 bytes | Alamat pengirim |
| Type/Length | 2 bytes | Jenis protokol |
| **Data (Payload)** | **46-1500 bytes** | Isi data |
| FCS | 4 bytes | Error detection |

---

### 3. Access Layer

**Definisi:** Lapisan jaringan tempat host terhubung ke switch untuk akses jaringan

| Perangkat | Layer | Operasi |
|-----------|-------|---------|
| **Hub** | Physical (L1) | Broadcast ke semua port (legacy) |
| **Switch** | Data Link (L2) | Forward ke port spesifik |

---

### 4. Hub vs Switch

| Aspek | Hub | Switch |
|-------|-----|--------|
| Layer | Physical (L1) | Data Link (L2) |
| Operasi | Broadcast semua | Forward spesifik |
| Collision Domain | Besar (satu domain) | Per port terpisah |
| Duplex | Half-duplex | Full-duplex |
| Efisiensi | Rendah | Tinggi |
| Status | Legacy | Standard modern |

---

### 5. Cara Kerja Switch

**MAC Address Table:**

| MAC Address | Port |
|-------------|------|
| AA:BB:CC:11:22:33 | Fa0/1 |
| DD:EE:FF:44:55:66 | Fa0/2 |

**Proses Forwarding:**

1. **Learn:** Tambahkan source MAC + port asal ke tabel
2. **Forward:** Cek destination MAC di tabel
   - **Ada di tabel** → Forward ke port spesifik (unicast)
   - **Tidak ada** → Flooding ke semua port kecuali asal

**Poin kunci:** Tabel dibangun dari **source MAC**, forward berdasarkan **destination MAC**

---

## 💡 Poin Penting

1. **Encapsulation** = membungkus data (Packet → Frame)
2. **Ethernet payload** = 46 hingga 1500 bytes
3. **Switch** = Layer 2, menggunakan MAC address table
4. **MAC table dibangun dari source MAC** yang masuk
5. **Destination unknown** → Flooding ke semua port kecuali asal
6. **FCS** untuk error detection
7. **Hub = broadcast semua** (legacy), **Switch = unicast** ke port spesifik
