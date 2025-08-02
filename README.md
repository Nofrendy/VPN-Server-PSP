# 🎮 PPSSPP Multiplayer Server - Direct Setup

> Server multiplayer PPSSPP dengan management panel web yang modern dan mudah digunakan.

Panduan lengkap untuk membuat server multiplayer PPSSPP menggunakan VPS Azure Ubuntu 22.04 dengan web management panel yang memungkinkan Anda bermain online dengan teman-teman dimana saja.

## ✨ Fitur

- 🎮 **PPSSPP AdhocServer** dengan auto-management
- 🌐 **Web Management Panel** yang modern dan responsif
- 📱 **Mobile-friendly** interface untuk monitoring
- 🔄 **Auto-restart** dan process management
- 📊 **Real-time logs** dan server status
- 📤 **Binary upload** via web interface
- 🔒 **Secure** dan mudah dikonfigurasi
- 🚀 **One-click installer** script

---

## 🚀 Quick Start

### 1. Persiapan VPS
- Sewa VPS Ubuntu 22.04 (disarankan Azure/Digital Ocean)
- Catat IP publik VPS Anda
- Pastikan domain mengarah ke IP VPS (opsional)

### 2. Konfigurasi Network
**Azure Network Security Group:**
- Port 3000 (TCP) - Web Management Panel
- Port 27312 (UDP) - PPSSPP AdhocServer

**VPS Firewall:**
Firewall akan dikonfigurasi otomatis oleh installer script.

### 3. Instalasi Server
Cukup jalankan satu command di VPS Anda:

```bash
# Download dan jalankan installer
wget -O install.sh [installer-url] && chmod +x install.sh && sudo bash install.sh
```

*Installer akan otomatis menginstall semua dependencies dan mengkonfigurasi server.*

### 4. Akses Web Panel
Setelah instalasi selesai:
- Buka browser: `http://[IP-VPS]:3000`
- Upload file AdhocServer binary
- Start server melalui web panel

### 5. Konfigurasi PPSSPP Client
Di aplikasi PPSSPP:
- **Settings** → **Networking**
- **Pro Ad Hoc Server**: `[IP-VPS]:27312`
- Simpan dan mulai bermain!

---

## 🎯 Cara Bermain

1. **Host** membuat room/lobby game
2. **Player lain** join ke room yang sama
3. Pastikan semua player menggunakan server yang sama
4. Selamat bermain multiplayer online! 🎮

---

## 🛠️ Manajemen Server

### Web Management Panel
- **Start/Stop/Restart** server dengan sekali klik
- **Monitor status** server real-time
- **View logs** untuk troubleshooting
- **Upload binary** AdhocServer baru
- **Responsive design** untuk akses mobile

### Service Management (Advanced)
Jika perlu akses langsung via SSH:
- **Status**: `systemctl status ppsspp-server`
- **Restart**: `systemctl restart ppsspp-server`
- **Logs**: `journalctl -u ppsspp-server -f`

---

## 🔧 Spesifikasi Teknis

- **Platform**: Ubuntu 22.04 LTS
- **Runtime**: Node.js 18.x
- **Process Manager**: SystemD service
- **Web Framework**: Express.js + Socket.IO
- **Frontend**: Modern responsive HTML5/CSS3
- **Binary**: PPSSPP AdhocServer (upload manual)

---

## 🎮 Game Compatibility

Server ini kompatibel dengan semua game PSP yang mendukung Ad Hoc multiplayer, termasuk:
- Monster Hunter Series
- God Eater Series  
- Phantasy Star Portable
- Crisis Core Final Fantasy VII
- Dan banyak lagi...

---

## ⚠️ Troubleshooting

### Server tidak bisa diakses:
- Pastikan port 3000 dan 27312 sudah dibuka di firewall
- Cek status service: `systemctl status ppsspp-server`

### PPSSPP tidak bisa connect:
- Pastikan menggunakan IP:Port yang benar
- Cek apakah AdhocServer sudah running di web panel

### Upload binary gagal:
- Pastikan file AdhocServer valid dan executable
- Cek logs di web panel untuk detail error

---

## 🤝 Kontribusi

Ingin berkontribusi pada project ini? Silakan hubungi melalui:

📱 **Instagram**: [@rends_mod](https://instagram.com/rends_mod)  
💬 **Telegram**: [@weathershit](https://t.me/weathershit)  
📧 **Email**: [nofrendydelmiren@gmail.com](mailto:nofrendydelmiren@gmail.com)

---

## 📝 Credits

- [angristan/wireguard-install](https://github.com/angristan/wireguard-install)
- [Souler/ppsspp-adhoc-server](https://github.com/Souler/ppsspp-adhoc-server)
- [PPSSPP](https://www.ppsspp.org/)

---

> Dokumentasi ini dibuat berdasarkan pengalaman setup server multiplayer PPSSPP di Azure VPS. Silakan modifikasi sesuai kebutuhan!
