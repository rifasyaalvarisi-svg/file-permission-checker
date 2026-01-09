# File Permission Checker

![Version](https://img.shields.io/badge/Version-2.0.0-blue)
![Python](https://img.shields.io/badge/Python-3.8+-green)
![PyQt6](https://img.shields.io/badge/PyQt6-6.6+-purple)
![License](https://img.shields.io/badge/License-MIT-yellow)

Aplikasi desktop PyQt6 untuk memindai, menganalisis, dan mengamankan izin file pada sistem berbasis Unix. Fitur antarmuka pengguna modern dengan tema gelap dan desain glassmorphism, analisis risiko real-time, enkripsi aman, manajemen backup, dan verifikasi integritas yang komprehensif.

## 🌟 Fitur

### Pemindai Izin
- **Pemindaian Real-time**: Analisis izin file dengan pelacakan progres
- **Klasifikasi Risiko**: Kategorikan file secara otomatis menjadi Risiko Tinggi, Sedang, atau Rendah
- **Deteksi Cerdas**: Identifikasi file sensitif (kunci, kredensial, konfigurasi, dll.)
- **Mode Simbolik & Oktal**: Tampilkan izin dalam kedua format
- **Penyaringan & Pencarian**: Filter berdasarkan tingkat risiko atau cari berdasarkan nama file

### Pipeline Keamanan
- **Alur Kerja Terorkestrasi**: Pindai → Backup → Hash → Enkripsi → Ubah Izin → Verifikasi
- **Kemampuan Rollback**: Rollback otomatis jika terjadi kesalahan
- **Pelacakan Progres**: Pembaruan progres real-time untuk setiap langkah
- **Audit Logging**: Catatan lengkap dari semua operasi

### Sistem Enkripsi
- **Enkripsi Fernet (AES-128-CBC)**: Enkripsi simetrik yang aman
- **Meter Kekuatan Kata Sandi**: Analisis kekuatan kata sandi real-time
- **Pembatasan Tingkat**: Perlindungan terhadap serangan brute-force (5 percobaan/5 menit)
- **Penanganan Memori Aman**: Data sensitif ditangani dengan buffer memori aman
- **Sistem Karantina**: File asli dipindahkan ke folder `.quarantine/`
- **Pemrosesan Batch**: Enkripsi/dekripsi banyak file dan folder

### Manajemen Backup
- **Backup Otomatis**: Buat backup sebelum perubahan izin
- **Riwayat Versi**: Lacak riwayat backup dengan timestamp
- **Pemulihan Satu Klik**: Pulihkan file dari riwayat backup
- **Verifikasi SHA-256**: Verifikasi integritas backup

### Verifikasi Integritas
- **Hashing SHA-256**: Hitung dan verifikasi hash file
- **Audit Logging**: Catat semua peristiwa keamanan dengan checksum
- **Integritas Database**: Verifikasi integritas database SQLite
- **Kepatuhan CIA Triad**: Status Confidentiality, Integrity, Availability

### Export & Pelaporan
- **Export CSV**: Ekspor hasil pemindaian ke format CSV
- **Export JSON**: Ekspor laporan detail dengan statistik
- **File Checksum**: Hasilkan file checksum `.sha256` untuk verifikasi

## 📋 Persyaratan

- **Python**: 3.8 atau lebih tinggi
- **PyQt6**: 6.6 atau lebih tinggi
- **cryptography**: Untuk enkripsi/dekripsi
- **Linux/Unix**: Sistem izin file diperlukan (bukan Windows)

## 🚀 Instalasi

```bash
# Kloning repositori
git clone https://github.com/rifasyaalvarisi-svg/file-permission-checker
cd file-permission-checker

# Buat virtual environment
python -m venv venv
source venv/bin/activate

# Instal dependensi
pip install -r requirements.txt

# Jalankan aplikasi
python main.py
```

## 📖 Penggunaan

### Mulai Cepat

1. **Luncuran Aplikasi**
   ```bash
   python main.py
   ```

2. **Pindai Folder**
   - Seret & jatuhkan folder ke jendela, ATAU
   - Klik "Browse" untuk memilih folder, ATAU
   - Masukkan path secara manual dan tekan Enter

3. **Lihat Hasil**
   - File ditampilkan dalam tabel yang dapat diurutkan
   - Indikator risiko: 🔴 Tinggi, ⚠️ Sedang, ✅ Rendah
   - Gunakan filter untuk menampilkan file berisiko saja

4. **Perbaiki Izin**
   - Klik "Harden Permissions" untuk perbaikan otomatis, ATAU
   - Pilih file tertentu dan klik "Harden Selected"
   - Pilih perbaikan cepat atau pengaturan lanjutan

### Tab Enkripsi

1. **Tambah File/Folder**
   - Klik "Add Files" untuk file individual
   - Klik "Add Folder" untuk menambah semua file secara rekursif

2. **Masukkan Kata Sandi**
   - Gunakan kolom kata sandi
   - Klik "Generate Secure Password" untuk kata sandi acak
   - Periksa indikator kekuatan

3. **Enkripsi/Dekripsi**
   - Beralih antara mode Enkripsi/Dekripsi
   - Klik tombol proses untuk memulai

### Tab Backup

1. **Buat Backup**
   - Pilih folder atau file
   - Klik "Create Backup"

2. **Pulihkan**
   - Pilih backup dari riwayat
   - Klik "Restore Selected"
   - Pilih folder tujuan

## 🎨 Struktur Proyek

```
file-permission-checker/
├── main.py                     # Titik masuk aplikasi & layar splash
├── style.qss                   # Qt stylesheet (tema gelap)
├── scan_history.db             # Database SQLite (dibuat otomatis)
├── core/
│   ├── __init__.py
│   ├── scanner.py              # Pemindaian file dengan analisis risiko
│   ├── permission_fixer.py     # Logika modifikasi izin
│   ├── security.py             # Manajemen kata sandi & enkripsi
│   ├── encryption_manager.py   # Worker enkripsi/dekripsi file
│   ├── backup.py               # Pembuatan & pemulihan backup
│   ├── integrity.py            # SHA-256 & audit logging
│   ├── pipeline.py             # Orkestrasi alur kerja
│   ├── database.py             # Operasi SQLite
│   └── secure_memory.py        # Penanganan string/buffer aman
├── ui/
│   ├── __init__.py
│   ├── main_window.py          # Jendela aplikasi utama
│   ├── dialogs.py              # Jendela dialog
│   ├── modern_widgets.py       # Komponen UI kustom
│   └── widget.py               # Widget tambahan
├── utils/
│   ├── __init__.py
│   ├── constants.py            # Konfigurasi & konstanta
│   └── helpers.py              # Fungsi utilitas
├── docs/
│   ├── ARCHITECTURE.md         # Gambaran arsitektur sistem
│   ├── RISK_LEVEL_SPECIFICATION.md
│   ├── RISK_TO_PERMISSION_MAPPING.md
│   └── UI_DESIGN_SYSTEM.md
└── permission_logs/            # Log perubahan izin
```

## ⚙️ Konfigurasi

Aturan kustom dapat didefinisikan di `utils/constants.py`:

```python
# Aturan sensitivitas file (izin oktal)
CUSTOM_RULES = {
    # Sensitivitas tinggi - baca/tulis pemilik saja (600)
    '.env': '600',
    '.key': '600',
    '.pem': '600',
    '.crt': '600',
    'id_rsa': '600',
    'authorized_keys': '600',
    
    # Direktori - pemilik saja (700)
    '.ssh': '700',
    '.gnupg': '700',
    '.git': '700',
}

# Pemetaan risiko ke izin
RISK_TO_PERMISSION = {
    'High': {'file': '600', 'dir': '700'},
    'Medium': {'file': '640', 'dir': '750'},
    'Low': {'file': '644', 'dir': '755'},
}
```

## 🔒 Pipeline Keamanan

Aplikasi menjalankan perubahan izin melalui pipeline yang aman:

```
┌─────────────┐
│    SCAN     │  Validasi file ada
└──────┬──────┘
       ▼
┌─────────────┐
│   BACKUP    │  Buat backup status saat ini
└──────┬──────┘
       ▼
┌─────────────┐
│  HASH_BEFORE│  Hitung SHA-256 sebelum perubahan
└──────┬──────┘
       ▼
┌─────────────┐
│   ENCRYPT   │  Enkripsi backup (opsional)
└──────┬──────┘
       ▼
┌─────────────┐
│    CHANGE   │  Terapkan izin baru
└──────┬──────┘
       ▼
┌─────────────┐
│  HASH_AFTER │  Verifikasi integritas
└──────┬──────┘
       ▼
┌─────────────┐
│   VERIFY    │  Periksa hash cocok (untuk file tidak terenkripsi)
└─────────────┘
       │
       ▼ Jika langkah gagal:
┌─────────────┐
│  ROLLBACK   │  Pulihkan status sebelumnya
└─────────────┘
```

## 📊 Klasifikasi Risiko

File diklasifikasikan berdasarkan **sensitivitas + matriks izin**:

| Sensitivitas | Izin | Tingkat Risiko | Deskripsi |
|-------------|------|----------------|-----------|
| Tinggi | > 600 | 🔴 Tinggi | File sensitif dengan izin longgar |
| Tinggi | ≤ 600 | ✅ Rendah | Sensitif tapi diamankan dengan benar |
| Sedang | > 644 | ⚠️ Sedang | Konfigurasi dengan akses tulis |
| Sedang | ≤ 644 | ✅ Rendah | Konfigurasi diamankan dengan benar |
| Rendah | Apa saja | ✅ Rendah | File tidak sensitif |
| Symlink | Berbahaya | 🔴 Tinggi | Symlink ke path sensitif |

### Deteksi Sensitivitas

**Sensitivitas Tinggi:**
- `.env`, `.key`, `.pem`, `.crt`, `.p12`, `.pfx`
- `id_rsa`, `id_dsa`, `id_ecdsa`, `id_ed25519`
- `authorized_keys`, `known_hosts`
- `.ssh`, `.gnupg`, `private`, `secrets`

**Sensitivitas Sedang:**
- `.conf`, `.config`, `.ini`, `.yaml`, `.yml`
- `.sql`, `.db`, `.sqlite`
- `docker-compose`, `dockerfile`, `nginx.conf`

## ⌨️ Pintasan Keyboard

| Pintasan | Tindakan |
|----------|----------|
| `Ctrl+S` | Mulai pemindaian |
| `Ctrl+F` | Perbaiki izin |
| `Ctrl+E` | Export ke CSV |
| `F5` | Segarkan tampilan |

## 📤 Format Export

### CSV

```csv
Name,Path,Mode,Symbolic,Risk,Expected,Size,Modified
.env,config/.env,644,rw-r--r--,High,600,1.2KB,2025-01-15
```

### JSON

```json
{
  "timestamp": "2025-01-15T10:30:00",
  "stats": {
    "high_risk": 12,
    "medium_risk": 45,
    "low_risk": 443,
    "total_files": 500
  },
  "files": [...]
}
```

## 🔐 Fitur Keamanan

### Detail Enkripsi
- **Algoritma**: Fernet (AES-128-CBC dengan HMAC)
- **Turunan Kunci**: PBKDF2HMAC-SHA256 (480.000 iterasi)
- **Format**: `[salt (16B)][verify_hash (32B)][encrypted_data]`
- **Pembatasan Tingkat**: 5 percobaan per jendela 5 menit

### Penanganan Memori Aman
- Data sensitif disimpan dalam buffer aman
- Penghapusan memori otomatis
- Tidak ada data sensitif di swap

### Audit Logging
- Semua tindakan dicatat dengan checksum SHA-256
- Jejak audit anti-manipulasi
- Tingkat keparahan: info, warning, critical

## 📚 Dokumentasi

Dokumentasi tambahan tersedia di `docs/`:

- **ARCHITECTURE.md**: Gambaran umum arsitektur sistem
- **RISK_LEVEL_SPECIFICATION.md**: Klasifikasi risiko detail
- **RISK_TO_PERMISSION_MAPPING.md**: Rekomendasi izin
- **UI_DESIGN_SYSTEM.md**: Spesifikasi tema dan komponen

## 🤝 Berkontribusi

1. Fork repositori
2. Buat branch fitur (`git checkout -b feature/layanan`)
3. Commit perubahan (`git commit -m 'Tambah layanan menarik'`)
4. Push ke branch (`git push origin feature/layanan`)
5. Buka Pull Request

## 📄 Lisensi

MIT License - lihat [LICENSE](LICENSE) untuk detail.

## 👤 Penulis

**zuckdorsey**
- GitHub: [@zuckdorsey](https://github.com/zuckdorsey)
- Proyek: https://github.com/zuckdorsey/file-perermission-checker

---

**⚠️ Penafian**: Gunakan alat ini dengan risiko Anda sendiri. Selalu backup data penting sebelum membuat perubahan izin.

