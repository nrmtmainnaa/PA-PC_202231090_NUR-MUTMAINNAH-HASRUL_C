# PENJELASAN CODINGAN FILTERING CITRA

 # 1. Mengimport Library
import cv2

import numpy as np

import matplotlib.pyplot as plt

fungsi ini untuk memasukkan library yang agar gambar tersebut bisa saya mengolah dan menampilkan

# 2. membaca gambar
image = cv2.imread('fotoinna.jpg')

fungsi ini menunjukkan bahwa gambar bisa diolah dan menyimpannya di variabel image

# 3. Konversi gambar ke grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

fungsi cv2.cvtColor digunakan untuk mengkonversi gambar dari format BGR (Blue, Green, Red) ke format grayscale (abu-abu).

# 5. Fungsi Mean filter

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


# 6. Median Filtering
median_filtered = cv2.medianBlur(image, 5)

fungsi cv2.medianBlur digunakan untuk menerapkan filter median pada gambar image.

# 7. Mean Filtering dengan kernel size 5

mean_filtered = mean_filter(gray_image, 5)

jadi menggunakan filter rata-rata (mean filter) pada gambar skala abu-abu gray_image, dengan ukuran kernel 5x5. Filter rata-rata bekerja dengan menggantikan nilai piksel dengan nilai rata-rata dari piksel-piksel tetangga dalam kernel yang ditentukan. Semakin besar ukuran kernel, semakin luas area tetangga yang dipertimbangkan, yang dapat menghasilkan penghalusan yang lebih signifikan namun dengan potensi hilangnya detail halus dalam gambar. Hasil dari operasi ini disimpan dalam variabel mean_filtered, yang berisi gambar yang telah diolah dengan filter rata-rata.

# 8. Menampilkan hasil dari mean dan median dari filtering citra

plt.figure(figsize=(12, 8))

plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Citra Asli')
plt.axis('on')

plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(median_filtered, cv2.COLOR_BGR2RGB))
plt.title('Setelah Median Filtering')
plt.axis('on')

plt.subplot(2, 2, 3)
plt.imshow(gray_image, cmap='gray')
plt.title('Original image')
plt.axis('on')

plt.subplot(2, 2, 4)
plt.imshow(mean_filtered, cmap='gray')
plt.title('Mean Filtered Image')
plt.axis('on')

plt.tight_layout()
plt.show()

Codingan di atas untuk menampilkan empat gambar secara bersamaan dalam satu jendela visualisasi. Pada baris-baris pertama, gambar asli (`image`) dan gambar hasil filtering dengan filter median (`median_filtered`) ditampilkan dengan konversi warna RGB menggunakan `cv2.cvtColor` untuk memastikan warna ditampilkan dengan benar. Pada baris-baris kedua, gambar asli dalam skala abu-abu (`gray_image`) dan gambar hasil filtering dengan filter rata-rata (`mean_filtered`) ditampilkan dengan colormap 'gray', menunjukkan perbedaan visual antara hasil pengolahan citra menggunakan kedua jenis filter tersebut. Setiap subplot diberi judul yang sesuai untuk menjelaskan jenis gambar yang ditampilkan, seperti citra asli, hasil setelah filter median, citra asli dalam skala abu-abu, dan hasil setelah filter rata-rata. Penyusunan layout menggunakan `plt.tight_layout()` membantu mengatur tata letak subplot secara otomatis untuk memastikan visualisasi yang rapi sebelum ditampilkan dengan `plt.show()`.
