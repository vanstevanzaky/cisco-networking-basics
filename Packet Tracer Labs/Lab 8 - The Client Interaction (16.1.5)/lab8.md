# Lab 8: Interaksi Klien (Client Interaction)

**Module:** 16 (Application Layer Services)  
**Topik:** 16.1.5  
**Status:** ✅ Selesai

---

## 📌 Tujuan Lab

- Mengamati interaksi antara server dan PC
- Memahami proses DNS resolution
- Memahami alur HTTP request/response
- Melacak aliran PDU menggunakan Simulation Mode

---

## 📋 Latar Belakang

Lab ini menggunakan network sederhana:
- **1 PC** → request services
- **1 Server** → DNS + HTTP services
- Koneksi langsung (tanpa router/switch)

**Fokus:** Mengamati traffic flow saat request web page:
1. DNS resolve URL → IP address
2. HTTP request web page
3. Server kirim web page (2 segments)
4. PC acknowledge receipt

---

## 🔧 Hasil Praktik

### Part 1: Masuk Simulation Mode

- Klik **Simulation Mode** (icon di kanan bawah)
- Mode berubah dari Realtime → Simulation

### Part 2: Atur Filter Event List

**Filter hanya DNS dan HTTP:**
1. Klik **Show All/None** → hapus semua centang
2. Klik **Edit Filters**
   - Tab IPv4 → ✅ DNS
   - Tab Misc → ✅ HTTP
3. Tutup window

### Part 3: Request Halaman Web

1. Klik **PC** → Desktop → **Web Browser**
2. Ketik URL: `www.example.com`
3. Klik **Go**
4. Minimize window PC

### Part 4: Jalankan Simulasi

Klik **Play** → amati animasi

**Events yang terjadi:**

| # | Event | Deskripsi |
|---|-------|-----------|
| 1 | DNS Query | PC bertanya: "www.example.com = IP berapa?" |
| 2 | DNS Response | Server jawab: "www.example.com = 192.168.1.x" |
| 3 | HTTP Request | PC request halaman web ke IP server |
| 4 | HTTP Response (1) | Server kirim segment 1 |
| 5 | HTTP Response (2) | Server kirim segment 2 |
| 6 | TCP ACK | PC konfirmasi sudah terima data |

### Part 5 & 6: Periksa PDU Information

**PDU Information Window:**
- Klik kotak warna di Event List
- Klik **Next Layer >>** untuk lihat detail tiap layer

**Breakdown OSI Layer:**

| Layer | Keluar (PC → Server) | Masuk (Server → PC) |
|-------|----------------------|---------------------|
| **Application** | DNS Query / HTTP GET | DNS Response / HTTP Data |
| **Transport** | UDP:53 / TCP:80 | UDP:53 / TCP:80 |
| **Network** | Src IP → Dst IP | Src IP → Dst IP |
| **Data Link** | Src MAC → Dst MAC | Src MAC → Dst MAC |

---

## 📊 Diagram Alur

```
┌─────┐                              ┌────────┐
│ PC  │                              │ Server │
└──┬──┘                              └───┬────┘
   │                                     │
   │  1. DNS Query (UDP:53)              │
   │  "www.example.com = ?"              │
   │ ──────────────────────────────────► │
   │                                     │
   │  2. DNS Response (UDP:53)           │
   │  "www.example.com = 192.168.1.x"    │
   │ ◄────────────────────────────────── │
   │                                     │
   │  3. HTTP GET (TCP:80)               │
   │  "GET /index.html"                  │
   │ ──────────────────────────────────► │
   │                                     │
   │  4. HTTP Response (TCP:80)          │
   │  "HTML content segment 1"           │
   │ ◄────────────────────────────────── │
   │                                     │
   │  5. HTTP Response (TCP:80)          │
   │  "HTML content segment 2"           │
   │ ◄────────────────────────────────── │
   │                                     │
   │  6. TCP ACK                         │
   │ ──────────────────────────────────► │
   │                                     │
```

---

## 💡 Pemahaman & Poin Penting

### Konsep Utama:

1. **DNS dulu baru HTTP** - Browser harus resolve URL ke IP dulu
2. **UDP untuk DNS** - Query cepat, tidak perlu connection setup
3. **TCP untuk HTTP** - Reliable, data harus lengkap
4. **Segmentation** - Halaman web dipecah jadi beberapa segment
5. **ACK** - PC konfirmasi setelah terima data

### Port Protocol:
| Protocol | Port | Transport |
|----------|------|-----------|
| DNS | 53 | UDP |
| HTTP | 80 | TCP |

### Kesimpulan:
- **1 web request = banyak packet** (DNS + HTTP)
- **Simulation Mode** berguna untuk troubleshooting
- **PDU Information** menunjukkan detail tiap layer
- Browser otomatis handle DNS resolution

### Relevansi CyberSec:
- DNS spoofing bisa redirect ke website palsu
- HTTP tidak terenkripsi (pakai HTTPS untuk aman)
- Packet capture bisa mengungkap aktivitas browsing
