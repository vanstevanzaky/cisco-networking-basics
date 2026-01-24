# Lab 1: Configure Wireless Router and Clients (4.4.4)

**Lab:** Packet Tracer - Configure a Wireless Router and Clients  
**Modul:** 4.4.4 - Build a Home Network  
**Tanggal:** 18 Januari 2026  
**Status:** ✅ Selesai (Score: 19/19)

---

## 📋 Objectives

1. Connect the Devices
2. Configure the Wireless Router
3. Configure IP Addressing and Test Connectivity

---

## 🔧 Topologi Jaringan

```
                         ┌─────────────┐
                         │  Internet   │
                         │   (Cloud)   │
                         └──────┬──────┘
                                │
                         ┌──────┴──────┐
                         │Cable Splitter│
                         └───┬─────┬───┘
                             │     │
                    ┌────────┘     └────────┐
                    │                       │
             ┌──────┴──────┐          ┌─────┴─────┐
             │ Cable Modem │          │    TV     │
             └──────┬──────┘          └───────────┘
                    │
         ┌──────────┴──────────┐
         │  Home Wireless      │
         │      Router         │
         │   192.168.0.1       │
         └──┬───────┬───────┬──┘
            │       │       │ )))
     ┌──────┴──┐ ┌──┴────┐ ┌┴───────┐
     │Office PC│ │Bedroom│ │ Laptop │
     │  Wired  │ │  PC   │ │Wireless│
     └─────────┘ └───────┘ └────────┘
```

**Network:** 192.168.0.0/24  
**DHCP Range:** 192.168.0.2 - 192.168.0.11 (Max 10 users)

---

## 📝 Langkah Praktikum

### Part 1: Connect the Devices

#### Step 1: Connect Coaxial Cables

| From | To | Cable Type |
|------|----|------------|
| Cable Splitter (Coaxial1) | Cable Modem (Port 0) | Coaxial |
| Cable Splitter (Coaxial2) | TV (Port 0) | Coaxial |

**Verifikasi:** Klik TV → Status ON → Gambar TV muncul

---

#### Step 2: Connect Network Cables

| From | To | Cable Type |
|------|----|------------|
| Cable Modem (Port 1) | Router (Internet port) | Copper Straight-Through |
| Office PC (FastEthernet0) | Router (GigabitEthernet 1) | Copper Straight-Through |
| Bedroom PC (FastEthernet0) | Router (GigabitEthernet 2) | Copper Straight-Through |

---

### Part 2: Configure the Wireless Router

#### Step 1: Access Router GUI

1. Klik **Office PC** → **Desktop** → **IP Configuration**
2. Pilih **DHCP** (tunggu dapat IP 192.168.0.x)
3. Catat **Default Gateway:** `192.168.0.1`
4. Buka **Web Browser** → ketik `192.168.0.1`
5. Login: `admin` / `admin`

---

#### Step 2: Configure Basic Settings

**Setup Tab - Network Setup:**

| Parameter | Nilai |
|-----------|-------|
| Maximum Number of Users | **10** |

→ Klik **Save Settings**

**Administration Tab:**

| Parameter | Nilai |
|-----------|-------|
| Router Password | **MyPassword1!** |

→ Klik **Save Settings** → Login ulang dengan password baru

---

#### Step 3: Configure Wireless LAN

**Wireless Tab - Basic Settings:**

| Parameter | Nilai |
|-----------|-------|
| 2.4 GHz Network | **Enable** |
| Network Name (SSID) | **MyHome** |

→ Klik **Save Settings**

**Wireless Security Tab:**

| Parameter | Nilai |
|-----------|-------|
| Security Mode | **WPA2 Personal** |
| Passphrase | **MyPassPhrase1!** |

→ Klik **Save Settings**

---

### Part 3: Configure IP Addressing and Test Connectivity

#### Step 1: Connect Laptop to Wireless

1. Klik **Laptop** → **Desktop** → **PC Wireless**
2. Tab **Connect** → pilih **MyHome**
3. Klik **Connect**
4. Masukkan Pre-shared Key: `MyPassPhrase1!`
5. Klik **Connect**

**Verifikasi:** "You have successfully connected to the access point"

---

#### Step 2: Test Connectivity - Office PC

1. **Office PC** → **Desktop** → **Web Browser**
2. Ketik `skillsforall.srv` → Klik **Go**
3. Halaman web berhasil ditampilkan ✅

---

#### Step 3: Configure Bedroom PC

1. **Bedroom PC** → **Desktop** → **IP Configuration**
2. Pilih **DHCP**
3. Buka **Web Browser** → `skillsforall.srv`
4. Halaman web berhasil ditampilkan ✅

---

## ✅ Hasil Assessment

**Score: 19/19 (100%)**

| Category | Score |
|----------|-------|
| Physical Connections | 8/8 |
| IP Configuration | 3/3 |
| Other Settings | 8/8 |

---

## 📊 Final Configuration Summary

| Device | IP Address | Connection | Status |
|--------|------------|------------|--------|
| Router | 192.168.0.1 | Gateway | ✅ |
| Office PC | DHCP (192.168.0.x) | Wired | ✅ |
| Bedroom PC | DHCP (192.168.0.x) | Wired | ✅ |
| Laptop | DHCP (192.168.0.x) | Wireless | ✅ |

| Router Setting | Value |
|----------------|-------|
| SSID | MyHome |
| Security | WPA2 Personal |
| Passphrase | MyPassPhrase1! |
| Admin Password | MyPassword1! |
| DHCP Max Users | 10 |

---

## 💡 Learning Outcomes

1. **Physical Topology** - Menghubungkan coaxial dan ethernet cables dengan benar
2. **Router Configuration** - Akses GUI router via web browser
3. **Wireless Security** - Setup WPA2 Personal dengan passphrase
4. **DHCP** - Automatic IP assignment untuk client devices
5. **Connectivity Testing** - Verifikasi akses internet via web browser

---

## 🔗 Referensi

- **Teori:** [Modul 4 - Build a Home Network](../../notes_modul/modul-04-id.md)
- **Terkait:** [Modul 3 - Wireless and Mobile Networks](../../notes_modul/modul-03-id.md)

---

**Time Elapsed:** 47:43  
**Completed:** 18 Januari 2026
