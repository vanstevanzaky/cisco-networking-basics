# Lab 5: Identifikasi Alamat MAC dan IP

**Module:** 13 (The ARP Process)  
**Topik:** 13.1.3  
**Status:** ✅ Selesai

---

## 📌 Tujuan Lab

- **Part 1:** Mengumpulkan informasi PDU untuk komunikasi jaringan lokal
- **Part 2:** Mengumpulkan informasi PDU untuk komunikasi jaringan remote

---

## 🔧 Hasil Praktik

### Part 1: Local Network Communication

**Ping 172.16.31.3 → 172.16.31.2 (Same Network)**

| At Device | Src MAC | Dest MAC | Src IPv4 | Dest IPv4 |
|-----------|---------|----------|----------|-----------|
| 172.16.31.3 | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| Switch | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| 172.16.31.2 (in) | 0060.7036.2849 | 000C.85CC.1DA7 | 172.16.31.3 | 172.16.31.2 |
| 172.16.31.2 (out) | 000C.85CC.1DA7 | 0060.7036.2849 | 172.16.31.2 | 172.16.31.3 |
| Switch | 000C.85CC.1DA7 | 0060.7036.2849 | 172.16.31.2 | 172.16.31.3 |
| 172.16.31.3 (in) | 000C.85CC.1DA7 | 0060.7036.2849 | 172.16.31.2 | 172.16.31.3 |

**Question:** Mengapa outbound PDU berbeda?

> Karena saat "in" itu masuk, dan "out" itu keluar. Ibaratnya sebuah rumah A dan B saling kirim surat. Dari rumah A ke Rumah B, itu kan "out" dari rumah A dan "in" di rumah B. Lalu alamatnya saling tukar pastinya kalau misal rumah B mau ngirim surat ke rumah A, kalau sama persis kan berarti ngirim ke rumahnya sendiri dong. Maka dari itu mengapa outbound PDU itu berbeda.

---

### Part 2: Remote Network Communication

**Ping 172.16.31.3 → 10.10.10.2 (Different Network)**

**Question:** Device dan interface mana yang punya destination MAC address tersebut?
> Router, interface FastEthernet1/0

#### Echo Request (172.16.31.3 → 10.10.10.2)

| At Device | Src MAC | Dest MAC | Src IPv4 | Dest IPv4 |
|-----------|---------|----------|----------|-----------|
| 172.16.31.3 | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Switch 2 | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Router (in) | 0060.7036.2849 | 00D0.BA8E.741A | 172.16.31.3 | 10.10.10.2 |
| Router (out) | 00D0.588C.2401 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |
| Switch 1 | 00D0.588C.2401 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |
| Access Point (in) | 00D0.588C.2401 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |
| Access Point (out) | 0050.0FAB.6C82 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |
| 10.10.10.2 (in) | 0050.0FAB.6C82 | 0060.2F84.4AB6 | 172.16.31.3 | 10.10.10.2 |

#### Echo Reply (10.10.10.2 → 172.16.31.3)

| At Device | Src MAC | Dest MAC | Src IPv4 | Dest IPv4 |
|-----------|---------|----------|----------|-----------|
| 10.10.10.2 (out) | 0060.2F84.4AB6 | 0050.0FAB.6C82 | 10.10.10.2 | 172.16.31.3 |
| Access Point (in) | 0060.2F84.4AB6 | 0050.0FAB.6C82 | 10.10.10.2 | 172.16.31.3 |
| Access Point (out) | 0060.2F84.4AB6 | 00D0.588C.2401 | 10.10.10.2 | 172.16.31.3 |
| Switch 1 | 0060.2F84.4AB6 | 00D0.588C.2401 | 10.10.10.2 | 172.16.31.3 |
| Router (in) | 0060.2F84.4AB6 | 00D0.588C.2401 | 10.10.10.2 | 172.16.31.3 |
| Router (out) | 00D0.BA8E.741A | 0060.7036.2849 | 10.10.10.2 | 172.16.31.3 |
| Switch 2 | 00D0.BA8E.741A | 0060.7036.2849 | 10.10.10.2 | 172.16.31.3 |
| 172.16.31.3 (in) | 00D0.BA8E.741A | 0060.7036.2849 | 10.10.10.2 | 172.16.31.3 |

---

## ❓ Reflection Questions

| No | Pertanyaan | Jawaban |
|----|------------|---------|
| 1 | Jenis kabel/media apa yang digunakan? | Copper, fiber, dan wireless |
| 2 | Apakah kabel mengubah penanganan PDU? | Tidak |
| 3 | Apa yang dilakukan Access Point pada PDU? | Mengubah format PDU dari wired (Ethernet) ke wireless (802.11) dan sebaliknya |
| 4 | Apakah addressing PDU diubah oleh Access Point? | Tidak |
| 5 | Layer OSI tertinggi yang digunakan Access Point? | Layer 1 (Physical Layer) |
| 6 | Di Layer OSI berapa kabel dan AP beroperasi? | Layer 1 |
| 7 | Di PDU Details, MAC mana yang muncul duluan? | Destination |
| 8 | Apa arti tanda X merah dan centang hijau? | PDU dikirim ke MAC address tertentu, jika MAC tidak cocok berarti bukan untuknya (X merah) |
| 9 | Di mana MAC address berubah tiba-tiba? | Di Router |
| 10 | Device mana yang punya MAC 00D0:BA? | Router |
| 11 | MAC address lain milik device apa? | Sending device dan receiving device |
| 12 | Apakah IPv4 address berubah di PDU? | Tidak |
| 13 | Apa yang terjadi pada address saat reply (pong)? | Address seperti bertukar tempat karena penerima menjadi pengirim dan sebaliknya |
| 14 | Mengapa interface router ada di 2 network berbeda? | Fungsi router adalah menghubungkan network berbeda, jadi harus punya 2 interface |
| 15 | Network IP mana yang dihubungkan router? | 10.10.10.0/24 dan 172.16.31.0/24 |

---

## 💡 Pemahaman & Learning Outcomes

### Konsep Utama:
1. **MAC address berubah di setiap hop** (terutama di router)
2. **IP address TETAP** dari source sampai destination
3. **Same network** → Destination MAC = MAC tujuan langsung
4. **Remote network** → Destination MAC = MAC gateway (router)
5. **Router** memisahkan broadcast domain dan mengubah frame Layer 2
6. **Switch & Access Point** beroperasi di Layer 1-2, tidak mengubah addressing
