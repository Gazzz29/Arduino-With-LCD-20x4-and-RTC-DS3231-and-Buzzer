# Jam Digital dengan LCD 20x4, RTC DS3231, dan Buzzer

Proyek Arduino yang menampilkan jam digital lengkap dengan tanggal dan waktu real-time menggunakan modul RTC DS3231 dan layar LCD 20x4.

## Fitur Utama

✅ **Tampilan Real-Time Clock** - Menampilkan hari, tanggal, dan waktu (jam:menit:detik)  
✅ **Nama Hari Bahasa Indonesia** - Menampilkan hari dalam bahasa lokal  
✅ **Buzzer Audio** - Nada suara setiap detik sebagai indikasi real-time  
✅ **LCD 20x4** - Layar LCD 4 baris x 20 kolom untuk tampilan yang jelas  
✅ **Backup Baterai** - Modul RTC DS3231 memiliki baterai internal

## Komponen Hardware

| Komponen | Jumlah | Fungsi |
|----------|--------|--------|
| Arduino Uno | 1 | Mikrokontroller utama |
| LCD 20x4 | 1 | Tampilan output |
| RTC DS3231 | 1 | Real-Time Clock dengan I2C |
| Buzzer | 1 | Output audio setiap detik |
| Breadboard | 1 | Tempat perakitan |
| Kabel Jumper | Sesuai | Penghubung antar komponen |

## Koneksi Pin Arduino

### LCD 20x4 (Mode 4-bit)
| Pin LCD | Pin Arduino | Catatan |
|---------|-------------|---------|
| RS | 7 | Register Select |
| EN | 6 | Enable |
| D4 | 5 | Data 4 |
| D5 | 4 | Data 5 |
| D6 | 3 | Data 6 |
| D7 | 2 | Data 7 |
| VSS | GND | Ground |
| VDD | 5V | Supply |
| V0 | Potensiometer | Kontras (optional) |

### RTC DS3231
| Pin RTC | Pin Arduino | Catatan |
|---------|-------------|---------|
| SDA | A4 | I2C Data |
| SCL | A5 | I2C Clock |
| VCC | 5V | Supply |
| GND | GND | Ground |

### Buzzer
| Pin Buzzer | Pin Arduino | Catatan |
|-----------|-------------|---------|
| Positif (+) | 8 | PWM Signal |
| Negatif (-) | GND | Ground |

**Catatan:** Pin 10 disiapkan sebagai OUTPUT tetapi tidak digunakan pada versi saat ini.

## Library yang Digunakan

- **LiquidCrystal** (fmalpartida/LiquidCrystal@^1.5.0) - Kontrol LCD 20x4
- **RTClib** (adafruit/RTClib@^2.1.4) - Kontrol RTC DS3231

## Instalasi

### 1. Prasyarat
- Arduino IDE atau PlatformIO
- Arduino Uno
- Driver CH340 (jika menggunakan board clone)

### 2. Clone atau Download Proyek
```bash
git clone <repository-url>
cd "Arduino With LCD 20x4 and RTC DS3231 and Buzzer"
```

### 3. Install Dependencies
Jika menggunakan PlatformIO:
```bash
platformio lib install
```

### 4. Upload ke Arduino
**Menggunakan PlatformIO:**
```bash
platformio run --target upload
```

**Atau menggunakan Arduino IDE:**
- Buka file `src/main.cpp`
- Pilih Board: Arduino Uno
- Pilih Port COM yang sesuai
- Click Upload

## Cara Kerja

1. **Inisialisasi** - Saat pertama kali dihidupkan, program mengecek apakah RTC kehilangan daya
2. **Sinkronisasi Waktu** - Jika RTC kosong, waktu disetel ke waktu kompilasi program
3. **Tampilan LCD** - Program menampilkan:
   - Baris 1: Nama hari, tanggal, bulan, tahun
   - Baris 2: Jam, menit, detik
   - Baris 4: Nama institusi/organisasi
4. **Audio Indikasi** - Buzzer berbunyi pada frekuensi 1000 Hz setiap detik

## Kustomisasi

### Mengubah Nama Institusi
Di dalam `main.cpp`, ubah bagian ini:
```cpp
lcd.print(" SMP BQ Islamic BS Bogor ");
```

### Mengubah Pin Koneksi
Ubah deklarasi pin di bagian atas file:
```cpp
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);  // Ubah sesuai kebutuhan
```

### Menyetel Waktu Manual
Ubah waktu RTC dengan menambahkan kode di setup():
```cpp
rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
// Atau dengan nilai spesifik:
// rtc.adjust(DateTime(2024, 5, 6, 10, 30, 45));
```

## Troubleshooting

| Masalah | Solusi |
|---------|--------|
| LCD tidak menampilkan apapun | Periksa koneksi pin, atur potensiometer kontras |
| RTC tidak menampilkan waktu | Periksa koneksi I2C (SDA/SCL), cek baterai RTC |
| Buzzer tidak berbunyi | Verifikasi pin 8 terhubung, cek polaritas buzzer |
| Arduino tidak terdeteksi | Install driver CH340 atau ganti cable USB |

## Spesifikasi Teknis

- **Board:** Arduino Uno (ATmega328P)
- **Platform:** ATmelavr
- **Kecepatan Clock:** 16 MHz
- **Memory RAM:** 2 KB
- **Memory Flash:** 32 KB
- **Tegangan Operasi:** 5V

## Lisensi

Proyek ini dapat digunakan secara bebas untuk keperluan pendidikan dan pembelajaran.

## Catatan

- RTC DS3231 memiliki akurasi ±2 ppm dan dilengkapi baterai backup
- LCD akan terus menampilkan waktu meskipun Arduino reset (asalkan RTC terhubung dan bertenaga)
- Untuk akurasi maksimal, gunakan baterai berkualitas untuk modul RTC

---

**Versi:** 1.0  
**Last Updated:** Mei 2024  
**Lokasi:** SMP BQ Islamic BS Bogor
