# Modul 16: Application Layer Services

**Modul:** 16 - Application Layer Services  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Client-Server Model** = Client request, Server respond
- **DNS** = Resolve domain name → IP address
- **HTTP/HTTPS** = Web browsing (port 80/443)
- **FTP** = File transfer (port 20/21)
- **Telnet/SSH** = Remote access (port 23/22)
- **Email** = SMTP (kirim), POP3/IMAP (terima)

---

## 📚 Materi

### 1. Client-Server Relationship

**Definisi:**
- **Server** = Host yang menjalankan software untuk menyediakan layanan
- **Client** = Host yang request layanan dari server

**Contoh layanan:**
- Web server → menyediakan halaman web
- Email server → menyimpan dan meneruskan email
- FTP server → menyediakan file untuk diunduh

```
┌────────┐         Internet         ┌────────┐
│ Client │ ◄─────────────────────► │ Server │
└────────┘                          └────────┘
  Request                            Response
```

---

### 2. URI, URN, dan URL

**URI (Uniform Resource Identifier):**
Identifikasi resource di network

| Komponen | Contoh | Keterangan |
|----------|--------|------------|
| **Protocol/Scheme** | `https://` | HTTP, FTP, SFTP, mailto |
| **Hostname** | `www.example.com` | Domain name |
| **Path** | `/author/book.html` | Lokasi file |
| **Fragment** | `#page155` | Bagian spesifik |

**Contoh lengkap:**
```
https://www.example.com/author/book.html#page155
└─┬─┘   └──────┬──────┘└──────┬───────┘└───┬───┘
Protocol   Hostname        Path       Fragment
```

**Perbedaan:**
- **URL** = Protocol + Hostname + Path (lokasi lengkap)
- **URN** = Hostname + Path (tanpa protocol)

---

### 3. Web Client & Server Interaction

**Proses request halaman web:**

```
┌────────┐                                    ┌────────────┐
│ Client │                                    │ Web Server │
└───┬────┘                                    └─────┬──────┘
    │                                               │
    │  1. DNS Lookup                                │
    │  "www.learnip.com = ?"                        │
    │ ─────────────────────► DNS Server             │
    │ ◄───────────────────── 172.16.10.50           │
    │                                               │
    │  2. TCP Connection (3-way handshake)          │
    │ ────────────────────────────────────────────► │
    │                                               │
    │  3. HTTP Request (port 80)                    │
    │  GET /index.html                              │
    │ ────────────────────────────────────────────► │
    │                                               │
    │  4. HTTP Response                             │
    │  HTML code                                    │
    │ ◄──────────────────────────────────────────── │
    │                                               │
    │  5. Browser render HTML → webpage             │
```

**Socket:**
- Kombinasi IP:Port yang mengidentifikasi satu conversation
- Contoh: `192.168.10.15:5507` → `172.16.10.50:80`

---

### 4. DNS (Domain Name System)

**Fungsi:** Mengubah domain name → IP address

**Proses DNS Lookup:**
```
User ketik: www.cisco.com
       │
       ▼
┌─────────────┐     "www.cisco.com = ?"     ┌────────────┐
│   Client    │ ──────────────────────────► │ DNS Server │
│             │ ◄────────────────────────── │            │
└─────────────┘     "172.230.155.162"       └────────────┘
       │
       ▼
Client bisa akses web server dengan IP
```

**Command nslookup:**
```cmd
C:\> nslookup
> www.cisco.com
Server:  UnKnown
Address:  10.10.10.1

Non-authoritative answer:
Name:    e2867.dsca.akamaiedge.net
Address: 172.230.155.162
Aliases: www.cisco.com
```

**Kenapa perlu DNS?**
- Manusia lebih mudah ingat nama daripada angka
- Network hanya memproses IP address, bukan domain name

---

### 5. HTTP dan HTML

| Istilah | Kepanjangan | Fungsi |
|---------|-------------|--------|
| **HTTP** | Hypertext Transfer Protocol | Aturan transfer data web |
| **HTML** | Hypertext Markup Language | Coding untuk tampilan web |
| **HTTPS** | HTTP Secure | HTTP + enkripsi (port 443) |

**HTTP Ports:**
| Protocol | Port | Keamanan |
|----------|------|----------|
| HTTP | 80 | ❌ Tidak terenkripsi |
| HTTPS | 443 | ✅ Terenkripsi (SSL/TLS) |

**Proses:**
1. Client kirim **HTTP request** ke server (port 80/443)
2. Server kirim **HTML code** sebagai response
3. Browser **render** HTML menjadi tampilan visual

---

### 6. FTP (File Transfer Protocol)

**Fungsi:** Transfer file antara client dan server

**Ports:**
| Port | Fungsi |
|------|--------|
| **21** | Control connection (command) |
| **20** | Data connection (transfer file) |

**Proses FTP:**
```
┌────────┐                              ┌────────────┐
│ Client │                              │ FTP Server │
└───┬────┘                              └─────┬──────┘
    │                                         │
    │  1. Control Connection (port 21)        │
    │  Login: username/password               │
    │ ──────────────────────────────────────► │
    │                                         │
    │  2. Data Connection (port 20)           │
    │  Transfer file                          │
    │ ◄─────────────────────────────────────► │
```

**FTP Commands:**
| Command | Fungsi |
|---------|--------|
| `put` | Upload file ke server |
| `get` | Download file dari server |
| `dir` | List isi directory |
| `delete` | Hapus file |
| `rename` | Rename file |
| `quit` | Keluar |

---

### 7. Virtual Terminal (Telnet & SSH)

**Fungsi:** Remote access ke device lain

| Protocol | Port | Keamanan |
|----------|------|----------|
| **Telnet** | 23 | ❌ Plain text (tidak aman) |
| **SSH** | 22 | ✅ Encrypted (aman) |

**Telnet:**
- Akses remote seperti duduk di depan device
- **TIDAK AMAN** - data dikirim plain text
- Password bisa di-sniff oleh attacker

**SSH (Secure Shell):**
- Sama seperti Telnet tapi **terenkripsi**
- Best practice: **SELALU gunakan SSH**

**Perbandingan:**
```
TELNET (Tidak Aman):
Attacker sniff → Username: cisco, Password: cisco123 (TERBACA!)

SSH (Aman):
Attacker sniff → hgdhxcvghdearwwtdyt764cb (TERENKRIPSI!)
```

**Syntax SSH:**
```cmd
C:\> ssh -l admin 64.100.1.1
Password: ****
HQ#
```

---

### 8. Email Protocols

**3 Protocol utama:**

| Protocol | Port | Fungsi | Arah |
|----------|------|--------|------|
| **SMTP** | 25 | Kirim email | Client → Server, Server → Server |
| **POP3** | 110 | Terima email (download & hapus) | Server → Client |
| **IMAP4** | 143 | Terima email (tetap di server) | Server → Client |

**Proses kirim email:**
```
┌────────┐  SMTP   ┌─────────────┐  SMTP   ┌─────────────┐  POP3/IMAP  ┌───────────┐
│ Sender │ ──────► │ Mail Server │ ──────► │ Mail Server │ ──────────► │ Recipient │
│        │         │    ISP A    │         │    ISP B    │             │           │
└────────┘         └─────────────┘         └─────────────┘             └───────────┘
```

**Perbedaan POP3 vs IMAP:**

| Aspek | POP3 | IMAP |
|-------|------|------|
| **Port** | 110 | 143 |
| **Email di server** | Dihapus setelah download | Tetap tersimpan |
| **Akses multi-device** | ❌ Sulit | ✅ Mudah |
| **Offline access** | ✅ Ya | ❌ Butuh koneksi |

---

### 9. Text Messaging & VoIP

**Text Messaging (Instant Messaging):**
- Real-time communication
- Peer-to-peer technology
- Contoh: WhatsApp, Telegram, Teams, Webex

**VoIP (Voice over IP):**
- Telepon melalui internet
- Mengubah suara analog → digital → IP packets
- Contoh: Skype, Zoom, WhatsApp Call

---

### 10. Common Application Services Summary

| Service | Protocol | Port | Transport |
|---------|----------|------|-----------|
| DNS | DNS | 53 | UDP/TCP |
| Web | HTTP | 80 | TCP |
| Secure Web | HTTPS | 443 | TCP |
| FTP Control | FTP | 21 | TCP |
| FTP Data | FTP | 20 | TCP |
| Telnet | Telnet | 23 | TCP |
| SSH | SSH | 22 | TCP |
| Email Send | SMTP | 25 | TCP |
| Email Receive | POP3 | 110 | TCP |
| Email Receive | IMAP4 | 143 | TCP |
| DHCP Server | DHCP | 67 | UDP |
| DHCP Client | DHCP | 68 | UDP |

---

## 💡 Poin Penting

1. **DNS** resolve domain → IP sebelum komunikasi
2. **HTTP** (80) tidak aman, **HTTPS** (443) terenkripsi
3. **FTP** pakai 2 port: 21 (control), 20 (data)
4. **Telnet** TIDAK aman → selalu pakai **SSH**
5. **SMTP** untuk kirim email, **POP3/IMAP** untuk terima
6. **Socket** = IP:Port (identifikasi conversation)

**Port Numbers untuk HAFAL:**
```
21 = FTP (control)
22 = SSH ✅
23 = Telnet ❌
25 = SMTP
53 = DNS
80 = HTTP
110 = POP3
143 = IMAP
443 = HTTPS ✅
```
