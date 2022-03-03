# BetaThinkTankTeam_JC_DS_VL_03_FinalProject
[contoh](BetaThinkTankTeam_JC_DS_VL_03_FinalProject/Dataset)

by: 
- Ismy Navira Fauziah
- Indradi Khalid Maulana
- Suci Laksono

# Price prediction model to help new furniture companies perform competitor-based analysis
> Untuk lebih lengkap dapat melihat pada file: 

# 1. Business Understanding
### Context/Background: 
Sebuah perusahaan furnitur baru di Saudi Arab ingin menentukan harga produk barunya. Penentuan harga yang tepat menjadi hal yang krusial bagi sebuah perusahaan. Terdapat kasus dimana sebuah perusahaan yang gagal dalam menentukan harga bisa mendapatkan kerugian ribuan hingga jutaan dollar (sumber: https://www.qualtrics.com/au/experience-management/product/how-to-run-pricing-study/?rid=ip&prevsite=en&newsite=au&geo=ID&geomatch=au). Oleh karena itu, perusahaan berusaha membuat prediksi harga sebaik mungkin. 

Untuk menentukan harga furnitur, terdapat beberapa metode yaitu "cost-based method" dan "competitor-based method". Kami sebagai tim data diperusahaan tersebut ingin melakukan "competitor-based" analisis dalam menentukan harga furnitur kami, untuk itu kami menggunakan data dari kompetitor berupa katalog harga barang. Salah satu kompetitor dibidang furnitur yang ingin kami analisis adalah perusahaan IKEA, karena IKEA merupakan salah satu pemain besar di industri furnitur Saudi Arab (sumber:https://www.mordorintelligence.com/industry-reports/saudi-arabia-furniture-market).

Dalam melakukan "competitor-based" analisis metode yang kami gunakan adalah price prediction yang dibantu dengan Machine Learning. Dengan digunakannya metode machine learning dibanding dengan cara manual/konvensional, tentu perusahan mendapat beberapa keuntungan: 

- Dapat mengolah data dari kompetitor yang berjumlah banyak menjadi lebih cepat dan jika diolah dengan benar maka akurasi harga prediksi akan sangat baik. 
- Dengan machine learning, hasil harga yang diperoleh lebih objektif (tergantung fitur yang berpengaruh terhadap harga) tidak subjektif seperti dikerjakan secara manual/konvensional
- Dengan machine learning kami juga bisa memprediksi jenis furnitur yang lebih bervariasi, karena digunakan model regresi untuk menentukan harganya. 
- Dapat menangkap pola harga kompetitor, sehingga jika ada perubahaan database, pola baru tersebut akan terlihat dan dapat diprediksi. 
- Lebih hemat waktu dan biaya, karena akan memangkas waktu saat meng-analisis harga satu per satu, serta memangkas sumber daya manusia karena proses yang dilakukan nantiinya akan semi-otomatis. 
(sumber: https://dlabs.ai/blog/price-prediction-how-machine-learning-can-help-you-grow-your-sales/)

### Problem statement: 
Dalam melakukan analisis harga produk kompetitor secara konvensional dimana seperti melakukan riset pasar, melakukan sorting produk sesuai jenis barang yang ingin dicari, dll akan diperlukan tenaga, waktu dan biaya yang cukup besar. 

Lalu muncul pertanyaan:
Bagaimana cara perusahaan meningkatkan efisiensi dalam memprediksi harga produk berdasarkan kompetitor, sehingga hasil yang diperoleh lebih akurat dan cepat?

### Goals: 
Berdasarkan permasalahan tersebut perusahaan ingin memiliki fitur untuk memprediksi harga furnitur dari data kompetitor, secara (cepat), akurat dan otomatis/semi-otomatis. Perusahaan juga ingin tahu faktor apa yang mempengaruhi sebuah harga dari data kompetitor. 

Oleh karena itu, kami membuat model machine learning yang dapat memprediksi harga sebuah furnitur. Model yang digunakan berupa regresi harga dari data katalog kompetitor. 

# 2.Data Understanding
Data set bersumber dari kaggle (Source: https://www.kaggle.com/ahmedkallam/ikea-sa-furniture-web-scraping). Data tersebut merupakan hasil web scrapping dari IKEA Arab Saudi.

## Attribute Information
| column name | description | 
| -- | -- |
| Unnamed: 0 | - |
| item_id | Product id |
| name | Name of product
| category | Category of product (furniture category) 
| price | Price of product after discount (current price)
| old_price | Price of product before discount
| sellable_online | Whether the product is sold online or not (bool)
| link | Web link
| other_colors | Any other choice of color? (bool)
| short_description | Brief description of product
| designer | Name who design the product
| depth | Depth of product (cm)
| height | Height of product (cm)
| width | Width of product (cm)

# 3. Data Cleaning
Berikut step-step yang kami lakukan pada tahap data cleaning: 
1. Cek data duplikat dan drop data duplikat
2. Cek data null atau missing value
3. isi data null atau missing value
4. Melakukan feature engineering
5. Drop kolom-kolom yang tidak terpakai (Unamed:0, item_id, name, link)

# 4. Exploratory Data Analysis (EDA)
1. Plot distribusi data setiap kolom atau fitur
2. Plot target vs fitur
3. Plot korelasi fitur dengan target

Dari tahap ini didapatkan fitur-fitur mana yang akan digunakan untuk pemodelan

# 5. Modeling 
Pada tahap ini karena model yang kami pakai adalah regresi, sehingga hal pertama yang kami lakukan adalah melakukan evaluasi terhadap data yang kami miliki apakah memenuhi asumsi untuk menggunakan model regresi linear. 
Untuk metodenya kami melakukan analisis residual, dan ternyata hasil menunjukan bahwa data kami tidak memenuhi asumsi, sehingga untuk tahap pemodelan kami tidak menggunakan model regresi linear. 

Berikut spesifikasi tahap pemodelan kami: 
- target = old_price
- features = category, other_colors, num_designer, depth, height, width
- further data preparation =
  - binary encoding for category
  - onehot untuk other_colors
  - scaling dengan robust scaler
- data splitting = 80:20
- Hyperparameter tuning with RandomizedSearchCV
- Model evaluation:
    - RMSE
    - MAE
    - MSE
- Model benchmark:
    - Decision tree regressor
    - Random forest regressor
    - KNN regressor
    - XGboost regressor

Berikut adalah hasil dari pemodelan yang kami lakukan: 
## Model benchmark
Dari metrics evaluasi yang kami pilih, di bawah ini adalah hasil dari evaluasi tersebut: 


