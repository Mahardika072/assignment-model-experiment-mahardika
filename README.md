# AI Model Experiment & Evaluation: Sentiment Analysis

Proyek ini bertujuan untuk membandingkan dua pendekatan teknis dalam membangun sistem klasifikasi sentimen ulasan pelanggan (*customer reviews*): **Model Klasik Machine Learning (Scikit-learn)** dan **Large Language Model API (Google Gemini API)**.

---

## 1. Problem Statement & Objective

- **Problem:** Mengklasifikasikan ulasan pelanggan (*customer reviews*) e-commerce ke dalam kategori sentimen biner (`positif` atau `negatif`).
- **Objective:** Mengevaluasi performa (akurasi, precision, recall, F1-score), kecepatan respons (*latency*), efisiensi biaya (*cost*), dan kemudahan implementasi dari kedua pendekatan untuk menentukan solusi terbaik dalam skala produksi[cite: 1].

---

## 2. Ringkasan Hasil Evaluasi

Eksperimen dilakukan menggunakan dataset yang sama (`customer_reviews_sentiment.csv`) dengan pembagian *training set* dan *test set* yang konsisten[cite: 1]. Berikut adalah tabel hasil perbandingan metrik evaluasinya[cite: 1]:

| Model / Pendekatan | Accuracy | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Model Klasik (TF-IDF + Scikit-learn)** | **1.00** | **1.00** | **1.00** | **1.00** |
| **LLM API (Gemini 2.5 Flash)** | 0.55 | 0.30 | 0.55 | 0.39 |

---

## 3. Analisis Trade-off & Limitation

1. **Performa & Akurasi:**
   - **Model Klasik:** Mengalami akurasi sempurna (1.00) pada dataset uji ini[cite: 1].
   - **LLM API:** Akurasi lebih rendah (0.55) karena adanya variasi format teks output dari LLM yang gagal saat dicocokkan secara eksak (*exact match*) dengan label target[cite: 1].

2. **Kecepatan & Effort:**
   - **Model Klasik:** Waktu eksekusi sangat cepat (hitungan milidetik), namun membutuhkan tahap *preprocessing* teks diawal (TF-IDF Vectorizer)[cite: 1].
   - **LLM API:** Tidak membutuhkan pelatihan model (*zero-shot learning*), namun memiliki latensi lebih tinggi karena memanggil API melalui jaringan[cite: 1].

3. **Biaya & Pengoperasian:**
   - **Model Klasik:** Bebas biaya API (*zero cost*) dan dapat berjalan secara *offline* di server lokal[cite: 1].
   - **LLM API:** Berbayar berdasarkan jumlah token (*pay-per-token*) serta rawan terkena batasan kuota (*Rate Limit* / HTTP 429)[cite: 1].

---

## 4. Rekomendasi Technical Approach

**Rekomendasi Utama: Model Klasik (Scikit-learn dengan TF-IDF Vectorizer)**[cite: 1]

**Alasan Rekomendasi:**
1. **Efisiensi & Determinisme:** Untuk tugas klasifikasi sentimen biner tertutup (`positif`/`negatif`), model klasik terbukti jauh lebih akurat, konsisten, dan tidak rawan error parsing output[cite: 1].
2. **Kecepatan & Biaya:** Model klasik jauh lebih hemat biaya untuk skala produksi karena tidak membutuhkan biaya token API berulang dan merespons input dalam hitungan milidetik[cite: 1].

---

## 5. Cara Menjalankan Project

1. **Clone repository ini ke komputer lokal:**
   ```bash
   git clone [https://github.com/USERNAME_GITHUB_MU/NAMA_REPO_MU.git](https://github.com/USERNAME_GITHUB_MU/NAMA_REPO_MU.git)
   cd model-experiment-assignment