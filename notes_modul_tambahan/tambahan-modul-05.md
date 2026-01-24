# Tambahan Modul 5: TCP/UDP & Port Numbers

**Pelengkap:** Modul 5 - Communication Principles  
**Fokus:** Materi yang WAJIB untuk Cybersecurity  
**Status:** ✅ Selesai

---

## 📌 Ringkasan Konsep Utama

### TCP vs UDP = Kirim Paket

**TCP = Kirim paket via JNE (Ada Resi)**
```
Kamu kirim → Kurir konfirmasi terima → Kamu dapat notif "paket sampai"
Kalau hilang? → Dikirim ulang

✅ Pasti sampai
✅ Ada tracking  
❌ Lebih lama
```

**UDP = Lempar surat dari jendela**
```
Kamu lempar → Selesai, tidak ada konfirmasi
Sampai atau tidak? → Tidak tahu, tidak peduli

✅ Cepat
❌ Tidak ada jaminan sampai
```

### 3-Way Handshake = Kenalan Dulu

```
Kamu:  "Halo, bisa bicara?" ----→ (SYN)
Teman: "Bisa, kamu dengar aku?" ← (SYN-ACK)  
Kamu:  "Iya, dengar!" ----------→ (ACK)

Baru bisa ngobrol!
```

### Port = Nomor Pintu di Gedung

```
IP Address = Alamat gedung (Jl. Sudirman No. 10)
Port       = Nomor kamar (Kamar 80, Kamar 443, dll)

Mau ke website? → Ketuk pintu kamar 80 (HTTP) atau 443 (HTTPS)
Mau kirim email? → Ketuk pintu kamar 25 (SMTP)
```

### Port Wajib Hafal (10 Saja!)

```
80   = Website biasa (HTTP)
443  = Website aman (HTTPS) 🔒
22   = Remote server (SSH)
21   = Download file (FTP)
53   = DNS (nama → IP)
25   = Kirim email (SMTP)
23   = Telnet (JANGAN PAKAI! ❌)
445  = Sharing Windows (HATI-HATI ransomware!)
3389 = Remote Desktop Windows
3306 = Database MySQL
```

---

## 📚 TCP vs UDP (Detail Teknis)

### Perbandingan Lengkap

| Aspek | TCP | UDP |
|-------|-----|-----|
| **Nama** | Transmission Control Protocol | User Datagram Protocol |
| **Koneksi** | Connection-oriented | Connectionless |
| **Reliability** | ✅ Reliable (ada acknowledgment) | ❌ Unreliable (no guarantee) |
| **Ordering** | ✅ Data terurut | ❌ Tidak dijamin urut |
| **Speed** | Lebih lambat | Lebih cepat |
| **Header Size** | 20-60 bytes | 8 bytes |
| **Error Checking** | ✅ Ya + retransmission | ✅ Ya, tapi no retransmission |
| **Flow Control** | ✅ Ya | ❌ Tidak |
| **Use Case** | Web, Email, File Transfer | Streaming, Gaming, DNS |

---

## 🤝 TCP 3-Way Handshake

### Proses Koneksi TCP

```
Client                          Server
   |                               |
   |-------- SYN (seq=100) ------->|  1. Client minta koneksi
   |                               |
   |<--- SYN-ACK (seq=300,ack=101)-|  2. Server setuju + acknowledge
   |                               |
   |-------- ACK (ack=301) ------->|  3. Client confirm
   |                               |
   |===== KONEKSI ESTABLISHED =====|
```

**Penjelasan:**
1. **SYN** (Synchronize): Client kirim request koneksi
2. **SYN-ACK**: Server terima dan balas konfirmasi
3. **ACK** (Acknowledge): Client konfirmasi, koneksi terbuka

### 🔴 Security Risk: SYN Flood Attack

```
Attacker                        Server
   |                               |
   |-------- SYN ---------------->|
   |-------- SYN ---------------->|  Banyak SYN tanpa ACK
   |-------- SYN ---------------->|
   |-------- SYN ---------------->|
   |                               |
   |      Server kehabisan        |
   |      resources (RAM)         |
   |      = DENIAL OF SERVICE     |
```

**Cara kerja:**
- Attacker kirim banyak SYN tanpa menyelesaikan handshake
- Server menunggu ACK yang tidak pernah datang
- Resource server habis → server down

**Defense:**
- SYN cookies
- Rate limiting
- Firewall rules

---

## 🔌 TCP Connection Termination (4-Way)

```
Client                          Server
   |                               |
   |-------- FIN ---------------->|  1. Client mau tutup
   |<------- ACK -----------------|  2. Server acknowledge
   |<------- FIN -----------------|  3. Server juga tutup
   |-------- ACK ---------------->|  4. Client acknowledge
   |                               |
   |===== KONEKSI CLOSED =========|
```

---

## 📍 Port Numbers

### Kategori Port

| Range | Nama | Keterangan |
|-------|------|------------|
| **0-1023** | Well-Known Ports | Untuk layanan standar (HTTP, FTP, SSH) |
| **1024-49151** | Registered Ports | Untuk aplikasi tertentu |
| **49152-65535** | Dynamic/Private | Untuk koneksi sementara (client side) |

---

## 🔴 PORT WAJIB HAFAL (Interview CyberSec!)

### Networking & Remote Access

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **20** | TCP | FTP Data | ❌ Clear text |
| **21** | TCP | FTP Control | ❌ Clear text, brute force target |
| **22** | TCP | SSH | ✅ Encrypted, tapi brute force target |
| **23** | TCP | Telnet | ❌ Clear text, JANGAN DIPAKAI |
| **3389** | TCP | RDP | ⚠️ Remote Desktop, sering di-attack |

### Web Services

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **80** | TCP | HTTP | ❌ Unencrypted web |
| **443** | TCP | HTTPS | ✅ Encrypted web (TLS/SSL) |
| **8080** | TCP | HTTP Proxy | Alternative HTTP port |
| **8443** | TCP | HTTPS Alt | Alternative HTTPS port |

### Email

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **25** | TCP | SMTP | Email sending, spam target |
| **110** | TCP | POP3 | ❌ Clear text email retrieval |
| **143** | TCP | IMAP | ❌ Clear text email access |
| **465** | TCP | SMTPS | ✅ Encrypted SMTP |
| **587** | TCP | SMTP Submission | Modern email sending |
| **993** | TCP | IMAPS | ✅ Encrypted IMAP |
| **995** | TCP | POP3S | ✅ Encrypted POP3 |

### DNS & DHCP

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **53** | TCP/UDP | DNS | DNS poisoning, amplification |
| **67** | UDP | DHCP Server | DHCP spoofing |
| **68** | UDP | DHCP Client | - |

### Database

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **1433** | TCP | MS SQL | Database attacks |
| **3306** | TCP | MySQL | Database attacks |
| **5432** | TCP | PostgreSQL | Database attacks |
| **27017** | TCP | MongoDB | Sering misconfigured |

### Other Important

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| **139** | TCP | NetBIOS | Windows sharing, SMB attacks |
| **445** | TCP | SMB | ⚠️ WannaCry, EternalBlue! |
| **161/162** | UDP | SNMP | Network monitoring, info leak |
| **389** | TCP | LDAP | Directory services |
| **636** | TCP | LDAPS | ✅ Encrypted LDAP |

---

## 🎯 Port Scanning (Intro)

### Apa itu Port Scanning?
Teknik untuk menemukan port yang **terbuka** pada target.

### Tools:
- **nmap** (paling populer)
- **masscan** (super fast)
- **netcat**

### Contoh nmap:
```bash
# Scan port umum
nmap 192.168.1.1

# Scan semua port
nmap -p- 192.168.1.1

# Scan port spesifik
nmap -p 22,80,443 192.168.1.1

# Detect service version
nmap -sV 192.168.1.1
```

### Port States:
| State | Artinya |
|-------|---------|
| **Open** | Port aktif, ada service |
| **Closed** | Port tidak ada service |
| **Filtered** | Firewall memblok |

---

## 🔴 Security Implications

### 1. Open Port = Potential Attack Surface
Setiap port terbuka adalah **pintu masuk** potensial.

### 2. Unnecessary Services = Risk
```
❌ Port 23 (Telnet) terbuka = BAHAYA
✅ Tutup port yang tidak dipakai
```

### 3. Port-based Attacks

| Attack | Target Port | Deskripsi |
|--------|-------------|-----------|
| **SSH Brute Force** | 22 | Tebak password SSH |
| **SQL Injection** | 1433, 3306 | Exploit database |
| **SMB Exploits** | 445 | WannaCry, EternalBlue |
| **DNS Amplification** | 53 | DDoS menggunakan DNS |

---

## 💡 Poin Penting

1. **TCP** = reliable, connection-oriented (web, email)
2. **UDP** = fast, connectionless (streaming, gaming, DNS)
3. **3-Way Handshake** = SYN → SYN-ACK → ACK
4. **SYN Flood** = DDoS dengan incomplete handshake
5. **Well-Known Ports** = 0-1023 (HTTP=80, HTTPS=443, SSH=22)
6. **Port terbuka = attack surface** → tutup yang tidak perlu
7. **Port 445 (SMB)** = target favorit ransomware

---

## 📝 Quick Reference Card

```
┌─────────────────────────────────────┐
│         PORTS WAJIB HAFAL           │
├─────────────────────────────────────┤
│ 21  FTP      │ 443 HTTPS            │
│ 22  SSH      │ 445 SMB ⚠️           │
│ 23  Telnet ❌ │ 3389 RDP             │
│ 25  SMTP     │ 53  DNS              │
│ 80  HTTP     │ 3306 MySQL           │
├─────────────────────────────────────┤
│     TCP = Reliable (Handshake)      │
│     UDP = Fast (No Handshake)       │
└─────────────────────────────────────┘
```

---

**Terkait:** Modul 5 (OSI Model), Modul 9 (IP Addressing)
