> **Materi:** *"Make Sense of Data with Analysis and AI"*  
> **Narasumber:** Andria Arisal, ST., M.Eng. (Pusat Riset Sains Data dan Informasi - BRIN)  
> **Penyelenggara:** Informatics Practitioner Lecture Series Program Studi Informatika, Universitas Bengkulu  
> **Tautan Video Webinar:** [YouTube Live - Informatics Practitioner Lecture Series](https://www.youtube.com/live/WeIWNNO5vbk?si=iq5hTnBXM42NXQIa)

---

## 📌 Ringkasan Studi Kasus

PT Maju Bersama (perusahaan distributor barang) menghadapi krisis finansial dalam kurun waktu 2 tahun terakhir:
* **Sales Revenue (Pendapatan):** Mengalami peningkatan.
* **Net Profit (Keuntungan Bersih):** Menurun sebesar **14%**.
* **Receivables (Piutang / Tagihan Belum Terbayar):** Melonjak tajam sebesar **300%**.
* **Operating Cash Flow:** Mengalami penurunan signifikan.

### **Pertanyaan Bisnis Manajemen**
> *"Mengapa pendapatan perusahaan terus naik, namun profit bersih dan arus kas justru turun drastis?"*

### **Solusi Data Science**
Menggunakan kerangka kerja **CRISP-DM** (*Cross-Industry Standard Process for Data Mining*) untuk menganalisis data transaksi, membangun model *Machine Learning* pemprediksi keterlambatan pembayaran (*Late Payment*), dan memberikan rekomendasi strategi mitigasi risiko kredit.

---

## 🔄 Metodologi CRISP-DM

Proyek ini dilaksanakan mengikuti 6 tahapan standar CRISP-DM:

```
[Business Understanding] ➡️ [Data Understanding] ➡️ [Data Preparation]
                                                            ⬇️
[Deployment / Decision]  ⬅️  [Evaluation]        ⬅️ [Modeling]
```

1. **Business Understanding:** Identifikasi masalah *cash flow*, penumpukan piutang, dan penurunan laba di tengah naiknya pendapatan.
2. **Data Understanding:** Menganalisis granularitas data transaksi PT Maju Bersama (120 Customer, 24 Produk, ~4.000 Invoice, dan ~24.000 Line Items).
   > *Catatan:* Pada skrip koding Python, digunakan simulasi data sintetik sebanyak 4.000 sampel invoice yang merepresentasikan pola dan struktur karakteristik dari populasi data transaksi tersebut.
3. **Data Preparation:** Pembersihan data, penanganan *missing values*, eliminasi *data leakage* (misal: menghapus kolom tanggal pembayaran riil pada fitur prediksi), serta rekayasa fitur (*Credit Utilization Ratio*).
4. **Modeling:** Menggunakan 3 algoritma klasifikasi:
   * **Logistic Regression** (Baseline model)
   * **Decision Tree Classifier**
   * **Random Forest Classifier**
5. **Evaluation:** Mengukur performa model menggunakan matriks *Accuracy*, *Precision*, *Recall*, dan *ROC-AUC Score*.
6. **Deployment & Prescriptive Analytics:** Memberikan rekomendasi bisnis berbasis data (*Data-Driven Policy*) untuk tim manajemen keuangan dan *sales*.

---

## 📈 4 Level Tingkatan Analytics

| Level Analytics | Pertanyaan Utama | Hasil / Implementasi pada Kasus |
| :--- | :--- | :--- |
| **Descriptive** | *Apa yang terjadi?* | Tren tren omzet naik, namun rasio piutang tak tertagih melonjak 300%. |
| **Diagnostic** | *Mengapa ini terjadi?* | Ditemukan bahwa histori keterlambatan bayar pelanggan dan penggunaan kredit mendekati/melebihi limit menjadi pemicu utama tagihan macet. |
| **Predictive** | *Apa yang akan terjadi?* | Model Machine Learning memprediksi tagihan mana yang berpotensi *Late Payment* dalam 30 hari ke depan. |
| **Prescriptive** | *Apa tindakan terbaik?* | Penerapan *Credit Ceiling* otomatis, pengetatan diskon sales, dan pembuatan *Early Warning System* penagihan. |

---

## 📊 Ringkasan Hasil Model & Evaluasi

| Model Machine Learning | Accuracy | Precision (Late Class) | Recall (Late Class) | ROC-AUC Score |
| :--- | :---: | :---: | :---: | :---: |
| **Logistic Regression** | 98% | 99% | 99% | 0.9974 |
| **Decision Tree** | 96% | 98% | 98% | 0.9403 |
| **Random Forest (Best Model)** 🏆 | **98%** | **98%** | **99%** | **0.9976** |

### **Fitur Paling Berpengaruh (Feature Importance - Random Forest):**
Berdasarkan hasil pemodelan Random Forest, urutan variabel yang paling memicu risiko keterlambatan pembayaran (*Late Payment*) adalah:
1. **`InvoiceAmount`**: Total nilai tagihan invoice (memiliki skor penting tertinggi ~62%).
2. **`PastLatePayments`**: Riwayat frekuensi keterlambatan pelanggan pada transaksi terdahulu.
3. **`CustomerTenure`**: Lama waktu pelanggan berlangganan/bertransaksi dengan perusahaan.
4. **`CreditLimit`**: Batas kredit maksimal yang diberikan kepada pelanggan.
5. **`DiscountGiven`**: Besarnya persentase diskon yang diberikan saat transaksi.

---

## 💡 Rekomendasi Preskriptif untuk Manajemen PT Maju Bersama

1. **Early Warning System (EWS):** Integrasikan model **Random Forest** ke dalam sistem ERP/Billing perusahaan untuk memberikan tanda (*flagging*) otomatis pada invoice berisiko tinggi saat baru diterbitkan.
2. **Pengetatan Credit Limit:** Pelanggan dengan tingkat *Credit Utilization* > 80% dan riwayat *Late Payment* $\ge 2$ kali dibatasi untuk tidak melakukan transaksi kredit baru sebelum tagihan lama dilunasi.
3. **Koreksi Aturan Diskon Sales:** Menghilangkan wewenang diskon mandiri oleh salesmen tanpa *approval* otomatis dari Komite Kredit / Divisi Keuangan.
