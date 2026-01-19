# Lab 2: Connect to a Web Server

**Module:** 8 (The Internet Protocol)  
**Topik:** 8.1.3 Connect to a Web Server  
**Tanggal Selesai:** 19 Januari 2026  
**Status:** ✅ SELESAI

---

## 📝 Summary (TL;DR)

- ✅ Verifikasi konektivitas ke web server dengan **ping**
- ✅ Akses web server menggunakan **IP address** (172.33.100.50)
- ✅ Memahami bahwa komunikasi Internet menggunakan IP address

---

## 📌 Tujuan Lab

> **Observe how packets are sent across the Internet using IP addresses.**

Mengamati bagaimana paket dikirim melalui Internet menggunakan alamat IP.

---

## 🖥️ Topologi & Perangkat

| Device | Fungsi |
|--------|--------|
| **PC0** | Client (source host) |
| **Web Server** | Server dengan IP 172.33.100.50 |

---

## 🔧 Hasil Praktik

### Part 1: Verify Connectivity to Web Server

**Langkah:**
1. Pilih **PC0**
2. Buka **Desktop Tab** → **Command Prompt**
3. Jalankan perintah ping ke web server

**Command:**
```
PC> ping 172.33.100.50
```

**Output:**
```
Pinging 172.33.100.50 with 32 bytes of data:

Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127

Ping statistics for 172.33.100.50:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

**Kesimpulan:** Reply menunjukkan konektivitas berhasil dari client ke web server.

> **Note:** Reply mungkin timeout di awal saat devices loading dan ARP dilakukan.

---

### Part 2: Connect to Web Server via Web Browser

**Langkah:**
1. Di **Desktop tab** PC0, pilih **Web Browser**
2. Ketik **172.33.100.50** di URL bar
3. Klik **Go**

**Hasil:**
- Web browser berhasil menampilkan halaman web dari server
- Koneksi menggunakan IP address langsung (tanpa domain name)

---

## ❓ Reflection Question

**Q: What messages did you see after the web page has finished loading?**

**A:** "You were able to reach this website because you had the IP address of the web server. The connecting PC also had a web client running on the device."

**Penjelasan:**
- Bisa mengakses website karena **mengetahui IP address** server
- PC client memiliki **web client (browser)** untuk mengirim request

---

## 💡 Learning Outcomes

1. **IP Address = Identifier untuk Komunikasi**
   - Untuk akses web server, kita butuh IP address-nya
   - IP memungkinkan packet sampai ke tujuan yang benar

2. **Ping untuk Verifikasi Konektivitas**
   - Sebelum akses service, pastikan koneksi OK dengan ping
   - Reply = reachable, Timeout = ada masalah

3. **Web Communication**
   - Browser (client) mengirim HTTP request ke IP server
   - Server merespons dengan halaman web

---

## ✅ Verification Checklist

- [x] Ping ke 172.33.100.50 berhasil (Reply received)
- [x] Web browser dapat menampilkan halaman dari server
- [x] Memahami peran IP address dalam komunikasi
- [x] Completion: 100%

---

## 🔗 Hubungan dengan Modul 8

Lab ini mendemonstrasikan:
- **Tujuan IP address** - identifikasi dan lokasi web server
- **Komunikasi menggunakan IP** - packet dikirim berdasarkan destination IP
- **Client-Server model** - PC0 sebagai client, 172.33.100.50 sebagai server

---

**File Lab:** `Connect to a Web Server.pka`
