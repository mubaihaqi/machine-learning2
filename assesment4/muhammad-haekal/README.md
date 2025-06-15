# Klasifikasi Gambar Hewan dengan MobileNetV2

Proyek ini merupakan implementasi deep learning untuk mengklasifikasi gambar hewan menggunakan arsitektur **MobileNetV2** dengan teknik **transfer learning**. Dataset diambil dari Kaggle dan terdiri dari 3 kelas hewan.

## Fitur
- Menggunakan model pretrained MobileNetV2
- Preprocessing dan augmentasi data dengan `ImageDataGenerator`
- Evaluasi model dengan akurasi, confusion matrix, dan classification report
- Dapat dijalankan langsung di Google Colab

## Struktur Dataset
Dataset berasal dari Kaggle: [`nicopalv/dataset-klasifikasi-gambar-hewan`](https://www.kaggle.com/datasets/nicopalv/dataset-klasifikasi-gambar-hewan)

Struktur folder setelah ekstraksi:
```
hewan_dataset/
└── dataset/
    ├── training_set/
    │   ├── kucing/
    │   ├── anjing/
    │   └── kelinci/
    └── test_set/
        ├── kucing/
        ├── anjing/
        └── kelinci/
```

## Cara Menjalankan

1. **Buka Google Colab**, lalu unggah file notebook `.ipynb`.
2. **Install dan autentikasi Kaggle**:
    ```python
    !pip install kaggle
    from google.colab import files
    files.upload()  # upload kaggle.json
    !mkdir -p ~/.kaggle
    !cp kaggle.json ~/.kaggle/
    !chmod 600 ~/.kaggle/kaggle.json
    ```
3. **Unduh dan ekstrak dataset**:
    ```python
    !kaggle datasets download -d nicopalv/dataset-klasifikasi-gambar-hewan
    !unzip dataset-klasifikasi-gambar-hewan.zip -d hewan_dataset
    ```
4. **Jalankan seluruh sel notebook** dari atas ke bawah.

## Evaluasi
Model dievaluasi menggunakan:
- Grafik akurasi per epoch
- Confusion Matrix
- Classification Report (Precision, Recall, F1-score)

## Lisensi
Proyek ini digunakan untuk keperluan pembelajaran dan penelitian.
