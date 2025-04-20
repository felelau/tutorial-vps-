# tutorial-vps-



# Verus Coin Miner Setup di Termux (Codeanywhere VPS)

## Persiapan

1. **Update & Upgrade system Termux:**
   ```bash
   pkg update && pkg upgrade -y
   ```

2. **Install tools dasar:**
   ```bash
   pkg install -y curl wget git htop unzip
   ```

## Clone dan Build ccminer

3. **Clone repository ccminer:**
   ```bash
   git clone https://github.com/Darktron/ccminer.git
   cd ccminer
   ```

4. **Buat file `build.sh` untuk build ccminer:**
   ```bash
   nano build.sh
   ```
   Isi `build.sh`:
   ```bash
   #!/bin/bash

   # Simple script to create the Makefile and build
   make distclean || echo clean

   rm -f Makefile.in
   rm -f config.status
   ./autogen.sh || echo done

   ./configure.sh

   make
   ```

5. **Kasih permission dan jalankan build:**
   ```bash
   chmod +x build.sh
   ./build.sh
   ```

## Konfigurasi Miner

6. **Edit konfigurasi mining:**

   - Edit `config.json` atau `ccminer.conf`
   - Contoh `config.json`:
   ```json
   {
     "url": "stratum+tcp://POOL_ADDRESS:PORT",
     "user": "YOUR_WALLET_ADDRESS",
     "pass": "x",
     "algo": "verus"
   }
   ```

## Membuat Start Script

7. **Buat file `start-miner.sh`:**
   ```bash
   nano start-miner.sh
   ```
   Isi `start-miner.sh`:
   ```bash
   #!/bin/bash

   ~/ccminer/ccminer -c ~/ccminer/config.json
   ```

8. **Kasih permission dan jalankan:**
   ```bash
   chmod +x start-miner.sh
   ./start-miner.sh
   ```

## Cara Berhenti Mining

- Tekan `CTRL + C` di terminal tempat mining berjalan.
- Atau cari PID proses miner dan kill:
  ```bash
  ps aux | grep ccminer
  kill -9 PID
  ```

## Catatan

- Proyek ini dijalankan di **Termux VPS** (Codeanywhere template).
- Firewall (`ufw`) tidak digunakan di setup Termux.
- Tidak perlu `sudo` atau `root`.

---

Kalau mau dijalankan otomatis setelah login, tinggal taruh `./start-miner.sh` di `.bashrc` atau `.zshrc`.

