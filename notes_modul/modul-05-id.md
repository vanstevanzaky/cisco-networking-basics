# Modul 5: Communication Principles

**Modul:** 5 - Communication Principles  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- Protokol = aturan komunikasi jaringan
- Model OSI (7 layer) vs TCP/IP (4 layer)
- Data turun stack (encapsulation) saat kirim, naik stack saat terima

---

## 📚 Materi

### 1. Protokol Jaringan

**Definisi:** Aturan yang mengatur komunikasi antar perangkat.

| Protokol | Fungsi |
|----------|--------|
| Ethernet | Komunikasi di LAN |
| IP | Pengalamatan & routing |
| TCP | Pengiriman data reliable |
| UDP | Pengiriman data cepat (unreliable) |
| HTTP | Komunikasi web |
| DNS | Domain → IP address |

---

### 2. Model TCP/IP (4 Layer)

| Layer | Protokol | Fungsi |
|-------|----------|--------|
| **Application** | HTTP, DNS, FTP | Layanan aplikasi |
| **Transport** | TCP, UDP | Host-to-host |
| **Internet** | IP, ICMP | Addressing & routing |
| **Network Access** | Ethernet | Akses media fisik |

---

### 3. Model OSI (7 Layer)

| # | Layer | Fungsi | Contoh |
|---|-------|--------|--------|
| 7 | Application | Interface aplikasi | HTTP, DNS |
| 6 | Presentation | Format, enkripsi | SSL, JPEG |
| 5 | Session | Kelola sesi | NetBIOS |
| 4 | Transport | Segmentasi | TCP, UDP |
| 3 | Network | Logical addressing | IP, ICMP |
| 2 | Data Link | Physical addressing | Ethernet, MAC |
| 1 | Physical | Transmisi bit | Kabel, sinyal |

**Cara ingat:** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

---

### 4. Encapsulation

```
Data → Segment → Packet → Frame → Bits
(Application → Transport → Network → Data Link → Physical)
```

| Layer | PDU (Protocol Data Unit) |
|-------|--------------------------|
| Transport | Segment |
| Network | Packet |
| Data Link | Frame |

---

## 💡 Poin Penting

1. **Protokol** = aturan komunikasi jaringan
2. **OSI** = 7 layer, **TCP/IP** = 4 layer
3. **Layer 4 (Transport)** = TCP (reliable) atau UDP (fast)
4. **Layer 3 (Network)** = IP address
5. **Layer 2 (Data Link)** = MAC address
6. **Encapsulation** = data dibungkus header tiap layer
