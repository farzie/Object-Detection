# 🎯 Object Detection — Google Teachable Machine


### Contoh Objek yang Dideteksi

| Kelas | Objek | Sampel |
|-------|-------|--------|
| 🖱️ **Mouse** | Mouse komputer/laptop | 402 |
| 🎮 **Gamepad** | Stik/controller game | 406 |
| 📺 **Remote TV** | Remote kontrol televisi | 397 |
| 🏔️ **Background** | Latar tanpa objek | 404 |

---

## 🚀 Cara Menggunakan

### 1. Clone Repository

```bash
git clone https://github.com/farzie/Object-Detection.git
cd Object-Detection
```

### 2. Struktur Folder

Pastikan semua file berada dalam **satu folder yang sama**:

```
📁 nama-repo/
├── 📄 index.html       ← Halaman utama (this file)
├── 📄 model.json       ← Arsitektur model TensorFlow.js
├── 📄 weights.bin      ← Bobot/parameter model terlatih
├── 📄 metadata.json    ← Label kelas & info model
└── 📄 README.md        ← Dokumentasi ini
```

### 3. Jalankan Lokal

Karena webcam memerlukan HTTPS atau localhost, gunakan salah satu cara berikut:

**Opsi A — VS Code Live Server** *(direkomendasikan)*
```
Install ekstensi "Live Server" → klik kanan index.html → "Open with Live Server"
```

**Opsi B — Python HTTP Server**
```bash
# Python 3
python -m http.server 8000

# Buka: http://localhost:8000
```

**Opsi C — Node.js**
```bash
npx serve .
```


## 📊 Hasil Training

### Parameter Model

| Parameter | Nilai |
|-----------|-------|
| Jumlah Kelas | 4 kelas |
| Total Data | 1.609 gambar |
| Epochs | 100 |
| Learning Rate | 0.001 |
| Batch Size | 16 |
| Arsitektur | MobileNet (Transfer Learning) |
| Input Size | 224 × 224 px |

### Metrik Akhir

| Metrik | Nilai | Status |
|--------|-------|--------|
| Training Accuracy | **100%** | ✅ Sempurna |
| Final Training Loss | **0.0001** | ✅ Sangat rendah |
| Durasi Training | **~80 detik** | ✅ Efisien |
| Overfitting | Tidak terdeteksi | ✅ |
| Underfitting | Tidak terdeteksi | ✅ |

### Hasil Pengujian per Kelas

```
╔══════════════╦═══════════════════╦════════════════╗
║ Objek        ║ Prediksi          ║ Confidence     ║
╠══════════════╬═══════════════════╬════════════════╣
║ 🖱️  Mouse    ║ Mouse             ║ 100%  ████████ ║
║ 🎮  Gamepad  ║ Gamepad           ║ 100%  ████████ ║
║ 📺  Remote   ║ Remote TV         ║ 100%  ████████ ║
║ 🏔️  Latar    ║ Background        ║ 100%  ████████ ║
╚══════════════╩═══════════════════╩════════════════╝
```

> Seluruh kelas mencapai confidence 100% tanpa kebingungan antar kelas.

---

## 🔧 Teknologi

| Library | Versi | Fungsi |
|---------|-------|--------|
| `@tensorflow/tfjs` | 1.3.1 | Runtime inferensi ML |
| `@teachablemachine/image` | 0.8 | Wrapper model TM |
| `MobileNet` | — | Arsitektur CNN base |
| Vanilla JS + CSS | — | UI tanpa framework |

---

## 📁 Deskripsi File Model

### `model.json`
Berisi **arsitektur model** dalam format JSON — definisi layer, konfigurasi, dan referensi ke file weights.

### `weights.bin`
File **bobot biner** hasil training (~5 MB). Berisi semua parameter yang telah dipelajari model dari 1.609 gambar training.

### `metadata.json`
Informasi model meliputi:
```json
{
  "tfjsVersion": "1.7.4",
  "tmVersion": "2.4.14",
  "modelName": "tm-my-image-model",
  "labels": ["Mouse", "Gamepad", "Remote", "Background"],
  "imageSize": 224
}
```

---

## 📖 Metodologi Singkat

```
Data Collection  →  Preprocessing  →  Training  →  Export  →  Deploy
  (Webcam)          (224×224 px)     (100 epoch)   (TFjs)   (GH Pages)
  1.609 imgs         Augmentation    LR = 0.001   3 files   index.html
```

1. **Pengumpulan Data** — Gambar direkam via webcam langsung di Teachable Machine dengan variasi sudut dan pencahayaan.
2. **Training** — MobileNet di-fine-tune dengan parameter epochs=100, lr=0.001, batch=16 langsung di browser.
3. **Evaluasi** — Semua kelas mencapai confidence 100% pada pengujian real-time.
4. **Export** — Model diekspor ke format TensorFlow.js dan dihosting via GitHub Pages.

---

## ⚠️ Troubleshooting

**Model tidak termuat?**
- Pastikan `model.json`, `weights.bin`, dan `metadata.json` ada di folder yang sama dengan `index.html`
- Jangan buka `index.html` dengan double-click (file://) — gunakan server lokal

**Kamera tidak aktif?**
- Izinkan akses kamera di browser saat diminta
- Pastikan tidak ada aplikasi lain yang menggunakan kamera
- Coba refresh halaman

**Prediksi tidak akurat?**
- Pastikan pencahayaan cukup terang
- Posisikan objek di tengah frame
- Jauhkan objek lain dari latar

---


<div align="center">
  <sub>Built with ❤️ using Google Teachable Machine & TensorFlow.js</sub>
</div>
