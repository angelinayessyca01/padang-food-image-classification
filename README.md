# Padang Food Image Classification Using Deep Learning

Project Computer Vision untuk mengklasifikasikan gambar ke dalam 9 kategori masakan Padang menggunakan Convolutional Neural Network (CNN) dan Transfer Learning. Project ini membandingkan model CNN baseline, VGG16, dan ConvNeXt, lalu menggunakan model terbaik untuk inference dan aplikasi prediksi berbasis Streamlit.

## Repository Outline

1.  `README.md` - Gambaran umum, tujuan, metode, hasil, dan referensi project.
2.  `notebook.ipynb` - Notebook utama untuk data loading, EDA, preprocessing, training, dan evaluasi model.
3.  `notebook_inference.ipynb` - Notebook untuk menguji model terbaik menggunakan gambar inference.
4.  `images/` - Contoh gambar masakan Padang yang digunakan pada proses inference.
5.  `deployment/prediction.py` - Script aplikasi Streamlit untuk memprediksi jenis masakan dari gambar yang diunggah.
6.  `deployment/requirements.txt` - Daftar library yang dibutuhkan untuk menjalankan aplikasi.
7.  `url.txt` - Tautan dataset, model, dan aplikasi deployment.

## Problem Background

Masakan Padang memiliki banyak jenis makanan dengan warna, bentuk, tekstur, dan penyajian yang terkadang terlihat mirip. Kondisi ini dapat menyulitkan orang yang belum familiar dengan masakan Padang, termasuk wisatawan, saat mencoba mengenali jenis makanan hanya dari gambar.

Project ini menggunakan pendekatan Computer Vision untuk membangun model klasifikasi gambar. Pengguna dapat mengunggah gambar masakan dan memperoleh prediksi kategori makanan beserta nilai confidence dari model.

## Project Output

Project ini menghasilkan model klasifikasi gambar dan aplikasi web untuk memprediksi 9 jenis masakan Padang.

Model yang dibandingkan adalah CNN baseline, VGG16 dengan Transfer Learning, dan ConvNeXt Small dengan Transfer Learning. Berdasarkan evaluasi pada test set, VGG16 menjadi model terbaik.

| Model                            | Test Accuracy |
|----------------------------------|--------------:|
| CNN Baseline                     |           68% |
| VGG16 Transfer Learning          |           87% |
| ConvNeXt Small Transfer Learning |           82% |

Selain menghasilkan akurasi tertinggi sebesar 87%, VGG16 memperoleh macro F1-score 0,87. ConvNeXt Small memperoleh macro F1-score 0,81. Ringkasan hasil project tidak mencantumkan macro F1-score CNN baseline.

VGG16 dipilih karena menghasilkan akurasi dan macro F1-score tertinggi di antara model yang diuji. Model ini kemudian digunakan untuk inference dan deployment.

Pada pengujian inference terhadap 9 gambar contoh, seluruh gambar diprediksi sesuai dengan kelas sebenarnya. Delapan gambar memperoleh confidence 100%, sedangkan gambar `gulai_tambusu` memperoleh confidence 99,58%. Hasil inference ini hanya menggambarkan sampel yang diuji dan tidak berarti akurasi model secara keseluruhan mencapai 100%.

Aplikasi demo dapat diakses melalui tautan berikut:

**[Padang Food Prediction
App](https://padangfoodprediction.streamlit.app/)**

## Data

Dataset yang digunakan adalah **Padang Cuisine (Indonesian Food Image Dataset)** dari Kaggle. Dataset ini berisi 993 gambar yang terbagi ke dalam 9 kelas masakan Padang.

Kelas yang digunakan:

1.  `ayam_goreng`
2.  `ayam_pop`
3.  `daging_rendang`
4.  `dendeng_batokok`
5.  `gulai_ikan`
6.  `gulai_tambusu`
7.  `gulai_tunjang`
8.  `telur_balado`
9.  `telur_dadar`

Setiap kelas memiliki sekitar 103 sampai 119 gambar, sehingga jumlah gambar antar kelas relatif seimbang. Gambar memiliki ukuran yang bervariasi dan perlu diseragamkan sebelum masuk ke model.

Dataset dibagi menjadi tiga subset dengan rasio 70:15:15:

| Subset     | Jumlah Gambar | Proporsi |
|:-----------|--------------:|---------:|
| Training   |           691 |      70% |
| Validation |           144 |      15% |
| Testing    |           158 |      15% |
| **Total**  |       **993** | **100%** |

Dataset lengkap tidak disimpan di repository. Notebook utama mengambil dataset dari sumber Kaggle. Folder `images/` berisi contoh gambar yang digunakan pada tahap inference.

**Sumber dataset:** [Padang Cuisine on Kaggle](https://www.kaggle.com/datasets/faldoae/padangfood)

## Method

Tahapan yang dilakukan dalam project ini:

1.  **Data Loading** - Mengambil dataset dan memeriksa jumlah gambar pada setiap kelas.
2.  **Exploratory Data Analysis (EDA)** - Mengamati sampel gambar, warna, tekstur, dimensi, sudut pengambilan gambar, posisi objek, dan variasi background.
3.  **Feature Engineering** - Membagi data menjadi training, validation dan testing dengan rasio 70:15:15. Pembagian menggunakan random seed agar dapat direproduksi.
4.  **Image Preprocessing** - Mengubah ukuran gambar menjadi 224 × 224 piksel dan menyesuaikan preprocessing dengan model yang digunakan.
5.  **Data Augmentation** - Menerapkan rotasi, zoom, pergeseran posisi, shear, dan horizontal flip pada data training.
6.  **CNN Baseline** - Melatih model CNN sebagai model pembanding awal.
7.  **Transfer Learning** - Menggunakan VGG16 dan ConvNeXt Small dengan bobot pretrained ImageNet.
8.  **Model Evaluation** - Membandingkan performa model menggunakan accuracy dan classification report, termasuk macro F1-score.
9.  **Model Selection** - Memilih VGG16 sebagai model terbaik berdasarkan hasil evaluasi pada test set.
10. **Model Inference** - Menguji model terpilih menggunakan gambar yang tidak digunakan pada proses training, validation, atau testing.
11. **Deployment** - Menyediakan aplikasi Streamlit untuk menerima unggahan gambar dan menampilkan hasil prediksi beserta confidence.

## Stacks

- **Programming Language:** Python
- **Deep Learning Framework:** TensorFlow dan Keras
- **Data Processing:** NumPy dan Pandas
- **Visualization:** Matplotlib dan Seaborn
- **Model Evaluation:** Scikit-learn
- **Image Processing:** Pillow
- **Deployment:** Streamlit dan gdown
- **Development Environment:** Jupyter Notebook
- **Dataset Source:** Kaggle

## Menjalankan Aplikasi Secara Lokal

Pastikan Python sudah terpasang. Kemudian jalankan perintah berikut dari direktori utama repository:

``` bash
pip install -r deployment/requirements.txt
streamlit run deployment/prediction.py
```

Aplikasi akan memuat model VGG16 dari tautan Google Drive yang dikonfigurasi pada script deployment. Pastikan model dapat diakses melalui tautan tersebut dan koneksi internet tersedia.

## Reference

- **Dataset:** [Padang Cuisine (Indonesian Food Image Dataset)](https://www.kaggle.com/datasets/faldoae/padangfood)
- **Best Model:** [VGG16 Model on Google Drive](https://drive.google.com/file/d/1XA6DRBC27UdDlX4-nEcno_KKeCgVA6Ju/view?usp=sharing)
- **Deployment App:** [Padang Food Prediction on Streamlit](https://padangfoodprediction.streamlit.app/)
