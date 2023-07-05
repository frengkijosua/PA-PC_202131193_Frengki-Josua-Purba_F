
# Word Segmentatin

1. Teori
Word segmentation adalah proses memisahkan teks menjadi unit-unit kata atau token. Dalam konteks pengolahan citra, word segmentation merupakan langkah awal untuk mendapatkan teks yang ada dalam gambar. Dalam teori ini, saya akan menjelaskan pendekatan untuk melakukan word segmentation dalam pengolahan citra menggunakan Python.

Langkah-langkah untuk melakukan word segmentation dalam pengolahan citra menggunakan Python:

- Preprocessing Citra:
Mengimpor citra menggunakan pustaka Python seperti OpenCV atau PIL.
Konversi citra ke skala keabuan (grayscale) jika perlu.
Mengaplikasikan teknik preprocessing seperti pemotongan (cropping), filtering, atau peningkatan kontras untuk meningkatkan kualitas citra.

- Segmentasi Teks Menggunakan Deteksi Tepi:
Menggunakan algoritma deteksi tepi seperti Canny atau Sobel untuk menemukan tepi yang ada pada citra.
Menerapkan teknik pemrosesan citra seperti dilasi (dilation) atau erosi (erosion) untuk memperbaiki hasil deteksi tepi.

- Segmentasi Teks Menggunakan Pemisahan Komponen Terhubung:
Menggunakan algoritma pemisahan komponen terhubung seperti komponen terhubung berdasarkan label (connected component labeling) untuk mengidentifikasi wilayah teks yang saling terhubung.
Menghapus komponen yang kecil atau tidak relevan berdasarkan ukuran atau properti tertentu.

- Pemisahan Kata:
Menggunakan metode pemisahan kata berdasarkan jarak antar teks untuk memisahkan kata-kata dalam wilayah teks yang saling terhubung.
Dapat menggunakan pendekatan berbasis jarak seperti analisis spasial atau menggunakan pendekatan berbasis pemrosesan teks seperti pemisahan kata menggunakan model NLP (Natural Language Processing) seperti pemisahan kata berbasis LSTM (Long Short-Term Memory).

- Pengenalan Karakter:
Setelah mendapatkan kata-kata yang terpisah, langkah selanjutnya adalah melakukan pengenalan karakter pada setiap kata.
Menggunakan metode pengenalan karakter berbasis pembelajaran mesin (machine learning) seperti penggunaan model Convolutional Neural Network (CNN) atau Optical Character Recognition (OCR) untuk mengenali karakter pada setiap kata.

- Pembersihan dan Pengolahan Lebih Lanjut:
Melakukan pembersihan pada hasil pengenalan karakter seperti menghilangkan karakter-karakter yang tidak relevan atau menggunakan teknik pengenalan karakter yang lebih canggih untuk meningkatkan akurasi.
Melakukan pengolahan lebih lanjut pada kata-kata yang tersegmentasi seperti pengenalan bahasa atau penerapan teknik pemrosesan teks lainnya.
Pada dasarnya, teori ini memberikan panduan umum tentang langkah-langkah yang dapat diambil untuk melakukan word segmentation dalam pengolahan citra menggunakan Python. Namun, setiap langkah tersebut dapat disesuaikan atau dikombinasikan dengan teknik-teknik lainnya tergantung pada kebutuhan dan karakteristik dari citra yang akan diproses.



2. Penjelasan Mengenai Project Saya (Word Segmentatin)

import cv2

import numpy as np

import matplotlib.pyplot as plt

- Import library:
~ Mengimpor pustaka OpenCV dengan menggunakan pernyataan import cv2. OpenCV (Open Source Computer Vision Library) adalah pustaka populer yang digunakan untuk pengolahan citra dan komputer.
~ Mengimpor pustaka NumPy dengan menggunakan pernyataan import numpy as np. NumPy adalah pustaka Python yang digunakan untuk melakukan operasi numerik dan manipulasi array.
~ Mengimpor pustaka matplotlib.pyplot dengan menggunakan pernyataan import matplotlib.pyplot as plt. Matplotlib adalah pustaka visualisasi data yang digunakan untuk membuat plot dan grafik.

- Persiapan Pengolahan Citra:
Anda perlu mempersiapkan citra yang akan diproses. Misalnya, Anda dapat menggunakan pernyataan img = cv2.imread('nama_citra.jpg') untuk membaca citra dari file gambar dengan nama 'nama_citra.jpg'. Anda juga dapat menentukan jalur lengkap file jika citra tidak berada di direktori yang sama dengan file Python Anda.

- Operasi Pengolahan Citra:
~ Setelah membaca citra, Anda dapat melakukan berbagai operasi pengolahan citra menggunakan fungsi-fungsi OpenCV. Misalnya, Anda dapat menggunakan fungsi cv2.cvtColor() untuk mengubah skala warna citra menjadi skala keabuan (grayscale) jika diperlukan.
~ Anda juga dapat menerapkan teknik-teknik pemrosesan citra seperti pemotongan (cropping) menggunakan fungsi cv2.crop(), peningkatan kontras menggunakan fungsi cv2.equalizeHist(), atau filter citra menggunakan fungsi cv2.filter2D().

- Visualisasi Hasil:
~ Setelah melakukan operasi pengolahan citra, Anda dapat memvisualisasikan hasilnya menggunakan matplotlib. Misalnya, Anda dapat menggunakan pernyataan plt.imshow(img) untuk menampilkan citra yang telah diproses di jendela plot.
~ Anda juga dapat menambahkan judul atau label sumbu pada plot menggunakan pernyataan-pernyataan seperti plt.title() atau plt.xlabel().
~ Terakhir, Anda dapat menggunakan pernyataan plt.show() untuk menampilkan plot citra yang telah diproses secara keseluruhan.

img = cv2.imread('20230705_114219.jpg')

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

h, w, c = img.shape

if w > 1000:
    
    new_w = 1000
    ar = w/h
    new_h = int(new_w/ar)
    
    img = cv2.resize(img, (new_w, new_h), interpolation = cv2.INTER_AREA)
plt.imshow(img);

Tahapan rinci pada source code Python di atas adalah sebagai berikut:

- Membaca Citra:
Menggunakan pernyataan cv2.imread('20230705_114219.jpg') untuk membaca citra dari file gambar dengan nama '20230705_114219.jpg'. Citra tersebut akan disimpan dalam variabel img.

- Konversi Warna:
Menggunakan pernyataan cv2.cvtColor(img, cv2.COLOR_BGR2RGB) untuk mengubah skala warna citra dari BGR (Blue-Green-Red) menjadi RGB (Red-Green-Blue). Hal ini dilakukan karena citra yang dibaca oleh OpenCV menggunakan skala warna BGR, sementara matplotlib.pyplot menggunakan skala warna RGB.

- Mendapatkan Dimensi Citra:
Menggunakan pernyataan h, w, c = img.shape untuk mendapatkan tinggi (h), lebar (w), dan jumlah saluran warna (c) dari citra. Variabel h akan menyimpan tinggi citra, w akan menyimpan lebar citra, dan c akan menyimpan jumlah saluran warna (biasanya 3 untuk citra berwarna RGB).

- Pengukuran Lebar Citra:
~ Memeriksa apakah lebar citra (w) lebih besar dari 1000 piksel dengan menggunakan kondisi if w > 1000:.
~ Jika lebar citra lebih besar dari 1000, maka akan dilakukan penyesuaian ukuran citra.

- Penyesuaian Ukuran Citra:
~ Menentukan lebar baru (new_w) yang diinginkan, dalam contoh ini 1000 piksel.
~ Menghitung rasio aspek (ar) dengan membagi lebar (w) oleh tinggi (h) citra asli.
~ Menghitung tinggi baru (new_h) dengan membagi lebar baru (new_w) oleh rasio aspek (ar), dan mengonversi hasilnya ke dalam bilangan bulat menggunakan fungsi int().
~ Menggunakan pernyataan cv2.resize() untuk mengubah ukuran citra menjadi lebar baru (new_w) dan tinggi baru (new_h) menggunakan metode interpolasi cv2.INTER_AREA yang memberikan hasil berkualitas baik untuk penurunan ukuran citra.

- Menampilkan Citra:
~ Menggunakan pernyataan plt.imshow(img) untuk menampilkan citra yang telah diubah ukurannya di jendela plot.
~ Terakhir, menggunakan pernyataan plt.show() untuk menampilkan plot citra yang telah diproses secara keseluruhan.

def thresholding(image):

    img_gray = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
    ret,thresh = cv2.threshold(img_gray,80,255,cv2.THRESH_BINARY_INV)
    plt.imshow(thresh, cmap='gray')
    return thresh

thresh_img = thresholding(img);

- Fungsi Thresholding:
~ Didefinisikan sebuah fungsi bernama thresholding yang menerima satu argumen, yaitu citra image.
~ Di dalam fungsi, citra input image dikonversi ke skala keabuan (grayscale) menggunakan pernyataan cv2.cvtColor(image,cv2.COLOR_BGR2GRAY). Citra hasilnya disimpan dalam variabel img_gray.
~ Menggunakan pernyataan cv2.threshold() untuk melakukan thresholding pada citra grayscale img_gray. Thresholding dilakukan dengan parameter sebagai berikut:
img_gray: citra input grayscale yang akan di-threshold.
80: nilai threshold yang digunakan, piksel dengan nilai di bawah threshold akan diubah menjadi 0 (hitam), sedangkan piksel dengan nilai di atas threshold akan diubah menjadi 255 (putih).
255: nilai maksimal yang diberikan untuk piksel yang melebihi threshold.
cv2.THRESH_BINARY_INV: jenis thresholding yang digunakan, dalam hal ini thresholding biner terbalik (invert).
Hasil thresholding disimpan dalam variabel thresh.

- Menampilkan Citra Hasil Thresholding:
Menggunakan pernyataan plt.imshow(thresh, cmap='gray') untuk menampilkan citra hasil thresholding thresh dalam plot. Pada pernyataan ini, parameter cmap='gray' digunakan untuk mengatur colormap plot menjadi skala abu-abu.

- Mengembalikan Citra Hasil Thresholding:
Menggunakan pernyataan return thresh untuk mengembalikan citra hasil thresholding thresh dari fungsi thresholding().

- Memanggil Fungsi dan Menyimpan Hasil:
~ Menggunakan pernyataan thresh_img = thresholding(img) untuk memanggil fungsi thresholding() dengan citra img sebagai argumen.
~ Citra hasil thresholding disimpan dalam variabel thresh_img.


kernel = np.ones((3,85), np.uint8)

dilated = cv2.dilate(thresh_img, kernel, iterations = 1)

plt.imshow(dilated, cmap='gray');

- Membuat Kernel:
Didefinisikan kernel menggunakan fungsi np.ones() dengan ukuran (3, 85) dan tipe data np.uint8. Kernel yang dibuat berukuran 3x85, di mana semua elemennya memiliki nilai 1. Kernel ini akan digunakan dalam operasi dilasi pada langkah selanjutnya.

- Dilasi Citra:
~ Menggunakan pernyataan cv2.dilate(thresh_img, kernel, iterations = 1) untuk melakukan operasi dilasi pada citra hasil thresholding thresh_img dengan menggunakan kernel yang telah dibuat. Hasil dilasi disimpan dalam variabel dilated.
~ Pada operasi dilasi, setiap piksel pada citra akan diperluas dengan menggunakan kernel yang diberikan. Piksel-piksel yang berdekatan dan berhubungan akan saling terhubung dan membentuk wilayah yang lebih besar.

- Menampilkan Citra Hasil Dilasi:
~ Menggunakan pernyataan plt.imshow(dilated, cmap='gray') untuk menampilkan citra hasil dilasi dilated dalam plot dengan colormap skala abu-abu.
~ Pernyataan ini akan menampilkan citra yang telah mengalami proses dilasi, di mana wilayah-wilayah teks yang telah saling terhubung menjadi lebih tebal dan terhubung secara visual.

img2 = img.copy()

for ctr in sorted_contours_lines:
    
    x,y,w,h = cv2.boundingRect(ctr)
    cv2.rectangle(img2, (x,y), (x+w, y+h), (40, 100, 250), 2)
    
plt.imshow(img2);


- Membuat Salinan Citra:
Membuat salinan citra awal dengan menggunakan pernyataan img2 = img.copy(). Salinan ini akan digunakan untuk menggambar persegi panjang di sekitar kontur-kontur.

- Loop Kontur:
Membuat loop for untuk mengiterasi melalui kontur-kontur yang disimpan dalam variabel sorted_contours_lines.
Di dalam loop, variabel ctr akan mewakili kontur saat ini yang sedang diproses.

- Membuat Persegi Panjang:
~ Menggunakan pernyataan cv2.boundingRect(ctr) untuk mendapatkan koordinat kotak pembatas (bounding box) dari kontur saat ini. Hasilnya adalah koordinat x, y (titik pojok kiri atas) dan lebar (w) serta tinggi (h) kotak pembatas.
~ Menggunakan pernyataan cv2.rectangle() untuk menggambar persegi panjang pada citra img2. Parameter yang digunakan adalah:
(x, y): titik pojok kiri atas persegi panjang.
(x+w, y+h): titik pojok kanan bawah persegi panjang.
(40, 100, 250): warna persegi panjang dalam format BGR (Blue-Green-Red). Dalam hal ini, warna yang digunakan adalah biru (40), hijau (100), dan merah (250).
2: ketebalan garis persegi panjang.

- Menampilkan Citra Hasil:
~ Menggunakan pernyataan plt.imshow(img2) untuk menampilkan citra hasil dengan persegi panjang yang telah digambar di sekitar kontur-kontur.
~ Pernyataan ini akan menampilkan citra dengan persegi panjang yang menunjukkan letak kontur-kontur yang terdeteksi.

img3 = img.copy()
words_list = []

for line in sorted_contours_lines:
    
    # roi of each line
    x, y, w, h = cv2.boundingRect(line)
    roi_line = dilated2[y:y+w, x:x+w]
    
    # draw contours on each word
    (cnt, heirarchy) = cv2.findContours(roi_line.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)
    sorted_contour_words = sorted(cnt, key=lambda cntr : cv2.boundingRect(cntr)[0])
    
    for word in sorted_contour_words:
        
        if cv2.contourArea(word) < 400:
            continue
        
        x2, y2, w2, h2 = cv2.boundingRect(word)
        words_list.append([x+x2, y+y2, x+x2+w2, y+y2+h2])
        cv2.rectangle(img3, (x+x2, y+y2), (x+x2+w2, y+y2+h2), (255,255,100),2)
        
plt.imshow(img3);


- Membuat Salinan Citra:
Membuat salinan citra awal dengan menggunakan pernyataan img3 = img.copy(). Salinan ini akan digunakan untuk menggambar persegi panjang di sekitar kata-kata.

- Loop Kontur Garis:
~ Membuat loop for untuk mengiterasi melalui kontur-kontur garis yang disimpan dalam variabel sorted_contours_lines.
~ Di dalam loop, variabel line akan mewakili kontur garis saat ini yang sedang diproses.

- ROI (Region of Interest) Setiap Baris:
~ Menggunakan pernyataan cv2.boundingRect(line) untuk mendapatkan koordinat ROI (Region of Interest) dari setiap baris kontur garis. Hasilnya adalah koordinat x, y (titik pojok kiri atas) dan lebar (w) serta tinggi (h) ROI.
~ Menggunakan pernyataan roi_line = dilated2[y:y+w, x:x+w] untuk mendapatkan ROI dari citra hasil dilasi dilated2 berdasarkan koordinat ROI baris yang telah diperoleh.

- Loop Kontur Kata di Setiap Baris:
~ Menggunakan loop for untuk mengiterasi melalui kontur-kontur kata yang terdapat dalam ROI baris.
~ Di dalam loop, variabel word akan mewakili kontur kata saat ini yang sedang diproses.

- Penyeleksian dan Penambahan Kata ke Daftar:
~ Menggunakan pernyataan if cv2.contourArea(word) < 400: continue untuk mengecualikan kata-kata yang memiliki luas (area) di bawah 400 piksel.
~ Menggunakan pernyataan x2, y2, w2, h2 = cv2.boundingRect(word) untuk mendapatkan koordinat kata yang sedang diproses.
~ Menambahkan koordinat kata (dalam bentuk [x_min, y_min, x_max, y_max]) ke dalam daftar words_list.

- Menggambar Persegi Panjang pada Setiap Kata:
~ Menggunakan pernyataan cv2.rectangle(img3, (x+x2, y+y2), (x+x2+w2, y+y2+h2), (255,255,100),2) untuk menggambar persegi panjang pada citra img3 dengan menggunakan koordinat kata yang sedang diproses.
~ Parameter yang digunakan dalam cv2.rectangle() adalah:
(x+x2, y+y2): titik pojok kiri atas persegi panjang.
(x+x2+w2, y+y2+h2): titik pojok kanan bawah persegi panjang.
(255, 255, 100): warna persegi panjang dalam format BGR (Blue-Green-Red). Dalam hal ini, warna yang digunakan adalah kuning (255, 255, 100).
2: ketebalan garis persegi panjang.

- Menampilkan Citra Hasil dengan Persegi Panjang pada Kata:
~ Menggunakan pernyataan plt.imshow(img3) untuk menampilkan citra hasil dengan persegi panjang yang telah digambar di sekitar kata-kata.
~ Pernyataan ini akan menampilkan citra dengan persegi panjang yang menunjukkan letak kata-kata yang terdeteksi.



3. Jurnal Terkait

https://journals.iium.edu.my/ejournal/index.php/iiumej/article/view/1408

Thank u:)