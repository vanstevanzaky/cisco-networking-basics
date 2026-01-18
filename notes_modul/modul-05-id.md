# Modul 5: Prinsip Komunikasi (Communication Principles)

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Konsep Inti

### 1. Protokol Jaringan
**Definisi:** Sekumpulan aturan yang mengatur proses komunikasi antar perangkat jaringan.

**Protokol Penting:**
- **Ethernet** - komunikasi di LAN
- **IP** - pengalamatan dan routing antar jaringan
- **TCP** - pengiriman data yang andal (reliable)
- **HTTP** - komunikasi web
- **DNS** - terjemahan nama domain ke IP address

### 2. Protocol Stack
**Definisi:** Susunan protokol dalam bentuk lapisan (layers) yang bekerja sama untuk komunikasi data.

**Cara kerja:**
- Data turun stack saat dikirim (encapsulation)
- Data naik stack saat diterima (de-encapsulation)

---

## 🔄 Model TCP/IP (4 Layer)

| Layer | Protokol | Fungsi |
|-------|----------|--------|
| **Application** | HTTP, FTP, DNS | Layanan aplikasi |
| **Transport** | TCP, UDP | Komunikasi host-to-host |
| **Internet** | IP, ICMP | Pengalamatan & routing |
| **Network Access** | Ethernet | Akses ke media fisik |

---

## 📊 Model OSI (7 Layer)

| Layer | Fungsi Utama |
|-------|--------------|
| 7. Application | Interface ke aplikasi |
| 6. Presentation | Format, enkripsi, kompresi |
| 5. Session | Mengatur sesi komunikasi |
| 4. Transport | Segmentasi & reliability |
| 3. Network | Logical addressing & routing |
| 2. Data Link | Framing & MAC addressing |
| 1. Physical | Transmisi bit |

**Cara mengingat:** All People Seem To Need Data Processing

---

## 🆚 Perbandingan OSI vs TCP/IP

| Aspek | OSI | TCP/IP |
|-------|-----|--------|
| Jumlah layer | 7 | 4 |
| Tipe | Konseptual | Praktis |
| Penggunaan | Pembelajaran | Internet nyata |

**Kesamaan:** Kedua model punya layer Transport dan Network

---

## 📦 Encapsulation

**Definisi:** Proses membungkus satu format pesan ke dalam format lain agar dapat dikirim melalui jaringan.

**Proses:**
1. Data → Segment (TCP/UDP header)
2. Segment → Packet (IP header)  
3. Packet → Frame (Ethernet header)
4. Frame → Bits (sinyal fisik)

---

## 💡 Poin Penting

1. **Protokol** = aturan komunikasi antar device
2. **TCP** = reliable (connection), **UDP** = fast (connectionless)
3. **Encapsulation:** Data → Segment → Packet → Frame → Bits
4. **OSI 7 layer** untuk konsep, **TCP/IP 4 layer** untuk praktis

---

**Konsep Terkait:** Network Media (Modul 6), Access Layer (Modul 7)