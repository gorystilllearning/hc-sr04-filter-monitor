# GitHub Pages untuk HC-SR04 Filter Monitor

Folder `dist` berisi seluruh dashboard dan tidak memerlukan build atau server berbayar. Workflow `.github/workflows/pages.yml` menerbitkan isi folder tersebut setiap kali branch `main` diperbarui.

## Publikasi

1. Buat repository **public** di GitHub dan unggah isi folder proyek ini ke branch `main`.
2. Buka **Settings → Pages** pada repository tersebut.
3. Pada **Build and deployment**, pilih **Source: GitHub Actions**.
4. Buka tab **Actions** dan tunggu workflow **Publish dashboard to GitHub Pages** selesai. URL situs muncul pada langkah deploy dan halaman Settings → Pages.

URL proyek biasanya berbentuk `https://NAMA_AKUN.github.io/NAMA_REPO/`.

## Data langsung dari ESP32

Dashboard mengharapkan JSON `actual`, `ema`, `ama`, dan `fixed` dari `/api/readings`; detailnya ada di `INTEGRATION.md`. Bila halaman dibuka melalui GitHub Pages, browser mengaksesnya dengan HTTPS. Koneksi ke ESP32 melalui `http://192.168.x.x` memerlukan dukungan dan izin akses jaringan lokal di browser, serta header CORS dari ESP32. Perangkat pembuka dashboard harus berada di Wi-Fi yang sama. Jika browser tetap memblokir koneksi, sajikan halaman dari ESP32 sendiri.

Mode demo: tambahkan `?demo=1` pada akhir URL.
