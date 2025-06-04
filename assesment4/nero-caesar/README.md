# 🍎🍅 Klasifikasi Apel dan Tomat dengan PyTorch

Repositori ini berisi sebuah notebook Jupyter untuk melatih model klasifikasi gambar sederhana menggunakan PyTorch, yang bertujuan membedakan antara gambar apel dan tomat.

## 📁 Berkas

- `applesandtomatoes.ipynb`: Notebook utama yang mencakup:
  - Pemrosesan dan pemuatan dataset menggunakan `torchvision`
  - Definisi arsitektur model CNN
  - Proses pelatihan dan evaluasi
  - Pelaporan akurasi serta prediksi pada data uji

## 🚀 Cara Menggunakan

1. Kloning repositori dan buka notebook-nya:

   ```bash
   git clone <url-repositori-anda>
   cd <nama-folder>
   jupyter notebook applesandtomatoes.ipynb
   ```

2. Pastikan Anda sudah menginstal pustaka Python yang dibutuhkan:

   ```bash
   pip install torch torchvision matplotlib
   ```

3. Jalankan setiap sel dalam notebook secara berurutan dari atas ke bawah.

## 🧠 Model

Model yang digunakan adalah jaringan saraf konvolusional (CNN) sederhana dengan komponen berikut:
- Lapisan konvolusional
- Fungsi aktivasi ReLU
- MaxPooling
- Lapisan fully connected (linear)

## 📊 Dataset

Dataset diasumsikan berada dalam direktori dengan struktur folder terpisah untuk gambar apel dan tomat, misalnya:

```
./data/train/apples
./data/train/tomatoes
```

Pastikan Anda menyesuaikan path (jalur folder) dalam kode notebook agar sesuai dengan lokasi dataset Anda.

---

✍️ Dibuat dengan ❤️ menggunakan PyTorch dan Jupyter Notebook.
