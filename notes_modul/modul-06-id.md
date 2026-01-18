# Modul 6: Media Jaringan (Network Media)

**Kursus:** Cisco Networking Academy - Networking Basics  
**Status:** ✅ Selesai  
**Tanggal:** Januari 2026

---

## 📚 Jenis Media Jaringan

### 1. Twisted-Pair Cable

**Jenis:**
- **UTP (Unshielded):** Tanpa pelindung, murah, umum di LAN
- **STP (Shielded):** Ada pelindung, lebih tahan gangguan

**Kategori UTP:**
- **Cat5e:** 1 Gbps, 100m (umum)
- **Cat6:** 10 Gbps, 55-100m
- **Cat6a:** 10 Gbps, 100m

**Kelebihan:**
- ✅ Murah & fleksibel
- ✅ Mudah dipasang
- ✅ Support PoE

**Kekurangan:**
- ❌ Jarak terbatas (100m)
- ❌ Rentan EMI/RFI
- ❌ Mudah disadap

**Penggunaan:** LAN kantor/rumah, Ethernet

---

### 2. Coaxial Cable

**Struktur:** Inti tembaga + isolasi + pelindung logam + jacket

**Kelebihan:**
- ✅ Tahan gangguan elektromagnetik

**Kekurangan:**
- ❌ Tebal & kaku
- ❌ Bandwidth terbatas
- ❌ Legacy technology

**Penggunaan:** TV kabel, set-top box (jarang untuk LAN modern)

---

### 3. Fiber-Optic Cable

**Cara kerja:** Transmisi data sebagai impuls **cahaya** melalui serat kaca/plastik

**Jenis:**
- **Single-Mode (SMF):** Laser, 40-100+ km, terabit
- **Multi-Mode (MMF):** LED, 2-5 km, gigabit

**Kelebihan:**
- ✅ Kecepatan sangat tinggi (terabit)
- ✅ Jarak sangat jauh
- ✅ **Kebal EMI & RFI** (100%)
- ✅ Sulit disadap

**Kekurangan:**
- ❌ Mahal
- ❌ Instalasi rumit
- ❌ Tidak support PoE

**Penggunaan:** Backbone jaringan, ISP, data center, submarine cables

---

## 📊 Perbandingan Media

| Media | Kecepatan | Jarak | EMI/RFI | Biaya | Keamanan |
|-------|-----------|-------|---------|-------|----------|
| **UTP** | 1-10 Gbps | 100m | ❌ Rentan | 💰 Murah | ⚠️ Mudah disadap |
| **Coaxial** | ~1 Gbps | 500m | ✅ Tahan | 💰💰 Sedang | ⚠️ Bisa disadap |
| **Fiber** | Terabit+ | 40-100+ km | ✅ Kebal | 💰💰💰 Mahal | ✅ Sulit disadap |

---

## 🛡️ EMI & RFI

**EMI (Electromagnetic Interference):**
- Gangguan elektromagnetik umum
- Sumber: Motor, lampu, perangkat listrik

**RFI (Radio Frequency Interference):**
- Gangguan spesifik frekuensi radio (subset EMI)
- Sumber: Wi-Fi, radio, microwave

**Poin Penting:**
- Fiber optic **kebal 100%** EMI & RFI (transmisi cahaya, bukan elektrik)
- UTP sangat rentan
- Coaxial lebih tahan tapi tidak kebal

---

## 💡 Poin Penting

1. **3 media:** Twisted-pair (UTP/STP), Coaxial, Fiber-optic
2. **Fiber** = terbaik (speed, distance) tapi mahal
3. **UTP** = paling umum untuk LAN (cost-effective)
4. **Fiber kebal EMI/RFI** karena transmit cahaya
5. **UTP max 100m**, Fiber bisa 40-100+ km

---

**Konsep Terkait:** Access Layer (Modul 7), Communication Principles (Modul 5)