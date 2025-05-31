# Klasifikasi Gambar Bunga (Rose vs Sunflower) menggunakan ResNet18

Proyek ini mendemonstrasikan penggunaan model ResNet18 yang telah dilatih sebelumnya (_pre-trained_) untuk tugas klasifikasi gambar bunga, yaitu membedakan antara bunga mawar (rose) dan bunga matahari (sunflower). Notebook ini mencakup seluruh proses mulai dari pemuatan dataset, pra-pemrosesan data, pelatihan model, evaluasi, hingga prediksi pada gambar baru.

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

Dataset yang digunakan adalah kumpulan gambar bunga yang disusun dalam folder `datasets/train` dengan dua subfolder:

- `rose`: Gambar bunga mawar.
- `sunflower`: Gambar bunga matahari.

Gambar-gambar dimuat menggunakan `ImageFolder` dari torchvision.

## Arsitektur Model

Model yang digunakan adalah ResNet18, sebuah Convolutional Neural Network (CNN) populer, dengan bobot yang telah dilatih sebelumnya pada dataset ImageNet (`ResNet18_Weights.DEFAULT`). Lapisan _fully connected_ (fc) terakhir dari ResNet18 dimodifikasi menjadi `nn.Linear` dengan 2 output, sesuai jumlah kelas (rose, sunflower).

- Total parameter model: ~11.18M
- Parameter yang dapat dilatih: ~11.18M

## Pra-pemrosesan Data

Setiap gambar dalam dataset melewati serangkaian transformasi sebelum dimasukkan ke model:

1. Ukuran gambar diubah menjadi 224x224 piksel.
2. Gambar dikonversi menjadi Tensor PyTorch.
3. Normalisasi gambar menggunakan mean `[0.485, 0.456, 0.406]` dan standar deviasi `[0.229, 0.224, 0.225]`.

Dataset kemudian dibagi menjadi data latih (80%) dan data validasi (20%). `DataLoader` digunakan untuk memuat data dalam batch berukuran 32.

## Pelatihan Model

- **Device**: Model dilatih menggunakan CUDA (GPU) jika tersedia, jika tidak maka menggunakan CPU.
- **Loss Function**: `nn.CrossEntropyLoss` digunakan sebagai fungsi kerugian.
- **Optimizer**: `optim.Adam` digunakan sebagai optimizer dengan laju pembelajaran (learning rate) `1e-3`.
- **Epoch**: Model dilatih selama 10 epoch.

Selama pelatihan, kerugian (loss) pada data latih dan data validasi, serta akurasi pada data validasi, dicatat setiap epoch. Model beserta bobot optimizer dan riwayat loss disimpan dalam file `flower_classifier_checkpoint.pth`.

## Hasil

Setelah 10 epoch pelatihan, model mencapai hasil sebagai berikut (contoh output):

- **Epoch 10**:
  - Train Loss: 0.0380
  - Val Loss: 0.0604
  - Val Accuracy: 0.9750(97.50%)

Kerugian pada data latih dan validasi menunjukkan tren penurunan yang baik, mengindikasikan bahwa model belajar dengan efektif.

## Prediksi

Notebook ini juga menyertakan fungsionalitas untuk memuat model yang telah dilatih dan melakukan prediksi pada gambar baru.

- Fungsi `load_model` digunakan untuk memuat checkpoint model.
- Fungsi `predict_image` mengambil path gambar, melakukan pra-pemrosesan yang sama seperti saat pelatihan, dan menghasilkan prediksi kelas (`rose` atau `sunflower`).

Contoh prediksi dilakukan pada gambar `datasets/test/mawartest.jpg`.

## Visualisasi

- **Loss Plot**: Kurva kerugian (loss) data latih dan data validasi per epoch divisualisasikan menggunakan Matplotlib untuk memantau proses pembelajaran model.
- **Accuracy Plot**: Kurva akurasi validasi per epoch.
- **Confusion Matrix**: Matriks kebingungan untuk evaluasi performa model pada data validasi.
- **Prediction Display**: Gambar yang diprediksi ditampilkan beserta label prediksinya menggunakan Matplotlib.

## Ketergantungan

Proyek ini menggunakan pustaka Python berikut:

- `torch`
- `torchvision`
- `matplotlib`
- `numpy`
- `scikit-learn`
- `seaborn`
- `Pillow`

## Cara Menjalankan

1. **Persiapan Dataset**: Pastikan dataset bunga tersedia pada path `datasets/train` dengan struktur folder sesuai kelas.
2. **Instalasi Ketergantungan**: Instal semua pustaka yang tercantum di atas.
3. **Menjalankan Notebook**:

- Untuk melatih model dari awal, jalankan semua sel notebook secara berurutan.
- Untuk melakukan prediksi menggunakan model yang telah dilatih (pastikan file `flower_classifier_checkpoint.pth` ada):
- Jalankan sel-sel yang berisi definisi fungsi `load_model` dan `predict_image`.
- Modifikasi `img_path` pada bagian prediksi untuk menunjuk ke gambar yang ingin diprediksi.
- Jalankan sel tersebut untuk melihat hasil prediksi dan visualisasi gambar.
