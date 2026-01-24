# Tambahan: DNS Protocol & DNS Attacks

**Topik:** Domain Name System  
**Fokus:** Materi yang WAJIB untuk Cybersecurity  
**Status:** ✅ Selesai

---

## 📌 Ringkasan Konsep Utama

### DNS = Buku Telepon Internet

```
Kamu mau telepon Google...

Kamu: "Nomor telepon Google berapa ya?"
DNS:  "Google = 142.250.185.78"
Kamu: "Makasih!" *telepon 142.250.185.78*

Tanpa DNS, pengguna harus menghafal semua IP
```

### Kenapa Perlu DNS?

```
Dengan DNS:    google.com     ✅ Gampang diingat!
Tanpa DNS:     142.250.185.78 ❌ Siapa yang hafal?

Instagram:     157.240.214.174
Facebook:      157.240.1.35
YouTube:       172.217.194.91
Netflix:       52.4.128.87

Tidak praktis jika harus menghafal semua
```

### Cara Kerja DNS (Seperti Tanya Alamat)

```
Kamu mau ke rumah "Budi" tapi tidak tahu alamatnya...

1. Tanya Ibu (Cache lokal)
   Ibu: "Tidak tahu"
   
2. Tanya Pak RT (DNS Resolver/ISP)
   Pak RT: "Coba tanya ke kantor kelurahan"
   
3. Tanya Kelurahan (Root DNS)
   Kelurahan: "Budi yang mana? Yang di .com? Tanya sana"
   
4. Tanya bagian .com (TLD DNS)
   .com: "Oh Budi.com? Itu di server X"
   
5. Tanya Server X (Authoritative DNS)
   Server X: "Budi.com = 192.168.1.50"

Proses selesai, alamat ditemukan
```

### DNS Cache = Catatan Kecil

```
Sudah pernah buka google.com?
Komputer catat: "google.com = 142.250.185.78"

Buka lagi? Tidak perlu tanya DNS!
Langsung dari catatan = LEBIH CEPAT

Lihat cache: ipconfig /displaydns (Windows)
Hapus cache: ipconfig /flushdns
```

### DNS Spoofing = Kasih Info Palsu

```
Kamu: "google.com alamatnya mana?"
Hacker: "192.168.1.666!" (alamat PALSU)

Kamu pikir buka Google, padahal ke website HACKER!
Bisa untuk:
- Phishing (curi password)
- Malware distribution
- Redirect ke iklan
```

### DNS paling populer:

```
Google DNS:     8.8.8.8 dan 8.8.4.4
Cloudflare:     1.1.1.1 (cepat + privasi)
OpenDNS:        208.67.222.222

Pilih yang terpercaya untuk keamanan!
```

---

## 📚 Apa itu DNS? (Detail Teknis)

**DNS = Domain Name System**

### Fungsi Utama:
Menerjemahkan **nama domain** menjadi **IP address**.

```
google.com  →  142.250.185.78
facebook.com → 157.240.1.35
```

### Kenapa Perlu DNS?
- Manusia lebih mudah ingat **nama** daripada angka
- IP address bisa berubah, nama tetap sama
- Memungkinkan load balancing (1 nama → banyak IP)

---

## 🏗️ Hierarki DNS

```
┌─────────────────────────────────────────────────────┐
│                  DNS HIERARCHY                       │
├─────────────────────────────────────────────────────┤
│                                                     │
│                    . (Root)                         │
│                       │                             │
│         ┌─────────────┼─────────────┐               │
│         │             │             │               │
│        .com          .org          .id              │
│         │             │             │               │
│    ┌────┴────┐       │        ┌────┴────┐          │
│    │         │       │        │         │          │
│  google   facebook  wikipedia  go      detik       │
│    │         │       │        │         │          │
│  www.    www.     www.     www.      www.          │
│                                                     │
│  FQDN: www.google.com.                              │
│        (ada titik di akhir = root)                  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### Komponen:
| Level | Contoh | Penjelasan |
|-------|--------|------------|
| **Root** | . | Puncak hierarki |
| **TLD** | .com, .org, .id | Top Level Domain |
| **SLD** | google, facebook | Second Level Domain |
| **Subdomain** | www, mail, api | Bagian dari domain |

### FQDN (Fully Qualified Domain Name):
```
www.google.com.
│   │      │  │
│   │      │  └─ Root (biasanya tidak ditulis)
│   │      └──── TLD
│   └─────────── SLD
└─────────────── Subdomain
```

---

## 🔄 DNS Query Process

### Recursive Query (Paling Umum)

```
┌────────────────────────────────────────────────────────────────┐
│                   DNS RESOLUTION PROCESS                        │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│   Client          Local DNS       Root    .com      google     │
│      │            (Resolver)       DNS     DNS       DNS       │
│      │                │             │       │         │        │
│  1.  │── "www.google.com?" ────────>│       │         │        │
│      │                │             │       │         │        │
│  2.  │                │── Query ───>│       │         │        │
│      │                │             │       │         │        │
│  3.  │                │<─ ".com NS" ─│       │         │        │
│      │                │             │       │         │        │
│  4.  │                │───── Query ────────>│         │        │
│      │                │             │       │         │        │
│  5.  │                │<── "google.com NS" ──│         │        │
│      │                │             │       │         │        │
│  6.  │                │─────────── Query ───────────>│        │
│      │                │             │       │         │        │
│  7.  │                │<────────── "142.250.185.78" ──│        │
│      │                │             │       │         │        │
│  8.  │<─ "142.250.185.78" ──────────│       │         │        │
│      │                │             │       │         │        │
│      │   [Client sekarang tahu IP google.com]         │        │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

### Langkah-langkah:
1. Client tanya Local DNS (resolver)
2. Local DNS tanya Root DNS
3. Root DNS kasih referral ke .com DNS
4. Local DNS tanya .com DNS
5. .com DNS kasih referral ke google.com DNS
6. Local DNS tanya google.com DNS
7. google.com DNS jawab dengan IP
8. Local DNS kasih jawaban ke client

---

## 📋 DNS Record Types

| Record | Fungsi | Contoh |
|--------|--------|--------|
| **A** | Domain → IPv4 | google.com → 142.250.185.78 |
| **AAAA** | Domain → IPv6 | google.com → 2404:6800:4003:c00::71 |
| **CNAME** | Alias ke domain lain | www.google.com → google.com |
| **MX** | Mail server | google.com → mail.google.com |
| **NS** | Name server | google.com → ns1.google.com |
| **TXT** | Text info | SPF, DKIM untuk email |
| **PTR** | IP → Domain (reverse) | 142.250.185.78 → google.com |
| **SOA** | Start of Authority | Info tentang zone |

---

## 🔴 DNS Attacks

### 1. DNS Spoofing / Cache Poisoning

**Apa itu?**
Attacker memasukkan **record DNS palsu** ke cache resolver.

```
┌────────────────────────────────────────────────────┐
│           DNS CACHE POISONING                      │
├────────────────────────────────────────────────────┤
│                                                    │
│  Victim         Local DNS         Attacker        │
│    │               │                  │           │
│    │── "bank.com?" ─>│                  │           │
│    │               │                  │           │
│    │               │── Query ke ─────>│           │
│    │               │   internet       │           │
│    │               │                  │           │
│    │               │<── Fake Response ─│           │
│    │               │   "bank.com =     │           │
│    │               │    10.10.10.10    │           │
│    │               │    (Attacker IP)" │           │
│    │               │                  │           │
│    │               │ [Cache poisoned!] │           │
│    │               │                  │           │
│    │<─ "10.10.10.10" ─│                  │           │
│    │               │                  │           │
│    │   Victim pergi ke site attacker!  │           │
│    │   (Phishing site)                 │           │
│                                                    │
└────────────────────────────────────────────────────┘
```

**Impact:**
- User diarahkan ke **phishing site**
- Bisa mencuri credentials
- Menyebar malware

---

### 2. DNS Hijacking

**Apa itu?**
Attacker mengubah setting DNS di device/router victim.

**Metode:**
- Malware mengubah DNS setting
- Compromise router, ubah DHCP DNS
- Rogue DHCP server

```
Legitimate: DNS = 8.8.8.8 (Google)
Hijacked:   DNS = 10.10.10.10 (Attacker)

Semua DNS query victim dikontrol attacker!
```

---

### 3. DNS Amplification Attack (DDoS)

**Apa itu?**
Menggunakan DNS server untuk **memperbesar** traffic DDoS.

```
┌────────────────────────────────────────────────────┐
│           DNS AMPLIFICATION ATTACK                 │
├────────────────────────────────────────────────────┤
│                                                    │
│  Attacker        Open DNS         Victim          │
│      │           Resolvers        (Target)         │
│      │               │                │           │
│  1.  │── Small Query ─>│                │           │
│      │   (Spoofed src: │                │           │
│      │    Victim IP)   │                │           │
│      │               │                │           │
│  2.  │               │── BIG Response ──>│           │
│      │               │   (50x larger!)  │           │
│      │               │                │           │
│      │   Attacker kirim 1 MB            │           │
│      │   Victim terima 50 MB!           │           │
│      │                                  │           │
│      │   Ribuan DNS server = MASSIVE DDoS!         │
│                                                    │
└────────────────────────────────────────────────────┘
```

**Kenapa "Amplification"?**
- Query DNS kecil (~60 bytes)
- Response bisa besar (~3000 bytes)
- Amplification factor: **50x atau lebih**

---

### 4. DNS Tunneling

**Apa itu?**
Menyembunyikan traffic di dalam **DNS queries** untuk bypass firewall.

```
Normal DNS: google.com
Tunneling:  aGVsbG8gd29ybGQ=.evil.com
            └── Data encoded dalam subdomain
```

**Use case attacker:**
- Exfiltrate data dari network
- C2 (Command & Control) communication
- Bypass firewall yang allow DNS

---

## 🛡️ DNS Security

### 1. DNSSEC (DNS Security Extensions)
- **Digital signature** untuk DNS records
- Memastikan response tidak dimanipulasi
- Mencegah cache poisoning

### 2. DNS over HTTPS (DoH)
- DNS query melalui HTTPS (port 443)
- Encrypted, ISP tidak bisa lihat
- Privacy protection

### 3. DNS over TLS (DoT)
- DNS query dienkripsi dengan TLS
- Port 853
- Alternative ke DoH

### 4. Use Trusted DNS
| Provider | Primary | Secondary |
|----------|---------|-----------|
| Google | 8.8.8.8 | 8.8.4.4 |
| Cloudflare | 1.1.1.1 | 1.0.0.1 |
| OpenDNS | 208.67.222.222 | 208.67.220.220 |
| Quad9 | 9.9.9.9 | 149.112.112.112 |

### 5. Monitor DNS Traffic
- Unusual query patterns
- High volume of NXDOMAIN
- Long subdomain names (tunneling indicator)

---

## 💻 DNS Commands

### Windows
```cmd
# Lihat DNS server
ipconfig /all

# Query DNS
nslookup google.com

# Query record spesifik
nslookup -type=MX google.com
nslookup -type=NS google.com

# Clear DNS cache
ipconfig /flushdns

# Lihat DNS cache
ipconfig /displaydns
```

### Linux
```bash
# Query DNS
dig google.com
dig google.com MX
dig google.com NS

# Simple query
host google.com

# Reverse lookup
dig -x 142.250.185.78

# Trace DNS resolution
dig +trace google.com

# Clear cache (systemd)
sudo systemd-resolve --flush-caches
```

---

## 💡 Poin Penting

1. **DNS** = Domain name → IP address
2. **Port:** UDP 53 (dan TCP 53 untuk zone transfer)
3. **Hierarki:** Root → TLD → SLD → Subdomain
4. **A Record** = IPv4, **AAAA** = IPv6, **MX** = Mail
5. **DNS Spoofing** = Poison cache dengan fake record
6. **DNS Amplification** = DDoS dengan response besar
7. **DNS Tunneling** = Hide data dalam DNS query
8. **Defense:** DNSSEC, DoH/DoT, Trusted DNS

---

## 📝 Quick Reference

```
┌─────────────────────────────────────┐
│         DNS CHEAT SHEET             │
├─────────────────────────────────────┤
│  Port: UDP/TCP 53                   │
├─────────────────────────────────────┤
│  Record Types:                      │
│  A     - IPv4 address               │
│  AAAA  - IPv6 address               │
│  CNAME - Alias                      │
│  MX    - Mail server                │
│  NS    - Name server                │
│  TXT   - Text (SPF, DKIM)           │
├─────────────────────────────────────┤
│  Commands:                          │
│  nslookup domain.com                │
│  dig domain.com                     │
│  host domain.com                    │
│  ipconfig /flushdns                 │
├─────────────────────────────────────┤
│  Attacks:                           │
│  • Cache Poisoning                  │
│  • DNS Hijacking                    │
│  • Amplification DDoS               │
│  • DNS Tunneling                    │
├─────────────────────────────────────┤
│  Trusted DNS:                       │
│  Google:     8.8.8.8                │
│  Cloudflare: 1.1.1.1                │
│  Quad9:      9.9.9.9                │
└─────────────────────────────────────┘
```

---

**Terkait:** Modul 5 (Application Layer), Tambahan Ports (Port 53)
