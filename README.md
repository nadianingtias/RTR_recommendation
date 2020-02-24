
[feedback-cycle]:https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/feedback_analysis_cycle.png "Feedback Analysis Cycle"

[data-sumber]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/data_sumer.jpg "Data Sumber"

[data-preview]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/data_preview.png "Data Sumber"

[question]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/question.png "Proposed Question"

[feedback3]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/feedback-3.png "Feedback Detail"

[feedback]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/feedback.png "Feedback Result"

[feedback-understand]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/feedback-understand.png "Finding Root Cause"

[design]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/design.png "Designing Solution"

[flask-form]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/flask-1.png "Formulir Preferensi User Awal"

[flask-form2]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/flask-2.png "Formulir Preferensi User Awal - Filled"

[flask-result]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/flask-3.png "Hasil Rekomendasi Berdasarkan Preferensi Input User"
[flask-result2]: https://github.com/nadianingtias/RTR_recommendation/blob/master/Img/flask-3.png "Hasil Rekomendasi Berdasarkan Item"

# **FEEDBACK ANALYSIS & ITEM SIZE CLOTHING RECOMMENDATION**

- **Dataset**: Dataset yang digunakan di dalam repository ini adalah dataset yang berasal dari sebuah website rental pakaian online bernama "Rent The Runway". Rent the Runway adalah layanan online yang menyediakan pakaian desainer dan penyewaan aksesoris. Awalnya merupakan murni perusahaan e-commerce, kemudian membuka lokasi ritel di New York City, Chicago, Washington, DC dan Las Vegas. Rent the Runway saat ini menawarkan lebih dari ribuan pakaian dan aksesoris dari lebih dari ratusan mitra desainer, termasuk Badgley Mischka, Vera Wang, Alexis Bittar, dan Calvin Klein.
<br>
!["https://www.kaggle.com/rmisra/clothing-fit-dataset-for-size-recommendation"][data-sumber]

- **Sumber Data** : [Kaggle Datasets](https://www.kaggle.com/rmisra/clothing-fit-dataset-for-size-recommendation)

- **Purpose** : Melakukan Customer Feedback Analysis, Menemukan Insight Yang Dapat Meningkatkan Layanan Perusahaan Terhadap Customer
- **Machine Learning**: Content Based Recommendation dan Collaborative Filtering

Dalam repository ini, terdapat dokumentasi Notebook dan Folder Flask:
> **Sebelum diproses, data yang akan digunakan telah dimasukkan di dalam database MongoDB** <br>

> **8. Folder (``Flask-app``)**: Merupakan folder aplikasi Flask dengan main server bernama (``app.py``)

> **8. Folder (``Notebook``)**: Berisi file notebook .ipynb yang memuat step by step proses olah dan analisa data.
>> **1. Transform data into numerical**: Dokumentasi preprocessing data menjadi data yang dapat diolah secara numerik <br>
> **2. Sentiment Labelling pada feedback review**: Dokumentasi pelabelan sentiment dari data teks review customer. (review_text, review_summary)<br>
> **3. Analisa Feedback**: Dokumentasi analisa customer feedback secara umum berdasarkan _Fit Feedback_  (``fit``), _Rating Feedback_ (``rating``) dan, sentimen dari _Review Feedback_ (``review_text``, ``review_summary``) .<br>
> **4. Analisa Feedback - Review Negatif**: Dokumentasi eksplorasi feedback review customer. Pengerucutan terhadap sentiment negatif, serta proses inspeksi term yang sering muncul dalam kalimat negatif customer.<br>
> **5. Analisa Feedback - Rating - user priority**: Dokumentasi pengerucutan analisa feedback terhadap user yang paling banyak berdampak <br>
> **6. Popular Items Recommendation**: Dokumentasi rekomendasi item size clothing berdasarkan weighted rating dengan tingkat populer lebih dari sama dengan 0.90 dari persentil frekuensi sewa<br>
> **7. Content Based Recommendation**: Dokumentasi rekomendasi item size clothing berdasarkan data content serta data transaksi untuk content terkait.<br>
> **8. CFF_KNN_SVDPP**: Dokumentasi rekomendasi item size clothing menggunakan collaborative filtering berdasarkan interaksi antar user dalam merating item pakaian.<br>


## Data 

Data yang tersedia dalam sumber, berupa rekam data feedback transaksi pelanggan dari situs sewa pakaian online "Rent The Runway". 
<br>
!["Struktur Data Sebelum Diolah"][data-preview]
<br>
Data di atas berisi 3 macam data yaitu data customer, data produk, dan data feedback dari transaksi.
1. Data Customer
    - ``user_id`` : ID unik dari setiap customer
    - ``bust_size`` : Ukuran bra customer
    - ``weight`` : Berat badan customer
    - ``height`` : Tinggi badan customer
    - ``body type`` : Tipe bentuk badan customer
    - ``age`` : Usia customer
2. Data Produk
    - ``item_id`` : ID unik produk
    - ``size`` : Ukuran produk
    - ``category`` : Kategori produk
3. Data Feedback Transaksi
    - ``review_date`` : Tanggal Memberikan Review
    - ``review_text`` : Teks ulasan customer terhadap transaksi terkait
    - ``review_summary`` : Ringkasan ulasan customer terhadap transaksi terkait
    - ``rating`` : Feedback berupa angka rating untuk produk terkait
    - ``fit`` : Feedback customer terhadap ukuran pakaian berupa "fit", "large", atau "small"
    - ``rented for`` : keperluan customer dalam menyewa

Dari overview data yang tersedia ini, muncul beberapa pertanyaan yang akan dijawab penggalian informasi dari data itu sendiri. Berikut beberapa pertanyaan yang dapat diajukan untuk data feedback ini.
 !["Proposed Question"][question]
 <br>


# Feedback Analysis
__Customer Feedback Analysis__ - sarana memahami sentimen, kebutuhan, dan keinginan customer, untuk membantu perusahaan tetap memberikan produk/layanan yang optimal.
<br>

![alt text][feedback-cycle]<br>
Actionable insight dari hasil analisa feedback customer dapat mengarahkan kita untuk meningkatkan bisnis yang sedang berjalan.

3 sumber untuk mendapatkan actionable insights
1. Survey NPS, atau survey lainnya
2. __Reviews__
3. Social Media

Ada 3 tipe actionable insight yang dapat diperoleh dari analisa feedback customer :
1. Insight > Critical Thinking > Action
2. Insight > Validation > Dont Require Action
3. Insight > Rethink the Strategy

3 teknik dalam NLP yang paling banyak digunakan untuk Customer Feedback Analysis
1. Brand Name Extraction 
2. Sentiment Identification - _Categorize_
3. Keywords Extraction – _Categorize & Finding Root Cause_

2 tahap penting dalam feedback analysis adalah tahap _categorization,_ dan _Finding root cause_. Karena 2 hal ini akan mengarahkan kita untuk memahami, dan merancang action yang solutif bagi perusahaan maupun customer. Salah satu rancangan action yang dibuat dalam projek ini adalah pembuatan _"Recommendation System"_

# RTR Feedback Analysis

![alt text][feedback3]<br>
Berdasar data, feedback customer cukup baik. 97% memberikan review positif, 73% memberikan feedback “fit”, dan 92% memberikan rating 8-10.  
![alt text][feedback]<br>
Berdasarkan data, sebesar 51.7% transaksi mendapat feedback sempurna (angka ini tentu bukan angka yang cukup aman). Kemudian, 0.46% (92 transaksi) mendapat feedback sangat buruk. Sedangkan 47.8% sisanya terdiri dari bermacam-macam feedback.
<br>
![alt text][feedback-understand]<br>
Dari data review negatif customer, kita mendapatkan berbagai term menarik dan insightful. Kita melihat banyak term tentang kesesuaian ukuran pakaian dengan customer seperti
 (size, fit, small, little, short, long dst). 

Serta ada beberapa term yang merujuk kepada pakaian seperti (material, fabric, look, color, dst) yang mungkin pelanggan merasa tidak nyaman dengan item yang disewa. 

Jika perusahaan ingin mengurangi return pakaian dari customer, perlu ditingkatkan/dipikirkan kembali strategi untuk memberikan customer ukuran pakaian yang sesuai.
<br>
![alt text][Design]<br>



# Item-size Clothing Recommendation
Sistem rekomendasi item beserta ukuran, dapat membantu perusahaan untuk meningkatkan pelayanan terhadap customer dalam hal pemilihan item pakaian dan ukuran yang tepat dengan keinginan customer.

Secara umum, rekomendasi terbagi ke dalam 2 jenis, yaitu ``Content Based Filtering dan Collaborative Filtering``. Kedua model ini dicoba untuk membuat sistem rekomendasi di dalam projek ini.

![pod_rec](https://github.com/mnrclab/Final_Project_PodcastRecommendation_UserSegmentation/blob/master/20_prod_recom.png)  

### **1) Content Based Filtering**

Sistem akan merekomendasikan pakaian beserta ukurannya berdasarkan beberapa informasi metadata. Metadata yang digunakan merupakan metadata yang dekat dengan informasi penyewaan sebelumnya. Seperti rerata feedback rating, skor weighted rating, keperluan sewa,rerata tinggi penyewa, rerata berat badan penyewa, rerata usia penyewa, serta nilai fit. 
<br>

Ide dasar sistem ini adalah memanfaatkan data item pakaian yang telah menyimpan track record untuk mendekati kebutuhan dari customer. Sistem akan merekomendasikan item-item yang sangat dekat dengan preferensi yang diperlukan oleh customer.

> **Cosine Similarity Formula**

![cosim](https://github.com/mnrclab/Final_Project_PodcastRecommendation_UserSegmentation/blob/master/21_cosim.png)

### **2) Collaborative Filtering**

Algoritma Collaborative Filtering terdiri atas 2 tipe. Tipe user (_user based_), serta tipe item (_item based_). User-based collaborative filtering menggunakan pola antar user yang mirip (similar) untuk merekomendasikan beberapa produk (jika user A suka produk X, maka user lain yang mirip user A kemungkinan juga suka produk X).

Sedangkan, item-based collaborative filtering lebih fokus kepada item produknya. Contohnya, jika produk X dipilih, biasanya produk Y juga dipilih. Maka jika ada user yang memilih produk X, maka akan direkomendasikan produk Y.


# **Flask Preview**
Berikut ini adalah preview App yang dibuat menggunakan Flask untuk menampilkan:
> * Input Preferensi User Awal<br>
> * Hasil Daftar Rekomendasi Berdasarkan Preferensi
> * Hasil Daftar Rekomendasi Berdasarkan Item Rekomendasi

## **Home**
Tampilan awal (``http://127.0.0.1:5001/``)  menampilkan formulir untuk input preferensi kebutuhan user awal.

<br>
![alt text][Flask-form]<br>
<br>
![alt text][Flask-form2]<br>

## **Hasil Rekomendasi**
Tampilan awal (``http://127.0.0.1:5001/senddata``)  menampilkan hasil daftar rekomendasi yang tersedia. Terdapat tombol __"cari yang mirip ini"__, merupakan tombol ganti preferensi berdasarkan item terkait.
Juga terdapat tombol __"kembali input data"__, untuk kembali kepada input preferensi user.

<br>
![alt text][Flask-result]<br>



> **Note**: Untuk diskusi lebih lanjut apabila ada pertanyaan, kritik, dan saran, berikut kontak email saya : nadia.ningtias20@gmail.com. Terima kasih.
