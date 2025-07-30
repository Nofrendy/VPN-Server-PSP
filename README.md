# VPN-Server-PSP
Saya coba buat server online multiplayer dengan mengandalkan VPS sebagai hosting utama dari VPN yang akan dibuat

# PPSSPP Multiplayer Server with WireGuard & AdhocServer (VPS Azure)

Panduan lengkap membuat server multiplayer PPSSPP agar bisa mabar online dengan teman menggunakan VPS (Ubuntu 22.04), WireGuard VPN, dan AdhocServer.

---

## 1. Sewa VPS Ubuntu 22.04
- Pilih region Indonesia (atau terdekat).
- Catat IP publik VPS.

---

## 2. Buka Port di NSG Azure & Firewall VPS
- **WireGuard:** UDP 54378
- **AdhocServer:** UDP 27312

Contoh rule NSG Azure:
- Destination port: 54378, Protocol: UDP, Action: Allow
- Destination port: 27312, Protocol: UDP, Action: Allow

Di VPS:
```bash
sudo ufw allow 54378/udp
sudo ufw allow 27312/udp
```

---

## 3. Install WireGuard di VPS

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wireguard -y
```

Atau gunakan script auto-install (rekomendasi):
```bash
curl -O https://raw.githubusercontent.com/angristan/wireguard-install/master/wireguard-install.sh
chmod +x wireguard-install.sh
sudo ./wireguard-install.sh
```
- Ikuti wizard, isi IP publik VPS, port (54378), DNS (1.1.1.1), dst.
- Buat client (misal: `rendsmodpsp`), file config akan dibuat (misal: `/home/username/wg0-client-rendsmodpsp.conf`).

---

## 4. Download & Import Config Client ke HP/PC

- Download file `.conf` ke HP/PC (bisa via `scp` atau QR code):
  ```bash
  sudo apt install qrencode -y
  qrencode -t ansiutf8 < /home/username/wg0-client-rendsmodpsp.conf
  ```
- Scan QR di aplikasi WireGuard HP, atau import file di PC.

---

## 5. Connect ke VPN WireGuard

- Aktifkan profile di aplikasi WireGuard.
- Test ping ke IP privat server (misal: `10.66.66.1`) dari HP/PC.

---

## 6. Install & Jalankan AdhocServer di VPS

```bash
sudo apt install git build-essential libsqlite3-dev -y
git clone https://github.com/Souler/ppsspp-adhoc-server.git
cd ppsspp-adhoc-server
make
./AdhocServer
```
- Pastikan output: `Listening for Connections on TCP Port 27312.`

---

## 7. Setting PPSSPP Multiplayer

- Semua pemain connect ke VPN WireGuard.
- Di PPSSPP:  
  - Settings → Networking  
  - Enable networking/WLAN  
  - Change PRO ad hoc server IP address: **isi dengan IP privat WireGuard server (misal: 10.66.66.1)**
- Simpan.

---

## 8. Mainkan Game Multiplayer

- Host buat room/lobby, pemain lain join.
- Selamat mabar!

---

## Troubleshooting

- Pastikan semua port sudah dibuka di NSG Azure dan firewall VPS.
- Cek status WireGuard:
  ```bash
  sudo systemctl status wg-quick@wg0
  sudo wg show
  ```
- Test ping antar client dan ke server.
- Pastikan semua client mengisi IP AdhocServer dengan benar.

---

## Credits

- [angristan/wireguard-install](https://github.com/angristan/wireguard-install)
- [Souler/ppsspp-adhoc-server](https://github.com/Souler/ppsspp-adhoc-server)
- [PPSSPP](https://www.ppsspp.org/)

---

> Dokumentasi ini dibuat berdasarkan pengalaman setup server multiplayer PPSSPP di Azure VPS. Silakan modifikasi sesuai kebutuhan!
