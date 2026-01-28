# Modul 13: MAC and IP Addresses

**Modul:** 13 - MAC and IP / ARP Process  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **MAC address** untuk komunikasi NIC-to-NIC di jaringan lokal (Layer 2)
- **IP address** untuk identifikasi sumber dan tujuan paket (Layer 3)
- **Same network:** Destination MAC = MAC device tujuan
- **Remote network:** Destination MAC = MAC default gateway (router)
- **ARP** digunakan untuk mencari MAC address dari IP yang diketahui

---

## 📚 Materi

### 1. Dua Jenis Address

| Address | Layer | Fungsi | Scope |
|---------|-------|--------|-------|
| **MAC Address** | Layer 2 | Komunikasi NIC-to-NIC | Lokal (per hop) |
| **IP Address** | Layer 3 | Identifikasi sumber & tujuan | End-to-end |

---

### 2. Komunikasi di Jaringan yang Sama

**Skenario:** PC1 (192.168.10.10) → PC2 (192.168.10.11) - **Same Network**

| Field | Value |
|-------|-------|
| Destination MAC | **MAC PC2** (55-55-55) |
| Source MAC | MAC PC1 (aa-aa-aa) |
| Source IP | 192.168.10.10 |
| Destination IP | 192.168.10.11 |

**Poin penting:** Destination MAC langsung ke device tujuan

---

### 3. Komunikasi ke Remote Network

**Skenario:** PC1 (192.168.10.10) → PC2 (10.1.1.10) - **Different Network**

#### Hop 1: PC1 → Router R1
| Field | Value |
|-------|-------|
| Destination MAC | **MAC Router R1** (bb-bb-bb) |
| Source MAC | MAC PC1 (aa-aa-aa) |
| Source IP | 192.168.10.10 |
| Destination IP | 10.1.1.10 |

#### Hop 2: Router R1 → Router R2
| Field | Value |
|-------|-------|
| Destination MAC | **MAC R2 G0/0/1** (dd-dd-dd) |
| Source MAC | MAC R1 G0/0/1 (cc-cc-cc) |
| Source IP | 192.168.10.10 |
| Destination IP | 10.1.1.10 |

#### Hop 3: Router R2 → PC2
| Field | Value |
|-------|-------|
| Destination MAC | **MAC PC2** (55-55-55) |
| Source MAC | MAC R2 G0/0/0 (ee-ee-ee) |
| Source IP | 192.168.10.10 |
| Destination IP | 10.1.1.10 |

**Kesimpulan:**
- **IP address TIDAK berubah** sepanjang perjalanan (end-to-end)
- **MAC address BERUBAH** di setiap hop (per link)

---

### 4. Broadcast Domain

**Broadcast MAC Address:** `FFFF.FFFF.FFFF` (48 bit semua 1)

| Konsep | Penjelasan |
|--------|------------|
| **Broadcast Domain** | Area dimana broadcast frame diteruskan |
| **Switch** | Meneruskan broadcast ke SEMUA port (kecuali port masuk) |
| **Router** | TIDAK meneruskan broadcast → memisahkan broadcast domain |

**Masalah:** Terlalu banyak host = broadcast traffic berlebihan  
**Solusi:** Pisahkan jaringan dengan router

---

### 5. ARP (Address Resolution Protocol)

**Fungsi:** Mencari MAC address dari IP address yang diketahui

#### Proses ARP (3 Langkah):

| Step | Aksi | Tipe |
|------|------|------|
| 1 | Host kirim **ARP Request** (berisi IP tujuan) | **Broadcast** |
| 2 | Host dengan IP cocok balas **ARP Reply** (berisi MAC-nya) | Unicast |
| 3 | Pengirim simpan di **ARP Table** | - |

**ARP Table:** Tabel yang menyimpan mapping IP ↔ MAC

**IPv6:** Menggunakan **Neighbor Discovery (ND)** sebagai pengganti ARP

---

### 6. Kapan Pakai MAC Mana?

| Tujuan | Destination MAC |
|--------|-----------------|
| **Same network** | MAC device tujuan |
| **Remote network** | MAC default gateway (router) |

---

## 🔬 Lab: Identify MAC and IP Addresses

### Part 1: Local Network Communication

**Ping 172.16.31.3 → 172.16.31.2 (Same Network)**

| At Device | Src MAC | Dest MAC | Src IP | Dest IP |
|-----------|---------|----------|--------|---------|
| 172.16.31.3 | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| Switch | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| 172.16.31.2 (in) | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| 172.16.31.2 (out) | 000C.85CC.1DA7 | 0060.7036.2849 | 172.16.31.2 | 172.16.31.3 |

**Observasi:** MAC dan IP swap saat reply

### Part 2: Remote Network Communication

**Ping 172.16.31.3 → 10.10.10.2 (Different Network)**

| At Device | Src MAC | Dest MAC | Src IP | Dest IP |
|-----------|---------|----------|--------|---------|
| 172.16.31.3 | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Switch 2 | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Router (in) | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Router (out) | 00D0.588C.2401 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |
| 10.10.10.2 (in) | 0050.0FAB.6C82 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |

**Observasi:** 
- MAC berubah di router (new frame created)
- IP tetap sama dari awal sampai akhir

### Reflection Questions

| Pertanyaan | Jawaban |
|------------|---------|
| Jenis kabel yang digunakan? | Copper, Fiber, Wireless |
| Di mana MAC address berubah? | Di **Router** |
| Layer OSI untuk switch & AP? | Layer 1 (Physical) |
| Di PDU Details, MAC mana dulu? | **Destination** MAC |
| IP address berubah? | **Tidak**, tetap end-to-end |
| Fungsi router punya 2 interface? | Menghubungkan 2 network berbeda |

---

## 💡 Poin Penting

1. **MAC address** = Layer 2, berubah setiap hop
2. **IP address** = Layer 3, tetap dari source ke destination
3. **Same network** → Destination MAC = MAC tujuan
4. **Remote network** → Destination MAC = MAC gateway (router)
5. **ARP Request** = Broadcast, **ARP Reply** = Unicast
6. **Broadcast domain** dipisahkan oleh router
7. **Broadcast MAC** = FFFF.FFFF.FFFF
8. Switch forward broadcast ke semua port (kecuali incoming)
9. Router **TIDAK** forward broadcast
10. IPv6 pakai **Neighbor Discovery** bukan ARP
