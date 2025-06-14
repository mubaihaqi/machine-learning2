Klasifikasi Gambar Hewan (Harimau vs Singa) menggunakan ResNet18


Proyek ini menunjukkan penerapan model ResNet18 yang telah dilatih sebelumnya (pre-trained) untuk tugas klasifikasi gambar hewan, khususnya untuk membedakan antara harimau dan singa. Notebook ini mencakup proses lengkap mulai dari pemuatan data, pra-pemrosesan, pelatihan model, evaluasi performa, hingga prediksi terhadap gambar baru.


Daftar Isi
Dataset

Arsitektur Model

Pra-pemrosesan Data

Pelatihan Model

Hasil

Prediksi

Visualisasi

Ketergantungan

Cara Menjalankan



Dataset
Dataset terdiri dari dua kelas hewan:

tiger: Gambar-gambar harimau.

lion: Gambar-gambar singa.

Struktur folder dataset berada dalam direktori datasets/train:

bash
Copy
Edit
datasets/train/
├── lion/
└── tiger/
Dataset dimuat menggunakan ImageFolder dari torchvision.datasets.

Arsitektur Model
Model yang digunakan adalah ResNet18, arsitektur CNN populer yang telah dilatih pada ImageNet. Lapisan fully connected terakhir diubah untuk menghasilkan dua output kelas:

python
Copy
Edit
model.fc = nn.Linear(model.fc.in_features, 2)
Parameter total: ~11.18 juta

Parameter dapat dilatih: ~11.18 juta

Pra-pemrosesan Data
Transformasi data yang dilakukan meliputi:

Resize gambar ke ukuran 224x224 piksel

Konversi ke Tensor

Normalisasi dengan nilai mean [0.485, 0.456, 0.406] dan std [0.229, 0.224, 0.225]

Data dibagi menjadi 80% data latih dan 20% data validasi. DataLoader digunakan dengan ukuran batch 32.

Pelatihan Model
Device: CUDA (GPU) jika tersedia, atau fallback ke CPU

Loss Function: CrossEntropyLoss

Optimizer: Adam dengan learning rate 1e-3

Epochs: 10

Model dan optimizer disimpan dalam checkpoint animal_classifier_checkpoint.pth.

Hasil
Setelah 10 epoch, model menunjukkan performa yang baik. Berdasarkan hasil evaluasi pada data validasi:

Loss Validasi Akhir: ~0.07

Akurasi Validasi: >90%

Model stabil dan tidak menunjukkan overfitting signifikan

Prediksi
Fungsi prediksi memungkinkan untuk menguji gambar baru:

python
Copy
Edit
predict_image(img_path)
Fungsi akan melakukan pra-pemrosesan yang sama

Menampilkan label hasil prediksi: lion atau tiger

Visualisasi
Notebook menyertakan visualisasi:

Loss Plot: Menunjukkan penurunan loss per epoch

Accuracy Plot: Akurasi validasi per epoch

Confusion Matrix: Evaluasi prediksi kelas

Sample Prediction: Menampilkan gambar yang diprediksi dan label hasil klasifikasi

Ketergantungan
Proyek ini menggunakan pustaka Python berikut:

torch

torchvision

matplotlib

numpy

scikit-learn

seaborn

Pillow

Cara Menjalankan
Persiapan Dataset
Siapkan folder datasets/train dengan dua subfolder: lion dan tiger, masing-masing berisi gambar sesuai kelas.

Instalasi Ketergantungan
Instal semua library yang disebutkan di atas, bisa menggunakan pip:

bash
Copy
Edit
pip install torch torchvision matplotlib numpy scikit-learn seaborn pillow
Menjalankan Notebook

Jalankan notebook klasifikasi hewan tiger,lion.ipynb dari awal hingga akhir.

Untuk prediksi gambar baru, sesuaikan img_path pada bagian prediksi dan jalankan sel terkait.
