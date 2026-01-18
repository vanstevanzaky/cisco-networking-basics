# Modul 7: Access Layer

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Konsep Inti

### 1. Encapsulation
**Definisi:** Proses membungkus pesan ke dalam format lain.

**Contoh:** Paket IP dibungkus ke dalam frame Ethernet

---

### 2. Ethernet Frame

**Field Penting:**
- **Destination MAC** - Alamat tujuan (6 bytes)
- **Source MAC** - Alamat pengirim (6 bytes)
- **Type/Length** - Jenis protokol (2 bytes)
- **Data (Payload)** - **46-1500 bytes**
- **FCS (Frame Check Sequence)** - Deteksi error (4 bytes)

**Poin Penting:** Payload Ethernet = **46 hingga 1500 bytes**

---

### 3. Access Layer

**Definisi:** Lapisan jaringan tempat host (PC, printer, IP phone) terhubung ke switch/hub untuk akses jaringan.

**Perangkat:**
- **Hub** - legacy, broadcast ke semua port (deprecated)
- **Switch** - modern, forward berdasarkan MAC address

---

## 🔄 Hub vs Switch

| Aspek | Hub | Switch |
|-------|-----|--------|
| **Layer** | Physical (Layer 1) | Data Link (Layer 2) |
| **Operasi** | Broadcast ke semua port | Forward ke port spesifik |
| **Collision** | Collision domain besar | Setiap port = collision domain terpisah |
| **Duplex** | Half-duplex | Full-duplex |
| **Efisiensi** | ❌ Rendah | ✅ Tinggi |
| **Penggunaan** | Legacy (tidak digunakan lagi) | Standard modern |

**Kesimpulan:** Switch jauh lebih efisien dan aman dari Hub

---

## 📡 Cara Kerja Switch

### 1. MAC Address Table

**Struktur:** Mapping antara MAC address ↔ Port

| MAC Address | Port | Aging Time |
|-------------|------|------------|
| AA:BB:CC:11:22:33 | Fa0/1 | 300s |
| DD:EE:FF:44:55:66 | Fa0/2 | 300s |

**Cara switch membangun tabel:**
- Switch membaca **Source MAC address** dari frame yang masuk
- Mencatat MAC address + port asal
- Simpan di MAC address table

**Poin Penting:** Tabel dibangun dari **source MAC**, bukan destination MAC

---

### 2. Proses Forwarding

**Langkah switch saat menerima frame:**

1. **Learn:** Tambahkan **source MAC** + port asal ke tabel MAC
2. **Forward:** Cek **destination MAC** di tabel:
   - **Jika ADA di tabel** → Forward ke port spesifik (unicast)
   - **Jika TIDAK ADA** → **Flooding** ke semua port kecuali port asal

**Flooding:** Kirim frame ke semua port kecuali port yang menerima frame

---

### 3. Fungsi Switch (Ringkas)

- **Learn** dari source MAC address
- **Forward** berdasarkan destination MAC address

---

## � Poin Penting

1. **Encapsulation** = membungkus data (Packet → Frame)
2. **Ethernet frame:** Dest MAC + Src MAC + Type + Data (46-1500 bytes) + FCS
3. **Switch = Layer 2**, menggunakan MAC address table
4. **MAC table dibangun dari source MAC** yang masuk
5. **Destination unknown → Flooding** ke semua port kecuali asal
6. **FCS** untuk error detection
7. **Hub (legacy) = broadcast semua**, Switch = unicast ke port spesifik


---

**Konsep Terkait:** Network Media (Modul 6), Internet Protocol (Modul 8)