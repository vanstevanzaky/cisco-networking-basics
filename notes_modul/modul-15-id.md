# Modul 15: TCP dan UDP

**Modul:** 15 - TCP and UDP  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **TCP** = Reliable, ada sequence number & acknowledgement
- **UDP** = Unreliable, cepat, tanpa overhead
- **Port Number** = Identifikasi aplikasi/service
- **Socket** = Kombinasi IP:Port
- **netstat** = Command untuk cek active connections

---

## 📚 Materi

### 1. Transport Layer Protocols

Di Transport Layer, data dipecah menjadi **segments** dan diberi **port information**.

| Protocol | Karakteristik | Use Case |
|----------|---------------|----------|
| **TCP** | Reliable, ordered, acknowledged | Web, Email, FTP, File transfer |
| **UDP** | Unreliable, fast, no overhead | Streaming, VoIP, Gaming, DNS |

---

### 2. UDP (User Datagram Protocol)

**Karakteristik:**
- ❌ Tidak ada sequence number
- ❌ Tidak ada acknowledgement
- ✅ Cepat (minimal overhead)
- ✅ Cocok untuk real-time

**Cara Kerja:**
```
Data → Segments → Add Port Info → Kirim → Done!
```

**Kapan pakai UDP?**
- Streaming video/audio
- VoIP (IP Phone)
- Online gaming
- DNS queries

> "Kalau beberapa packet hilang di VoIP, kita tidak akan notice. Delay untuk retransmit justru lebih mengganggu daripada kehilangan beberapa packet."

---

### 3. TCP (Transmission Control Protocol)

**Karakteristik:**
- ✅ Sequence number di setiap segment
- ✅ Acknowledgement (ACK)
- ✅ Retransmission jika packet hilang
- ✅ Ordered delivery
- ❌ Lebih lambat (ada overhead)

**Cara Kerja:**
```
Data → Segments → Add Port + Sequence # → Kirim → ACK → Next batch
```

**Kapan pakai TCP?**
- Web browsing (HTTP/HTTPS)
- Email (SMTP, POP3, IMAP)
- File transfer (FTP)
- Bank transactions
- Apapun yang butuh **semua data sampai lengkap**

> "Dalam transfer bank jutaan dollar, kalau kehilangan packet yang berisi account number → CATASTROPHIC!"

---

### 4. TCP vs UDP Comparison

| Aspek | TCP | UDP |
|-------|-----|-----|
| **Reliability** | ✅ Reliable | ❌ Unreliable |
| **Sequence Number** | ✅ Ada | ❌ Tidak ada |
| **Acknowledgement** | ✅ Ada | ❌ Tidak ada |
| **Retransmission** | ✅ Otomatis | ❌ Tidak ada |
| **Order Guarantee** | ✅ In-order | ❌ Out-of-order possible |
| **Speed** | Lebih lambat | Lebih cepat |
| **Overhead** | Tinggi | Rendah |
| **Connection** | Connection-oriented | Connectionless |

---

### 5. TCP Window & Acknowledgement

**Proses:**
1. Source kirim segments dengan sequence number (1, 2, 3)
2. Destination terima semua → kirim ACK "minta sequence 4"
3. Source kirim batch berikutnya (4, 5, 6)
4. Repeat...

**Window Size:**
- **Reliable connection** → Window besar (ratusan ribu packets)
- **Unreliable connection** (satellite) → Window kecil (ACK lebih sering)

```
Reliable:    [1,2,3,4,5...1000] → ACK 1001
Unreliable:  [1,2,3] → ACK 4 → [4,5,6] → ACK 7
```

---

### 6. Port Numbers

#### Well-Known Ports (0-1023)

| Port | Protocol | Application |
|------|----------|-------------|
| **20** | TCP | FTP - Data |
| **21** | TCP | FTP - Control |
| **22** | TCP | SSH (Secure Shell) |
| **23** | TCP | Telnet |
| **25** | TCP | SMTP (Email) |
| **53** | UDP/TCP | DNS |
| **67** | UDP | DHCP Server |
| **68** | UDP | DHCP Client |
| **69** | UDP | TFTP |
| **80** | TCP | HTTP (Web) |
| **110** | TCP | POP3 (Email) |
| **143** | TCP | IMAP (Email) |
| **161** | UDP | SNMP |
| **443** | TCP | HTTPS (Secure Web) |

#### Port Ranges:
| Range | Nama | Deskripsi |
|-------|------|-----------|
| 0-1023 | Well-Known | Standard services |
| 1024-49151 | Registered | Vendor applications |
| 49152-65535 | Dynamic/Private | Client source ports |

---

### 7. How Ports Work

**Server Side:**
- Server "listen" pada port tertentu
- Web server → listen port 80
- FTP server → listen port 21
- Satu server bisa menjalankan banyak service

**Client Side:**
- Client pakai **random port** (>1024) sebagai source
- Destination port = server's well-known port

**Contoh Web Request:**
```
Client → Server:
  Source Port: 5305 (random)
  Dest Port: 80 (web server)

Server → Client:
  Source Port: 80
  Dest Port: 5305 (return ke client)
```

---

### 8. Socket Pairs

**Socket = IP Address + Port Number**

Format: `IP:Port`

**Contoh:**
| Device | Socket |
|--------|--------|
| Client | 192.168.1.5:1099 |
| Server | 192.168.1.7:80 |

**Socket Pair:** `192.168.1.5:1099, 192.168.1.7:80`

**Dalam Frame:**
```
┌─────────────────────────────────────────────────────────────┐
│ Dest MAC │ Src MAC │ Src IP │ Dest IP │ Src Port │ Dst Port │
├─────────────────────────────────────────────────────────────┤
│ Layer 2  │ Layer 2 │ Layer 3│ Layer 3 │ Layer 4  │ Layer 4  │
└─────────────────────────────────────────────────────────────┘
```

**Contoh Multiple Connections:**
| Connection | Src Port | Dest Port | Service |
|------------|----------|-----------|---------|
| FTP | 1305 | 21 | File transfer |
| Web | 1099 | 80 | HTTP |

> Socket pairs memungkinkan **multiple applications** berkomunikasi **bersamaan** dari satu device!

---

### 9. netstat Command

**Fungsi:** Melihat active TCP connections

```cmd
C:\> netstat

Active Connections

  Proto  Local Address          Foreign Address        State
  TCP    192.168.1.124:3126     192.168.0.2:netbios    ESTABLISHED
  TCP    192.168.1.124:3158     207.138.126.152:http   ESTABLISHED
  TCP    192.168.1.124:3166     www.cisco.com:http     ESTABLISHED
```

**Options:**
| Command | Fungsi |
|---------|--------|
| `netstat` | Show active connections |
| `netstat -n` | Show numerical IP & port (tanpa resolve) |
| `netstat -a` | Show all connections & listening ports |
| `netstat -b` | Show executable name (program) |

**Security Use:**
> "Unexplained TCP connections can pose a major security threat!"
> 
> Pakai netstat untuk detect suspicious connections.

---

### 10. TCP/IP Model dengan Ports

```
┌─────────────────────────────────────────────────┐
│  APPLICATION LAYER                              │
│  ┌──────┐  ┌──────┐  ┌──────┐                  │
│  │ HTTP │  │ SMTP │  │ DNS  │                  │
│  │ :80  │  │ :25  │  │ :53  │                  │
│  └──┬───┘  └──┬───┘  └──┬───┘                  │
├─────┼─────────┼─────────┼───────────────────────┤
│  TRANSPORT LAYER                                │
│  ┌──┴─────────┴──┐  ┌───┴───┐                  │
│  │      TCP      │  │  UDP  │                  │
│  └───────┬───────┘  └───┬───┘                  │
├──────────┼──────────────┼───────────────────────┤
│  INTERNET LAYER                                 │
│  ┌───────┴──────────────┴───────┐              │
│  │            IP                │              │
│  └──────────────┬───────────────┘              │
├─────────────────┼───────────────────────────────┤
│  NETWORK ACCESS LAYER                           │
│  ┌──────────────┴───────────────┐              │
│  │          Network             │              │
│  └──────────────────────────────┘              │
└─────────────────────────────────────────────────┘
```

---

## 💡 Poin Penting

1. **TCP** = Reliable (ACK, sequence, retransmit)
2. **UDP** = Fast, unreliable (streaming, VoIP)
3. **Port < 1024** = Well-known (standard services)
4. **Port > 1024** = Dynamic (client source)
5. **Socket** = IP + Port
6. **Socket Pair** = Source socket + Dest socket
7. **netstat** = Security tool untuk cek connections
8. **DNS** pakai **UDP** untuk query, **TCP** untuk server-to-server

**Port Numbers untuk HAFAL:**
| Port | Service | Protocol |
|------|---------|----------|
| 21 | FTP | TCP |
| 22 | SSH | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | UDP/TCP |
| 80 | HTTP | TCP |
| 443 | HTTPS | TCP |

**CyberSec Relevance:**
- `netstat` untuk detect malware connections
- Unusual ports → possible backdoor
- Port scanning → reconnaissance technique
- Firewall rules based on port numbers
