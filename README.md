# PCD_UTS_202231042_2024_ITPLN
# LAPORAN <br>
# SOAL 1
-Import library<br>
Disini saya menggunakan yang dibutuhkan untuk mengolah citra ini:
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
ini merupakan cara untuk membuat library yang dibutuhkan, yang dimana masing-masing dari library itu memiliki fungsi yang berbeda beda.

-Membaca Data Gambar<br>
```python
image = cv2.imread("baguskrisnaUTS.jpg")
```
Ini adalah sintax yang dipergunakan untuk membaca atau mendeteksi gambar/citra.

-Membaca ukuran dari gambar
```python
image.shape
```
Ini digunakan untuk menampilkan tuple yang berisi tentang informasi terkait ukuran dari sebuah gambar/citra.

-Mengkonversi gambar ke RGB
```python
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
ini digunakan untuk mengubah format BGR ke dalam format RGB

-Menampilkan hasil konversi ke RGB
```python
plt.imshow(image)
```
Ini digunakan untuk menampilkan gambar 

-Meningkatkan kecerahan dan kontras dari sebuah citra
```python
alpa = 1.2
beta = 10

citragabungan= np.zeros((baris,kolom,3))

for x in range (baris) :
    for y in range (kolom) :
        gcx = (image[x, y] * alpa) + beta
        citragabungan[x, y] = gcx

citragabungan = citragabungan.astype(np.uint8)

fig, axs = plt.subplots(2, 2, figsize = (15,5))
axs[0, 0].imshow(image)
axs[0, 1].hist(image.ravel(), 256, [0, 256])
axs[1, 0].imshow(citragabungan)
axs[1, 1].hist(citragabungan.ravel(), 256, [0,256])
plt.show()
```
Program ini digunakan untuk menambah kecerahan suatu gambar/citra dengan cara mendeteksi setiap piksel pada gambar dan program  ini juga akan menampilkan histogram dari gambar asli dan histogram dari gambar yang sudah dicerahkan. Biasanya digunakan untuk mengecek perbandingan kecerahan antara citra awal dan citra baru

-Mendeteksi Warna
```python
plt.subplot(2, 2, 1)
plt.imshow(citragabungan)
plt.title('Citra Kontras')

# mendeteksi warna merah
plt.subplot(2, 2, 2)
plt.imshow(citragabungan[:,:,0], cmap="gray")
plt.title('RED')

# mendeteksi warna hijau
plt.subplot(2, 2, 3)
plt.imshow(citragabungan[:,:,1], cmap="gray")
plt.title('GREEN')

# mendeteksi warna merah
plt.subplot(2, 2, 4)
plt.imshow(citragabungan[:,:,2], cmap="gray")
plt.title('BLUE')

plt.show()
```
Program ini menggunakan Matplotlib untuk menampilkan beberapa plot citra dalam satu gambar, bersamaan dengan judul yang sesuai untuk setiap plot. Plot tersebut mencakup citra dengan kontras yang telah dimodifikasi, serta tiga plot tambahan untuk masing-masing saluran warna RGB dari citra tersebut. Dengan menggunakan kode ini, kita dapat melihat citra dengan kontras yang telah dimodifikasi serta tiga plot tambahan yang menunjukkan kontribusi masing-masing saluran warna (merah, hijau, dan biru) terhadap citra tersebut. Hal ini memungkinkan kita untuk memahami peran dan distribusi warna dalam citra secara lebih detail.

-Menampilkan Histogram
```python
fig, axs = plt.subplots(3, 2, figsize=(15, 15))

# warna merah
merah = citragabungan[:, :, 0]
histmerah = cv2.calcHist([merah], [0], None, [256], [0,256])
axs[0, 0].imshow(merah, cmap='gray')
axs[0, 0].set_title('RED')
axs[0, 1].plot(histmerah, color='r')
axs[0, 1].set_title('RED-HISTOGRAM')

# warna hijau
hijau = citragabungan[:, :, 1]
histhijau = cv2.calcHist([hijau], [0], None, [256], [0,256])
axs[1, 0].imshow(hijau, cmap='gray')
axs[1, 0].set_title('GREEN')
axs[1, 1].plot(histhijau, color='g')
axs[1, 1].set_title('GREEN-HISTOGRAM')

# warna biru
biru = citragabungan[:, :, 2]
histbiru = cv2.calcHist([biru], [0], None, [256], [0,256])
axs[2, 0].imshow(biru, cmap='gray')
axs[2, 0].set_title('BLUE')
axs[2, 1].plot(histbiru, color='b')
axs[2, 1].set_title('BLUE-HISTOGRAM')

plt.tight_layout()
plt.show()
```
Kode ini menghasilkan grid subplot dengan 3 baris dan 2 kolom, di mana setiap baris berisi gambar dan histogram untuk satu saluran warna (merah, hijau, dan biru) dari citra yang telah dimodifikasi. Histogram menunjukkan distribusi intensitas piksel dalam saluran warna yang sesuai. Dengan menggunakan kode tersebut, kita dapat memvisualisasikan distribusi intensitas piksel dalam saluran warna merah, hijau, dan biru secara terpisah, bersama dengan gambar untuk setiap saluran warna. Hal ini membantu untuk memahami kontribusi masing-masing saluran warna terhadap citra secara lebih jelas.

-Menentukan Ambang Batas Dari Citra
```python
# Konversi citra ke dalam ruang warna HSV
hsv_image = cv2.cvtColor(citragabungan, cv2.COLOR_RGB2HSV)

# Definisikan rentang warna untuk setiap warna
lower_blue = np.array([100, 100, 100])
upper_blue = np.array([140, 255, 255])

# Gunakan ambang batas untuk warna hijau yang telah Anda temukan
lower_green = np.array([20, 100, 100])
upper_green = np.array([250, 255, 255])

lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([180, 255, 255])

# Deteksi warna biru
mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)
# Deteksi warna hijau
mask_green = cv2.inRange(hsv_image, lower_green, upper_green)
# Deteksi warna merah
mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = cv2.bitwise_or(mask_red1, mask_red2)

# Plot hasil

#gambar 1
gray = cv2.cvtColor(citragabungan, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

#gambar 2
plt.subplot(2, 2, 2)
plt.imshow(mask_blue, cmap='gray')
plt.title('Blue')
plt.xticks(np.arange(0, mask_blue.shape[1]+1, 800))
plt.yticks(np.arange(0, mask_blue.shape[0]+1, 500))
plt.axis('on')

#gambar 3
plt.subplot(2, 2, 3)
plt.imshow(np.maximum(mask_red, mask_blue), cmap='gray')
plt.title('Red-blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

#gambar 4
plt.subplot(2, 2, 4)
plt.imshow(mask_green, cmap='gray')
plt.title('Red-Green-Blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

#menampilkan output
plt.tight_layout()
plt.show()
```
Program ini melakukan deteksi warna pada citra yang telah dimodifikasi menggunakan metode segmentasi berdasarkan ruang warna HSV. Selain itu, program juga menampilkan plot dari hasil deteksi warna. Program ini memberikan visualisasi dari hasil deteksi warna pada citra yang telah dimodifikasi, memungkinkan untuk memahami bagaimana proses deteksi warna berfungsi dan menunjukkan hasilnya dalam ruang warna HSV.

-Teori Pendukung
https://www.konsepkoding.com/2023/09/tutorial-python-opencv-deteksi-warna-gambar.html
