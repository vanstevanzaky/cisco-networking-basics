# Modul 6: Media Jaringan

**Modul:** 6 - Network Media  
**Status:** ✅ Selesai

---

## 📌 Ringkasan

- **Twisted-pair (UTP/STP)** paling umum untuk LAN, murah tapi jarak terbatas 100m
- **Coaxial** tahan EMI tapi legacy, jarang untuk LAN modern
- **Fiber optic** tercepat dan terjauh, kebal EMI, tapi mahal
- Fiber transmit **cahaya**, bukan sinyal elektrik → kebal interferensi

---

## 📚 Materi

### 1. Twisted-Pair Cable

| Jenis | Karakteristik |
|-------|---------------|
| **UTP** | Tanpa pelindung, murah, umum di LAN |
| **STP** | Ada pelindung, lebih tahan gangguan |

| Kategori | Kecepatan | Jarak Max |
|----------|-----------|-----------|
| Cat5e | 1 Gbps | 100m |
| Cat6 | 10 Gbps | 55-100m |
| Cat6a | 10 Gbps | 100m |

**Kelebihan:** Murah, fleksibel, support PoE  
**Kekurangan:** Jarak terbatas (100m), rentan EMI/RFI

---

### 2. Coaxial Cable

**Struktur:** Inti tembaga + isolasi + pelindung logam + jacket

**Kelebihan:** Tahan gangguan elektromagnetik  
**Kekurangan:** Tebal, kaku, bandwidth terbatas  
**Penggunaan:** TV kabel (legacy, bukan LAN modern)

---

### 3. Fiber Optic Cable

| Jenis | Sumber Cahaya | Jarak | Kecepatan |
|-------|---------------|-------|-----------|
| **Single-Mode (SMF)** | Laser | 40-100+ km | Terabit |
| **Multi-Mode (MMF)** | LED | 2-5 km | Gigabit |

**Kelebihan:** Kecepatan tertinggi, jarak terjauh, kebal EMI/RFI 100%, sulit disadap  
**Kekurangan:** Mahal, instalasi rumit, tidak support PoE

---

### 4. Perbandingan Media

| Media | Kecepatan | Jarak | EMI/RFI | Biaya | Keamanan |
|-------|-----------|-------|---------|-------|----------|
| **UTP** | 1-10 Gbps | 100m | Rentan | Murah | Mudah disadap |
| **Coaxial** | ~1 Gbps | 500m | Tahan | Sedang | Bisa disadap |
| **Fiber** | Terabit+ | 100+ km | Kebal | Mahal | Sulit disadap |

---

### 5. EMI dan RFI

| Interferensi | Definisi | Sumber |
|--------------|----------|--------|
| **EMI** | Gangguan elektromagnetik | Motor, lampu, perangkat listrik |
| **RFI** | Gangguan frekuensi radio | Wi-Fi, radio, microwave |

**Catatan:** Fiber optic kebal 100% karena transmit cahaya, bukan sinyal elektrik

---

## 💡 Poin Penting

1. **3 jenis media:** Twisted-pair, Coaxial, Fiber optic
2. **Fiber** = terbaik (speed, distance) tapi paling mahal
3. **UTP** = paling umum untuk LAN karena cost-effective
4. **Fiber kebal EMI/RFI** karena transmit cahaya
5. **UTP max 100m**, Fiber bisa ratusan km
6. **Single-mode** untuk jarak jauh, **Multi-mode** untuk jarak sedang
