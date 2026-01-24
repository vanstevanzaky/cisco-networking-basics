# Modul 11: Dynamic Addressing (DHCP)

**Modul:** 11 - Dynamic Addressing with DHCP  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Static IP** untuk device penting (server, printer), dikonfigurasi manual
- **Dynamic IP (DHCP)** untuk client biasa, otomatis
- **DORA process:** Discover → Offer → Request → Acknowledgment
- **Lease** = IP dipinjam sementara, dikembalikan saat disconnect

---

## 📚 Materi

### 1. Static vs Dynamic IP

| Aspek | Static | Dynamic (DHCP) |
|-------|--------|----------------|
| Konfigurasi | Manual | Otomatis |
| Cocok untuk | Server, printer, router | Laptop, HP, PC user |
| Keuntungan | Predictable, kontrol penuh | Efisien, tidak repot |
| Kekurangan | Memakan waktu, rentan error | IP bisa berubah |

---

### 2. DHCP (Dynamic Host Configuration Protocol)

**Informasi yang diberikan DHCP:**
- IPv4 address
- Subnet mask
- Default gateway
- DNS server
- Lease time

---

### 3. DORA Process

| Step | Nama | Pengirim | Fungsi |
|------|------|----------|--------|
| 1 | **Discover** | Client | Broadcast mencari DHCP server |
| 2 | **Offer** | Server | Tawarkan IP address |
| 3 | **Request** | Client | Minta IP yang ditawarkan |
| 4 | **Acknowledgment** | Server | Konfirmasi IP diberikan |

**Catatan:** Discover dan Request adalah **broadcast**

---

### 4. DHCP Server

| Environment | DHCP Server |
|-------------|-------------|
| Enterprise | Dedicated server (Windows Server, Linux) |
| Home/Small Office | Wireless router |
| Mobile User | ISP server |

**Wireless router** bisa jadi DHCP client (dari ISP) sekaligus DHCP server (untuk LAN)

---

### 5. Lease Concept

**Proses:**
1. Client connect → Dapat IP (lease 24 jam misalnya)
2. Client disconnect → IP dikembalikan ke pool
3. Client lain → Bisa dapat IP yang sama

**Renewal:** Client akan memperpanjang lease sebelum habis (biasanya di 50% waktu)

---

### 6. Kapan Pakai Static vs Dynamic?

| Device | Rekomendasi | Alasan |
|--------|-------------|--------|
| Web Server | Static | Client perlu IP tetap |
| Printer kantor | Static | Semua PC perlu tahu IP-nya |
| Laptop karyawan | Dynamic | IP berubah tidak masalah |
| Guest WiFi | Dynamic | Sementara, tidak perlu IP tetap |

---

## 💡 Poin Penting

1. **Static IP** untuk server dan device penting
2. **Dynamic IP (DHCP)** untuk client biasa
3. **DORA:** Discover → Offer → Request → Acknowledgment
4. DHCP memberikan: IP, subnet mask, gateway, DNS, lease time
5. **Lease** = IP dipinjam, bukan permanen
6. IP dikembalikan ke pool saat device disconnect
7. Wireless router bisa jadi **DHCP client dan server** sekaligus
