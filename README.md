👤 Identitas
Nama : Dewi Eka Febriani
NIM : 4222411003
RE MALAM A- SEMESTER 5

# 🤖 Robot Penyapu Tangga - Transfer Learning

## Deskripsi Proyek

Proyek ini merupakan pengembangan sistem klasifikasi gambar untuk mendukung robot penyapu tangga.

Robot dirancang untuk membersihkan permukaan tangga menggunakan **sikat (brush) berputar, bukan vacuum**. Sistem klasifikasi gambar digunakan untuk mengenali kondisi lingkungan yang berkaitan dengan robot, yaitu:

- **Tangga**
- **Kotoran**
- **Penghalang**

Metode yang digunakan adalah **Transfer Learning** dengan arsitektur **MobileNetV2** yang telah dilatih menggunakan dataset ImageNet.

---

## 🎯 Tujuan

Tujuan proyek ini adalah:

1. Mengumpulkan dataset yang relevan dengan robot penyapu tangga.
2. Melakukan preprocessing dan pembagian dataset.
3. Membangun model klasifikasi gambar menggunakan Transfer Learning.
4. Melatih model untuk mengenali tangga, kotoran, dan penghalang.
5. Mengevaluasi performa model menggunakan data testing.
6. Mendokumentasikan hasil proyek dalam repository GitHub.

---

## 🗂️ Dataset

Proyek menggunakan tiga kategori gambar:

| Kelas | Keterangan |
|---|---|
| `tangga` | Gambar tangga atau permukaan tangga |
| `kotoran` | Gambar sampah/kotoran yang dapat ditemukan di lingkungan |
| `penghalang` | Gambar objek yang dapat menjadi penghalang robot |

### Sumber Dataset

**1. Stairs Object Detection Dataset**

- Sumber: Roboflow
- Pembuat: Tom Lai
- Jumlah gambar: 1.567
- Kelas yang digunakan: `stairs`
- Lisensi: CC BY 4.0

Sumber:
https://universe.roboflow.com/tom-lai-8bp7n/stairs-i2yia

**2. TrashNet**

Digunakan kategori `trash` sebagai sumber gambar kotoran/sampah.

Sumber:
https://github.com/garythung/trashnet

**3. Indoor Obstacles Dataset**

Digunakan kelas `unknown obstacle` sebagai sumber gambar penghalang.

- Lisensi: CC BY 4.0

Sumber:
https://universe.roboflow.com/project-wcqez/indoor-obstacles/dataset/1

Informasi sumber dataset juga tersedia pada:

`dataset/SUMBER_DATASET.md`

---

## 📊 Pembagian Dataset

Dataset dibagi menjadi:

- **70% Training**
- **15% Validation**
- **15% Testing**

Pembagian dataset dilakukan menggunakan:
dataset/
├── train/
│   ├── tangga/
│   ├── kotoran/
│   └── penghalang/
│
├── validation/
│   ├── tangga/
│   ├── kotoran/
│   └── penghalang/
│
└── test/
    ├── tangga/
    ├── kotoran/
    └── penghalang/
src/prepare_dataset.py# robot-penyapu-tangga
Arsitektur model:
Input Image
     ↓
MobileNetV2
     ↓
Global Average Pooling
     ↓
Dropout
     ↓
Dense Layer
     ↓
Softmax
     ↓
3 Classes
Kelas output:
1. tangga
2. kotoran
3. penghalang

   Teknologi yang Digunakan:
1. Python 3.12
2. TensorFlow 2.21
3. Keras
4. MobileNetV2
5. NumPy
5. Pandas
6. Matplotlib
7. Scikit-learn
8. Pillow
9. Jupyter Notebook

   Install seluruh library dengan:
   py -3.12 -m pip install -r requirements.txt
   

Setelah training selesai, model akan disimpan di:
model/robot_penyapu_tangga.keras

Untuk mengevaluasi model:
py -3.12 src/evaluate.py

Evaluasi menggunakan dataset testing.

Hasil Pengujian
Kelas	Precision	Recall	F1-Score	Support
Tangga	1.00	1.00	1.00	236
Kotoran	1.00	1.00	1.00	22
Penghalang	1.00	0.83	0.91	6

Hasil accuracy keseluruhan pada data testing dibulatkan menjadi 1.00.

Hasil tersebut merupakan hasil pengujian pada dataset yang digunakan dalam proyek. Performa pada kondisi lingkungan nyata dapat berbeda sehingga diperlukan pengujian menggunakan data lapangan.
🔎 Prediksi Gambar

Untuk melakukan prediksi terhadap satu gambar:

py -3.12 src/predict.py --image "path/gambar.jpg"
Program akan menampilkan kelas hasil prediksi dan probabilitasnya.

📓 Jupyter Notebook

Notebook Transfer Learning tersedia di:

notebook/transfer_learning_robot_penyapu_tangga.ipynb

Notebook berisi proses:

Import library
Persiapan dataset
Loading dataset
Pembuatan model MobileNetV2
Training model
Evaluasi model
Visualisasi hasil
📁 Struktur Repository
robot-penyapu-tangga/
│
├── dataset/
│   ├── train/
│   ├── validation/
│   ├── test/
│   └── SUMBER_DATASET.md
│
├── model/
│   └── robot_penyapu_tangga.keras
│
├── notebook/
│   └── transfer_learning_robot_penyapu_tangga.ipynb
│
├── src/
│   ├── prepare_dataset.py
│   ├── train.py
│   ├── evaluate.py
│   ├── predict.py
│   └── utils.py
│
├── results/
│
├── dokumentasi/
│
├── README.md
├── requirements.txt
└── .gitignore
🤖 Konsep Robot

Robot penyapu tangga menggunakan sistem sikat (brush) berputar untuk membersihkan debu dan kotoran pada permukaan tangga.

Konsep utama robot:

Sikat berputar untuk menyapu kotoran.
Sistem roda untuk membantu robot bergerak di tangga.
Sensor untuk mendeteksi lingkungan.
Tempat penampungan hasil sapuan.
Sistem kontrol otomatis/manual.
Sistem klasifikasi gambar untuk mengenali kondisi lingkungan.

Dokumentasi desain robot tersedia pada folder:

dokumentasi/🔄 Cara Kerja Sistem

Secara umum sistem bekerja sebagai berikut:

Kamera
   ↓
Mengambil Gambar
   ↓
Preprocessing
   ↓
Model MobileNetV2
   ↓
Klasifikasi
   ↓
Tangga / Kotoran / Penghalang
   ↓
Informasi untuk Sistem Robot
📌 Kesimpulan

Proyek ini berhasil membangun sistem klasifikasi gambar menggunakan metode Transfer Learning dengan MobileNetV2.

Model digunakan untuk mengenali tiga kategori yang relevan dengan robot penyapu tangga, yaitu tangga, kotoran, dan penghalang.

Model telah dilatih dan dievaluasi menggunakan dataset training, validation, dan testing. Hasil pengujian menunjukkan bahwa model dapat melakukan klasifikasi pada data testing yang digunakan.

Pengujian menggunakan gambar dari lingkungan nyata tetap diperlukan untuk mengetahui performa sistem sebelum diterapkan secara langsung pada robot.

📚 Referensi
TensorFlow — https://www.tensorflow.org/
MobileNetV2 — https://keras.io/api/applications/mobilenet/
Roboflow Stairs Dataset — https://universe.roboflow.com/tom-lai-8bp7n/stairs-i2yia
TrashNet — https://github.com/garythung/trashnet
Roboflow Indoor Obstacles — https://universe.roboflow.com/project-wcqez/indoor-obstacles/dataset/1

