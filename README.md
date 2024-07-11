# PA-PC_202231090_NUR-MUTMAINNAH-HASRUL_C

1. # Mengimport Library
<td>
import cv2
  <tr>
import numpy as np
    <tr>
import matplotlib.pyplot as plt
fungsi ini untuk memasukkan library yang agar gambar tersebut bisa saya mengolah dan menampilkan

 2. # membaca gambar
image = cv2.imread('fotoinna.jpg')
fungsi ini menunjukkan bahwa gambar bisa diolah dan menyimpannya di variabel image

# MEDIAN

3. # Median Filtering
median_filtered = cv2.medianBlur(image, 5)
fungsi cv2.medianBlur digunakan untuk menerapkan filter median pada gambar image.

#Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)), plt.title('citra asli')
plt.subplot(1, 2, 2), plt.imshow(cv2.cvtColor(median_filtered, cv2.COLOR_BGR2RGB)), plt.title('After Median Filtering')
plt.show()
fungsi codingan diatas adalah menerapkan filter median pada gambar untuk mengurangi noise dan kemudian menampilkan gambar asli serta gambar hasil filter median berdampingan untuk perbandingan.

# MEAN

4. # Konversi gambar ke grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
fungsi cv2.cvtColor digunakan untuk mengkonversi gambar dari format BGR (Blue, Green, Red) ke format grayscale (abu-abu).

5. # Fungsi Mean filter
 def mean_filter(image, kernel_size):
    # Mendapatkan dimensi gambar
    h, w = image.shape
    
    # Membuat padding untuk gambar
    pad_size = kernel_size // 2
    padded_image = cv2.copyMakeBorder(image, pad_size, pad_size, pad_size, pad_size, cv2.BORDER_CONSTANT, value=0)
    
    # Membuat hasil gambar kosong
    mean_filtered = np.zeros_like(image)
    
    # Melakukan mean filtering
    for i in range(h):
        for j in range(w):
            # Mengambil nilai dari kernel
            kernel = padded_image[i:i+kernel_size, j:j+kernel_size]
            mean_value = np.mean(kernel)
            mean_filtered[i, j] = mean_value
    
    return mean_filtered

Fungsi mean_filter ini untuk melakukan operasi mean filtering pada gambar grayscale yang diberikan sebagai input. Fungsi ini menerima dua parameter: image, yaitu gambar grayscale, dan kernel_size, yaitu ukuran kernel untuk filter mean. Pertama, fungsi mendapatkan dimensi gambar dan membuat padding pada gambar menggunakan cv2.copyMakeBorder untuk menambahkan batas di sekitar gambar sesuai dengan ukuran kernel. Padding ini diperlukan untuk memastikan filter dapat diterapkan ke seluruh gambar, termasuk tepi gambar. Fungsi kemudian membuat array kosong mean_filtered dengan ukuran yang sama dengan gambar asli untuk menyimpan hasil filtering. Selanjutnya, fungsi melakukan iterasi melalui setiap piksel dalam gambar asli. Untuk setiap piksel, sebuah kernel (sub-array) dari gambar yang dipadding diambil, dan nilai rata-rata dari kernel ini dihitung menggunakan np.mean. Nilai rata-rata ini kemudian ditetapkan ke piksel yang sesuai dalam array mean_filtered. Akhirnya, fungsi mengembalikan gambar yang telah difilter.

7. # Mean Filtering dan Hasil
#Mean Filtering dengan kernel size 5
mean_filtered = mean_filter(gray_image, 5)
#Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(gray_image, cmap='gray'), plt.title('Original Image')
plt.subplot(1, 2, 2), plt.imshow(mean_filtered, cmap='gray'), plt.title('Mean Filtered')
plt.show()

Jadi fungsi ini adalah untuk fungsi mean_filter dipanggil dengan parameter gray_image dan kernel_size 5, yang menghasilkan gambar mean_filtered setelah menerapkan filter mean. Mean filtering adalah teknik yang digunakan untuk mengurangi noise dengan menggantikan setiap piksel dengan rata-rata nilai piksel di sekitarnya dalam area kernel. Setelah mean filtering, hasilnya dibandingkan dengan gambar asli. Dengan menggunakan Matplotlib, gambar asli dan gambar hasil mean filtering ditampilkan berdampingan dalam satu figure dengan ukuran 10x5 inci. Subplot pertama menunjukkan gambar asli dengan colormap grayscale, dan subplot kedua menunjukkan gambar yang telah difilter dengan mean filtering, juga dengan colormap grayscale. Tujuan dari mean filtering ini adalah untuk menghaluskan gambar dan mengurangi noise tanpa kehilangan detail penting.
