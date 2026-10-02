# HC-SR04 Filter Monitor

Dashboard web untuk menampilkan bacaan aktual HC-SR04, hasil filter EMA, hasil filter AMA, dan jarak fixed. Grafik menunjukkan 60 sampel terbaru dan galat tiap pembacaan terhadap jarak fixed.

Halaman statis berada di [`dist/index.html`](dist/index.html). Publikasi GitHub Pages dijelaskan di [`GITHUB_PAGES.md`](GITHUB_PAGES.md), sedangkan format JSON dan contoh endpoint ESP32 ada di [`INTEGRATION.md`](INTEGRATION.md).

Gunakan tombol **Sumber data** pada dashboard untuk memasukkan alamat Wi-Fi lokal ESP32. Mode demo tersedia dengan menambahkan `?demo=1` ke URL.
