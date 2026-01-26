# Tambahan Modul 12: Gateway & NAT Security

**Pelengkap:** Modul 12 - Gateways to Other Networks  
**Fokus:** Materi yang WAJIB untuk Cybersecurity  
**Status:** ✅ Selesai

---

## 📌 Ringkasan Konsep Utama

### Gateway = Pintu Keluar yang Bisa Diintai

```
Semua traffic keluar rumah PASTI lewat pintu depan...

Kalau hacker berdiri di pintu? → Lihat SEMUA yang keluar masuk!

Gateway = titik strategis untuk:
- Sniffing (nguping traffic)
- MITM (man-in-the-middle)
- Traffic interception
```

### NAT = Topeng untuk Sembunyi

```
Tanpa NAT:
Internet bisa lihat: 192.168.1.10, 192.168.1.11, 192.168.1.12...
"Oh ada 3 komputer di dalam!"

Dengan NAT:
Internet hanya lihat: 203.0.113.5 (1 IP saja)
"Entah ada berapa di dalam..."

NAT = Menyembunyikan struktur internal
```

---

## 🔐 Gateway Security

### Attack Vectors

| Serangan | Cara Kerja |
|----------|------------|
| **Rogue Gateway** | Attacker pasang gateway palsu, traffic lewat dia |
| **ARP Spoofing** | Claim sebagai gateway → intercept traffic |
| **Gateway Enumeration** | Scan untuk identifikasi network boundary |
| **DHCP Spoofing** | Beri gateway palsu via fake DHCP |

### Rogue Gateway Attack

```
Normal:
PC → Gateway (192.168.1.1) → Internet

Attack:
PC → HACKER (192.168.1.100) → Gateway → Internet
         ↓
    Baca semua traffic!
```

**Cara kerja:**
1. Attacker connect ke network
2. Kirim ARP reply palsu: "Gateway ada di MAC saya!"
3. PC percaya → kirim traffic ke attacker
4. Attacker forward ke gateway asli (supaya tidak curiga)
5. Attacker baca semua traffic yang lewat

---

## 🔐 NAT Security

### Keuntungan Security NAT

| Aspek | Penjelasan |
|-------|------------|
| **IP Hiding** | Internal IP tidak terlihat dari luar |
| **Reduced Attack Surface** | Hanya 1 IP yang bisa di-scan dari luar |
| **No Direct Access** | Tidak bisa langsung akses device internal |

### Keterbatasan NAT (Bukan Firewall!)

```
NAT bisa:
✅ Sembunyikan IP internal
✅ Persulit direct attack dari luar

NAT TIDAK bisa:
❌ Filter malicious traffic
❌ Block port tertentu
❌ Detect intrusion
❌ Protect jika attacker sudah di dalam

NAT ≠ Firewall!
```

### NAT Bypass Techniques

| Teknik | Cara |
|--------|------|
| **Reverse Shell** | Korban connect keluar ke attacker |
| **Port Forwarding Abuse** | Exploit misconfigured port forward |
| **UPnP Exploitation** | Auto port forward tanpa approval |
| **Internal Pivot** | Compromise 1 device, scan internal dari sana |

---

## 🛡️ Mitigasi & Defense

### Protect Gateway

| Defense | Implementasi |
|---------|--------------|
| **Static ARP** | Hardcode MAC gateway di device penting |
| **ARP Inspection** | Switch validasi ARP packets |
| **802.1X** | Authentication sebelum masuk network |
| **Network Segmentation** | Pisahkan critical assets |

### Strengthen NAT

| Defense | Implementasi |
|---------|--------------|
| **Disable UPnP** | Matikan auto port forward |
| **Firewall Rules** | Tambahkan filtering, jangan rely NAT saja |
| **Audit Port Forwards** | Review manual port forwards |
| **Egress Filtering** | Monitor outbound connections |

---

## 💡 Poin Penting untuk Interview

1. **Gateway** = titik strategis untuk MITM attack
2. **ARP spoofing** = cara paling umum hijack gateway
3. **NAT** menyembunyikan tapi **bukan firewall**
4. Attacker di dalam network bisa **bypass NAT**
5. Defense: **Static ARP + Firewall + Segmentation**
