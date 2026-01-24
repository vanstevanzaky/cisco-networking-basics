# Modul 2: Network Components, Types, and Connections

**Modul:** 2 - Network Components, Types, and Connections  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- Model jaringan: Client-Server vs Peer-to-Peer
- NIC memiliki MAC address sebagai identitas hardware
- Kabel: Straight-through (device berbeda), Crossover (device sejenis)

---

## 📚 Materi

### 1. Client dan Server

| Peran | Fungsi | Contoh |
|-------|--------|--------|
| **Client** | Meminta layanan | Web browser |
| **Server** | Menyediakan layanan | Web server |
| **Peer** | Keduanya sekaligus | File sharing P2P |

**Model Jaringan:**
| Model | Kelebihan | Kekurangan |
|-------|-----------|------------|
| Client-Server | Scalable, secure | Butuh dedicated server |
| Peer-to-Peer | Sederhana, murah | Tidak scalable |

---

### 2. Network Interface Card (NIC)

- Menghubungkan device ke jaringan
- Memiliki **MAC address** (identitas hardware unik)
- Bisa wired (Ethernet) atau wireless (Wi-Fi)

---

### 3. Jenis Kabel

| Kabel | Penggunaan | Contoh |
|-------|------------|--------|
| **Straight-through** | Device berbeda | PC ↔ Switch |
| **Crossover** | Device sejenis | PC ↔ PC |
| **Console/Rollover** | Konfigurasi | PC ↔ Router console |

---

### 4. Network Devices

| Device | Layer | Fungsi |
|--------|-------|--------|
| **Switch** | 2 (Data Link) | Forward frame berdasarkan MAC |
| **Router** | 3 (Network) | Forward packet berdasarkan IP |
| **Access Point** | 2 | Bridge wireless ↔ wired |
| **Firewall** | 3-7 | Filter traffic, keamanan |

---

## 💡 Poin Penting

1. **Client** meminta, **Server** menyediakan layanan
2. **NIC** punya MAC address unik dari pabrik
3. **Straight-through** = PC ke Switch (device berbeda)
4. **Crossover** = PC ke PC (device sejenis)
5. **Switch** = Layer 2, pakai MAC address
6. **Router** = Layer 3, pakai IP address
