# Lab 2: Connect to a Web Server (8.1.3)

**Lab:** Packet Tracer - Connect to a Web Server  
**Modul:** 8.1.3 - The Internet Protocol  
**Tanggal:** 19 Januari 2026  
**Status:** ✅ Selesai

---

## 📋 Objectives

Observe how packets are sent across the Internet using IP addresses.

---

## 🔧 Topologi Jaringan

```
┌─────────────┐                              ┌─────────────────┐
│    PC0      │ ──────── Internet ────────── │   Web Server    │
│   Client    │                              │  172.33.100.50  │
└─────────────┘                              └─────────────────┘
```

---

## 📝 Langkah Praktikum

### Part 1: Verify Connectivity to Web Server

**Langkah:**
1. Klik **PC0** → Tab **Desktop** → **Command Prompt**
2. Ping ke web server untuk verifikasi konektivitas

**Command:**
```
PC> ping 172.33.100.50
```

**Output:**
```
Pinging 172.33.100.50 with 32 bytes of data:

Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
Reply from 172.33.100.50: bytes=32 time=0ms TTL=127

Ping statistics for 172.33.100.50:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

> **Note:** Reply mungkin timeout di awal saat devices loading dan ARP dilakukan.

---

### Part 2: Connect to Web Server via Web Browser

**Langkah:**
1. Di **Desktop** tab PC0 → pilih **Web Browser**
2. Ketik `172.33.100.50` di URL bar
3. Klik **Go**

**Hasil:** Web page berhasil ditampilkan

---

## ❓ Reflection Question

**Q:** What messages did you see after the web page has finished loading?

**A:** "You were able to reach this website because you had the IP address of the web server. The connecting PC also had a web client running on the device."

---

## 💡 Learning Outcomes

1. **IP Address untuk Komunikasi** - Akses web server membutuhkan IP address tujuan
2. **Ping untuk Verifikasi** - Test konektivitas sebelum akses service
3. **Client-Server Model** - PC sebagai client, web server sebagai server
4. **Web Communication** - Browser mengirim HTTP request ke IP server

---

## 🔗 Referensi

- **Teori:** [Modul 8 - The Internet Protocol](../../notes_modul/modul-08-id.md)

---

**Completed:** 19 Januari 2026
