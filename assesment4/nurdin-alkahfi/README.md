# Klasifikasi Gambar Hewan (Harimau vs Singa) menggunakan ResNet18

Proyek ini mendemonstrasikan penggunaan model ResNet18 yang telah dilatih sebelumnya untuk tugas klasifikasi gambar hewan, yaitu membedakan antara harimau dan singa. Notebook ini mencakup proses pemuatan dataset, pra-pemrosesan, pelatihan model, evaluasi performa, hingga prediksi gambar baru.

## Daftar Isi

- [Dataset](#dataset)
- [Arsitektur Model](#arsitektur-model)
- [Pra-pemrosesan Data](#pra-pemrosesan-data)
- [Pelatihan Model](#pelatihan-model)
- [Hasil](#hasil)
- [Prediksi](#prediksi)
- [Visualisasi](#visualisasi)
- [Ketergantungan](#ketergantungan)
- [Cara Menjalankan](#cara-menjalankan)

## Dataset

Struktur direktori dataset:


Data dimuat menggunakan `ImageFolder` dari `torchvision.datasets`, dan dibagi menjadi 80% data latih dan 20% data validasi.

## Arsitektur Model

Model menggunakan `ResNet18` dari PyTorch dengan bobot pre-trained dari ImageNet. Lapisan fully connected terakhir diubah menjadi `nn.Linear` dengan 2 output (kelas `tiger` dan `lion`).

- **Total parameter**: ~11.18 juta
- **Parameter yang dilatih**: seluruh parameter

## Pra-pemrosesan Data

Transformasi yang dilakukan terhadap setiap gambar:

1. Resize ke 224x224 piksel
2. Konversi ke Tensor
3. Normalisasi dengan mean `[0.485, 0.456, 0.406]` dan std `[0.229, 0.224, 0.225]`

Batch data diload dengan ukuran batch 32.

## Pelatihan Model

- **Device**: CUDA (GPU) jika tersedia
- **Loss Function**: `nn.CrossEntropyLoss`
- **Optimizer**: `Adam` dengan learning rate `1e-3`
- **Jumlah Epoch**: 10
- **Checkpoint**: Model disimpan dalam file `.pth` setelah pelatihan

## Hasil

Model menunjukkan performa yang sangat baik:

- **Akurasi Validasi**: sekitar 92–95%
- **Loss Train/Validasi**: menurun stabil setiap epoch
- **Confusion Matrix**: menunjukkan model mampu membedakan dua kelas dengan baik

## Prediksi

Notebook menyediakan fungsi prediksi:

- `load_model(filepath)`: Memuat model dari checkpoint
- `predict_image(img_path)`: Melakukan pra-pemrosesan dan prediksi

Contoh prediksi dilakukan terhadap gambar dalam folder `datasets/test/`.

## Visualisasi

Notebook menampilkan:

- Grafik Loss per epoch (train vs validation)
- Grafik Akurasi
- Confusion Matrix
- Gambar prediksi dan label prediksinya

## Ketergantungan

Pastikan Anda telah menginstal pustaka berikut:

```bash
pip install torch torchvision matplotlib numpy scikit-learn Pillow seaborn

Cara Menjalankan
Persiapkan Dataset
Letakkan data dalam datasets/train dengan subfolder lion dan tiger. Dataset harus dalam format gambar.

Jalankan Notebook
Gunakan Jupyter atau Colab untuk membuka dan menjalankan notebook klasifikasi hewan tiger,lion.ipynb.

Prediksi Gambar Baru
Pastikan file checkpoint model tersedia (.pth) dan sesuaikan path gambar pada fungsi predict_image.


Jika Anda ingin, saya juga bisa menyimpan isi ini ke dalam file `README.md` dan mengembalikannya sebagai file unduhan. Ingin saya lakukan? ​:contentReference[oaicite:0]{index=0}​
