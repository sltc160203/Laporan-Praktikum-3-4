
# Praktikum 3 & 4

## DETEKSI GARIS DAN TEPI
import cv2 
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("foto 1.jpg")

cv2.imshow("Gambar asli parkiran",img)
cv2.waitKey(0)
cv2.destroyAllWindows()

## PENJELASAN
- cv2: Library OpenCV untuk pemrosesan gambar.

- numpy: Library untuk operasi numerik.

- matplotlib.pyplot: Library untuk visualisasi data.

## MENAMPILKAN TEPI DAN GAMBAR
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(img, 100, 150)

cv2.imshow("Gambar asli parkirann",edges)
cv2.waitKey(0)
cv2.destroyAllWindows()

## PENJELASAN
- cv2.imread("foto 1.jpg"): Membaca gambar dengan nama file "foto 1.jpg".

- cv2.imshow: Menampilkan gambar asli dengan jendela berjudul "Gambar asli parkiran".

- cv2.waitKey(0): Menunggu penekanan tombol apa saja untuk melanjutkan.

- cv2.destroyAllWindows(): Menutup semua jendela OpenCV yang terbuka.

##  TAMPILAN MENGGUNAKAN FIGURE,AXIX (FUNGSI MATLOTLIB) 
fix, axs = plt.subplots(1, 2, figsize = (10,10))
ax = axs.ravel()
ax[0].imshow(gray, cmap = 'gray')
ax[0].set_title("gambar grayscale")

ax[1].imshow(edges, cmap = 'gray')
ax[1].set_title("gambar grayscale")

## PENJELASAN
- plt.subplots(1, 2, figsize=(10, 10)): Membuat sebuah figure dengan 2 subplot berdampingan, masing-masing berukuran 10x10 inci.

- axs.ravel(): Meratakan array subplot menjadi satu dimensi untuk memudahkan pengaksesan.

- ax[0].imshow(gray, cmap='gray'): Menampilkan gambar grayscale pada subplot pertama dengan skala warna grayscale.

- ax[0].set_title("gambar grayscale"): Memberi judul pada subplot pertama.

- ax[1].imshow(edges, cmap='gray'): Menampilkan gambar hasil deteksi tepi pada subplot kedua dengan skala warna grayscale.

- ax[1].set_title("gambar grayscale"): Memberi judul pada subplot kedua.

## GARIS
## MENAMPILKAN GARIS PADA GAMBAR

lines = cv2.HoughLinesP(edges, 1, np.pi/100, 30, maxLineGap=5)
img_line = img.copy()

for line in lines:
        x1, y1, x2, y2, = line[0]
        cv2.line(img_line, (x1,y1), (x2,y2), (0,0,225),1)

## PENJELASAN
- cv2.HoughLinesP(edges, 1, np.pi/100, 30, maxLineGap=5): Mendeteksi garis dalam gambar hasil deteksi tepi menggunakan transformasi Hough dengan parameter:

- edges: Gambar hasil deteksi tepi.

- 1: Resolusi jarak dalam piksel.

- np.pi/100: Resolusi sudut dalam radian.

- 30: Ambang minimum akumulator untuk garis.

- maxLineGap=5: Jarak maksimum antara segmen garis yang dapat disambungkan untuk membentuk satu garis.

- img.copy(): Membuat salinan gambar asli untuk menggambar garis.

- for line in lines: Loop melalui setiap garis yang terdeteksi.

- x1, y1, x2, y2 = line[0]: Mengambil koordinat titik awal dan akhir garis.

- cv2.line(img_line, (x1, y1), (x2, y2), (0, 0, 225), 1): Menggambar garis merah (BGR: (0, 0, 225)) dengan ketebalan 1 piksel pada salinan gambar.

## TAMPILAN MENGGUNAKAN FIGURE,AXIX (FUNGSI MATLOTLIB) 
gray1 = cv2.cvtColor(img_line, cv2.COLOR_BGR2RGB)
fix, axs = plt.subplots(1, 2, figsize = (10,10))
ax = axs.ravel()
ax[0].imshow(gray, cmap = 'gray')
ax[0].set_title("gambar grayscale")

ax[1].imshow(gray1, cmap = 'gray')
ax[1].set_title("gambar edges")

## PENJELASAN

- cv2.cvtColor(img_line, cv2.COLOR_BGR2RGB): Mengonversi gambar dengan garis deteksi dari format BGR ke RGB untuk kompatibilitas dengan Matplotlib.
- plt.subplots(1, 2, figsize=(10, 10)): Membuat sebuah figure dengan 2 subplot berdampingan, masing-masing berukuran 10x10 inci.
- axs.ravel(): Meratakan array subplot menjadi satu dimensi untuk memudahkan pengaksesan.
- ax[0].imshow(gray, cmap='gray'): Menampilkan gambar grayscale pada subplot pertama dengan skala warna grayscale.
- ax[0].set_title("gambar grayscale"): Memberi judul pada subplot pertama.
- ax[1].imshow(gray1, cmap='gray'): Menampilkan gambar dengan garis deteksi pada subplot kedua dengan skala warna grayscale.
- ax[1].set_title("gambar edges"): Memberi judul pada subplot kedua.

## KESIMPULAN

- Kode ini menunjukkan cara mendeteksi tepi dan garis pada gambar menggunakan OpenCV, dan bagaimana hasilnya dapat divisualisasikan menggunakan Matplotlib. Proses ini mencakup:

- Membaca dan menampilkan gambar asli.
- Mengonversi gambar ke grayscale.
- Mendeteksi tepi menggunakan metode Canny.
- Mendeteksi garis menggunakan Hough Transform.
- Menggambar garis yang terdeteksi pada gambar asli.
- Menampilkan hasil deteksi tepi dan garis secara berdampingan menggunakan Matplotlib.