# 🔐 Bug Bounty Portfolio

**Handle:** Muhkhoirisma  
**Fokus:** IDOR, Broken Access Control, Unauthenticated Endpoint  

---

## 📌 Tentang Saya

Bug hunter dengan pengalaman melaporkan kerentanan keamanan ke program resmi (VDP & bug bounty), baik dari perusahaan swasta maupun instansi pemerintah.

---

## 🏆 Pencapaian

| # | Pencapaian | Keterangan |
|---|------------|-------------|
| 1 | **IDOR** – Platform Keuangan (Kredivo) | Kerentanan valid, diterima, dan diberikan bounty |
| 2 | **Unauthenticated Access** – Pemerintah Provinsi Bali | Mendapat piagam resmi atas kontribusi keamanan sistem elektronik |
| 3 | **Laporan ke NASA VDP** | Melaporkan temuan ke NASA Vulnerability Disclosure Program |

---

## 🛠️ Studi Kasus

### Kasus 1: IDOR di Endpoint Deprecated
- **Target:** Platform keuangan (Kredivo)  
- **Endpoint:** API lama yang masih aktif  
- **Eksploitasi:** Perubahan parameter ID → akses data akun user lain  
- **Dampak:** Kebocoran nama & email akun manajer perusahaan  
- **Status:** ✅ Valid (diberikan bounty)

### Kasus 2: Unauthenticated Access
- **Target:** Sistem UMKM Pemerintah Provinsi Bali  
- **Endpoint:** Fitur import produk  
- **Eksploitasi:** Fitur bisa diakses tanpa login sama sekali  
- **Dampak:** Potensi manipulasi data produk UMKM  
- **Status:** ✅ Valid (mendapat piagam resmi)

---

## 🧰 Tools

- **Burp Suite** (Repeater, Intruder, Proxy)
- **Dirsearch** (directory enumeration)
- **Manual testing** (parameter ID, hidden endpoint, logic bug)

---

## 🎯 Target Saat Ini

Mencari private bug bounty program atau invited testing yang fokus pada IDOR dan broken access control.

---

## 📬 Kontak

**Email:** sad306391@gmail.com

---

*Semua laporan telah diredaksi untuk menghormati kebijakan program masing-masing. Bukti pendukung tersedia jika diperlukan.*
