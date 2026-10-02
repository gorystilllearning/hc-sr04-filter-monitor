# Integrasi dashboard dengan ESP32

Dashboard membaca data setiap 250 ms dari endpoint berikut:

```text
GET /api/readings
```

Respons harus berupa JSON dengan empat angka:

```json
{
  "actual": 49.82,
  "ema": 49.91,
  "ama": 49.97,
  "fixed": 50.00
}
```

- `actual`: pembacaan mentah HC-SR04.
- `ema`: keluaran filter EMA.
- `ama`: keluaran Adaptive Moving Average dengan metode Kaufman.
- `fixed`: jarak acuan yang sudah ditetapkan.

## Contoh endpoint memakai WebServer ESP32

Tambahkan handler berikut ke kode yang sudah memiliki `WebServer server(80)` dan variabel nilai pengukuran.

```cpp
server.on("/api/readings", HTTP_GET, []() {
  String json = "{";
  json += "\"actual\":" + String(actualDistance, 2) + ",";
  json += "\"ema\":" + String(emaDistance, 2) + ",";
  json += "\"ama\":" + String(amaDistance, 2) + ",";
  json += "\"fixed\":" + String(fixedDistance, 2);
  json += "}";
  server.sendHeader("Cache-Control", "no-store");
  server.sendHeader("Access-Control-Allow-Origin", "https://gorystilllearning.github.io");
  server.sendHeader("Access-Control-Allow-Private-Network", "true");
  server.send(200, "application/json", json);
});

server.on("/api/readings", HTTP_OPTIONS, []() {
  server.sendHeader("Access-Control-Allow-Origin", "https://gorystilllearning.github.io");
  server.sendHeader("Access-Control-Allow-Methods", "GET, OPTIONS");
  server.sendHeader("Access-Control-Allow-Private-Network", "true");
  server.send(204);
});
```

Jika dashboard dibuka melalui GitHub Pages, klik **Sumber data** dan masukkan alamat ESP32, misalnya `http://192.168.4.1`. Perangkat pembuka dashboard harus terhubung ke Wi-Fi yang sama dengan ESP32. Browser yang mendukung akses jaringan lokal dapat meminta izin; izinkan untuk halaman dashboard. Dukungan browser berbeda-beda. Opsi paling kompatibel bila koneksi HTTP lokal diblokir adalah menyajikan `dist/index.html` langsung dari ESP32 melalui LittleFS/SPIFFS.

Header `Access-Control-Allow-Origin` sengaja dibatasi ke origin GitHub Pages akun ini. Jika dashboard dipindahkan ke domain lain, ganti nilainya dengan origin domain tersebut (skema dan host, tanpa path). Contoh ini hanya untuk endpoint pembacaan; jangan tambahkan endpoint yang mengubah konfigurasi alat tanpa autentikasi.

Mode demo dapat dibuka dengan menambahkan `?demo=1` pada URL.
