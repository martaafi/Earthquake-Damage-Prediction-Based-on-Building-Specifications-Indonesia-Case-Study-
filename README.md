# Earthquake Damage Prediction Based on Building Specifications: Indonesia Case Study
## Latar Belakang
Sebagai negara yang terletak di sekitar _Ring Of Fire_, tak jarang negara kita, Indonesia, mengalami bencana gempa bumi baik akibat dari pergerakan lempeng tektonik maupun aktivitas gunung berapi. Dengan tingginya angka bencana ini, tentunya tidak sedikit kerugian yang didapat. Guna mengantisipasi terjadinya bencana gempa bumi kedepannya, sebuah perusahaan properti ingin mengetahui pengaruh dari spesifikasi bangunan terhadap kerusakan yang diterima oleh bangunan tersebut. 

## Tujuan
Memprediksi tingkat kerusakan bangunan akibat gempa bumi berdasarkan spesifikasinya.

## Dataset
| No | Variable                     | Description                                             |
| -- | ---------------------------- | ------------------------------------------------------- |
| 1  | **floors_before_eq (total)** | Jumlah total lantai pada bangunan sebelum gempa terjadi |
| 2  | **old_building**             | Usia bangunan (dalam tahun)                             |
| 3  | **plinth_area (ft²)**        | Luas bangunan dalam satuan kaki persegi                 |
| 4  | **height_before_eq (ft)**    | Tinggi bangunan sebelum gempa (dalam kaki)              |
| 5  | **land_surface_condition**         | Kondisi permukaan tanah saat bangunan dibangun                                                                                                                                            |
| 6  | **type_of_foundation**             | Jenis fondasi yang digunakan                                                                                                                                                              |
| 7  | **type_of_roof**                   | Jenis atap bangunan                                                                                                                                                                       |
| 8  | **type_of_ground_floor**           | Jenis lantai pada ground floor                                                                                                                                                            |
| 9 | **type_of_other_floor**            | Jenis lantai selain ground floor                                                                                                                                                          |
| 10 | **position**                       | Posisi bangunan (misalnya berdempetan langsung dengan bangunan lain atau tidak)                                                                                                           |
| 11 | **building_plan_configuration**    | Konfigurasi bangunan terkait bentuk, ukuran, dan penempatan struktur utama                                                                                                                |
| 12 | **technical_solution_proposed** | solusi yang ditawarkan untuk bangunan yang terdampak gempa |
| 13 | **legal_ownership_status** | status kepemilikan bangunan |
| 14 | **has_secondary_use** | keterangan apakah bangunan memiliki kegunaan sekunder |
| 15 | **type_of_reinforcement_concrete** | Tipe beton bertulang: <br>0 = No reinforcement concrete <br>1 = Has non-engineered reinforcement concrete <br>2 = Has engineered reinforcement concrete <br>3 = Has both                                                            |
| 16 | **residential_type** | tipe penggunaaan sebagai hunian |
| 17 | **no_family_residing** | jumlah keluarga yang tinggal dalam bangunan tersebut |
| 18 | **public_place_type**           | Tipe penggunaan sebagai tempat umum                   |
| 19 | **industrial_use_type**         | Tipe industri                      |
| 20 | **govermental_use_type**        | Tipe penggunaan sebagai bangunan pemerintahan         |
| 21 | **flexible_superstructure**        | Indikator penggunaan superstructure fleksibel   |
| 22 | **wall_binding**                   | Material perekat dinding: <br>0 = Unknown/not stated <br>1 = Clay <br>2 = Mortar + Cement <br>3 = Mortar + Cement + Clay <br>5 = Mud + Mortar, Clay <br>7 = Mud + Mortar, Clay, Cement + Mortar |
| 23 | **wall_material**                  | Material dasar dinding: <br>0 = Unknown/not stated <br>1 = Red Bricks <br>2 = Stone Bricks <br>3 = Red Bricks, Stone Bricks                                                              |
| 24 | **damage_grade (variabel target)** | tingkat kerusakan yang disebabkan oleh gempa (1-5) |

## Exploratory Data Analysis
**Barchart dan Pie Chart Label Damage Grade**

<img width="395" height="295" alt="image" src="https://github.com/user-attachments/assets/7b559e9c-889b-47b0-b751-fe9ff00c5c67" /> <img width="395" height="295" alt="image" src="https://github.com/user-attachments/assets/c7b63825-960b-483a-ad7d-03084e4ca3dd" />

Berdasarkan grafik batang dan diagram lingkaran, terlihat bahwa tingkat kerusakan parah mendominasi. Kerusakan tingkat 5, yang paling berat, mencakup 35,4% dari total kasus dengan 109.660 insiden, diikuti oleh tingkat 4 dengan 24% atau 74.345 kasus. Kerusakan tingkat menengah (tingkat 3) mewakili 18,2% dengan 56.205 kasus. Sementara itu, kerusakan ringan (tingkat 1 dan 2) hanya mencakup sebagian kecil, masing-masing 11,8% (33.773 kasus) dan 10,7% (36.446 kasus). Secara keseluruhan, lebih dari 59% struktur mengalami kerusakan berat (tingkat 4-5), sementara kerusakan ringan hingga sedang (tingkat 1-3) mencakup sekitar 41% kasus. Distribusi ini mengindikasikan bahwa gempa tersebut menyebabkan dampak yang sangat serius, dengan mayoritas bangunan mengalami kerusakan parah.

**Boxplot dan Histogram Variabel Numerik Data Train**
<img width="2990" height="1214" alt="image" src="https://github.com/user-attachments/assets/a85d3d11-192d-4f59-9f27-a7d93b8828f4" /> 

<img width="2989" height="1223" alt="image" src="https://github.com/user-attachments/assets/fb0c1693-23a2-4fc9-b975-a1867d4accfc" />

- ’Floors_before_eq’ (Jumlah lantai bangunan sebelum gempa): Mayoritas bangunan memiliki 2-3 lantai, dengan puncak tertinggi pada 2 lantai. Bangunan 1 dan 4 lantai juga cukup umum. Boxplot menunjukkan adanya outlier hingga 9 lantai, namun histogram mengonfirmasi bahwa bangunan di atas 4 lantai sangat jarang.
- ’Old_building’ (Usia bangunan): Distribusi usia bangunan sangat miring ke kanan. Sebagian besar bangunan berusia relatif muda, namun boxplot menunjukkan adanya outlier yang mengindikasikan beberapa bangunan sangat tua. Histogram memperjelas bahwa mayoritas bangunan berusia di bawah 100 tahun, dengan penurunan tajam untuk usia yang lebih tua.
- ’Plinth_area’ (Luas alas bangunan): Distribusi luas alas bangunan cenderung normal namun sedikit miring ke kanan. Boxplot dan histogram sama-sama menunjukkan variasi yang cukup lebar, dengan mayoritas bangunan memiliki luas antara 200-600 m2. Terdapat outlier yang mencolok, mengindikasikan beberapa bangunan dengan luas yang sangat besar.
- ’Height_before_eq’ (Tinggi bangunan sebelum gempa): Selaras dengan jumlah lantai, mayoritas bangunan memiliki tinggi yang relatif seragam antara 10-30 kaki. Boxplot menampilkan outlier yang signifikan, sementara histogram memperlihatkan penurunan tajam frekuensi untuk bangunan yang lebih tinggi.
- ’No_family_residing’ (Jumlah keluarga yang tinggal): Boxplot dan histogram konsisten menunjukkan bahwa hampir semua bangunan dihuni oleh 1 keluarga. Boxplot memperlihatkan outlier, yang dikonfirmasi oleh histogram bahwa ada sedikit sekali bangunan yang dihuni oleh 2 atau lebih keluarga.

## Evaluai Metrik
Evaluasi metrik yang digunakan untuk menilai akurasi model adalah F1-Score Macro Avg:

<img width="438" height="100" alt="image" src="https://github.com/user-attachments/assets/6af9dd69-d351-4f2e-b0a9-e06050a048a0" />

## Hasil Pemodelan
| No | Model | F1-Score |
| -- | ----- | -------- |
| 1 | Cat Boost | 0,4040 |
| 2 | Hist Gradient Boosting | 0,3947 |
| 3 | Random Forest | 0,3870 |
| 4 | Gradient Boosting | 0,2967 |
| 5 | Extra Trees Classifier | 0,3724 | 
| 6 | MLP Classifier | 0,3965 |
| 7 | AdaBoost Classifier | 0,3785 |

Dari beberapa pemodelan yang telah dilakukan, diperoleh bahwa model Cat Boost memiliki nilai F1 Score macro avg yang paling tinggi dibandingkan model yang lain. Oleh karena itu dilakukan prediksi data test menggunakan model Cat Boost
