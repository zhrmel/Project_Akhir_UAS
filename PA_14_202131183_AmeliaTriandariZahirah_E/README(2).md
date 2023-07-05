# Background Remove

Amelia Triandari Zahirah - 202131183

## Teori

Pengolahan citra adalah suatu proses manipulasi dan analisis data citra untuk mendapatkan informasi yang lebih berguna atau untuk menghasilkan citra baru yang memiliki kualitas atau karakteristik yang diinginkan. Pengolahan citra umumnya dilakukan menggunakan perangkat lunak komputer dan teknik pengolahan citra digital.

Proses pengolahan citra dapat melibatkan serangkaian langkah seperti pemrosesan pra-pengolahan, pemrosesan inti, dan pemrosesan pasca-pengolahan. Berikut adalah penjelasan singkat tentang beberapa tahapan penting dalam pengolahan citra:

1. Pemrosesan Pra-pengolahan: Tahap ini melibatkan langkah-langkah untuk mempersiapkan citra sebelum masuk ke proses pengolahan inti. Langkah-langkah ini dapat mencakup peningkatan kualitas citra, pengurangan derau, penajaman, peningkatan kontras, dan normalisasi.

2. Pemrosesan Inti: Pada tahap ini, operasi pengolahan utama dilakukan pada citra. Ini mencakup berbagai teknik seperti filtrasi, segmentasi, ekstraksi fitur, transformasi domain, dan pemodelan statistik. Misalnya, pemfilteran dapat digunakan untuk mengurangi derau, sedangkan segmentasi dapat digunakan untuk memisahkan objek dari latar belakang.

3. Pemrosesan Pasca-pengolahan: Setelah proses inti selesai, tahap ini melibatkan langkah-langkah tambahan seperti penggabungan, penggabungan informasi dari citra yang berbeda, pemulihan atau rekonstruksi citra, peningkatan tampilan, dan kompresi citra. Pada tahap ini, citra yang dihasilkan dari proses inti dapat diubah untuk memperoleh hasil akhir yang diinginkan.

Teknik pengolahan citra dapat digunakan dalam berbagai aplikasi, termasuk pengenalan pola, penglihatan komputer, kedokteran, penginderaan jauh, keamanan, dan grafika komputer. Beberapa contoh penerapan pengolahan citra adalah deteksi wajah, penelusuran objek, restorasi gambar, analisis tekstur, pengenalan tulisan tangan, dan pengenalan karakter.

Dengan perkembangan teknologi dan kemajuan dalam bidang kecerdasan buatan, pengolahan citra semakin kompleks dan canggih. Hal ini memungkinkan penggunaan teknik pengolahan citra yang lebih lanjut, seperti pengolahan citra 3D, pengenalan emosi dari wajah manusia, dan augmented reality.

#### Background Removal

Background removal atau penghapusan latar belakang adalah teknik pengolahan citra yang bertujuan untuk memisahkan objek utama dari latar belakangnya. Dalam banyak kasus, latar belakang dapat mengganggu atau mengaburkan objek yang ingin dianalisis atau dipakai. Dengan menghapus latar belakang, objek utama dapat dipisahkan dan digunakan lebih efektif dalam berbagai aplikasi seperti pengenalan objek, pengenalan wajah, dan komposisi gambar.

Berikut adalah beberapa teknik umum yang digunakan untuk background removal pada pengolahan citra:

1. Thresholding: Metode ini melibatkan mengubah intensitas piksel dalam citra menjadi dua nilai, yaitu 0 (hitam) atau 255 (putih), berdasarkan ambang tertentu. Jika intensitas piksel di atas ambang tertentu, dianggap bagian objek, dan jika di bawah ambang, dianggap bagian latar belakang.

2. Algoritma Segmentasi: Penggunaan algoritma segmentasi, seperti algoritma berbasis wilayah atau berbasis tepi, untuk mengidentifikasi dan memisahkan objek dari latar belakangnya. Algoritma ini mengelompokkan piksel-piksel dengan sifat yang serupa dalam kelompok-kelompok atau wilayah-wilayah yang terpisah.

3. Algoritma Deteksi Tepi: Teknik ini mencari tepi objek dengan mengidentifikasi perbedaan kontras atau kecuraman yang tajam antara objek dan latar belakang. Setelah tepi terdeteksi, objek dapat diisolasi dengan cara memisahkan piksel-piksel tepi dari latar belakangnya.

4. Penggunaan Model Learning: Penggunaan teknik pembelajaran mesin seperti metode klasifikasi (misalnya, SVM atau Random Forest) untuk mengklasifikasikan piksel sebagai bagian dari objek atau latar belakang berdasarkan fitur-fitur yang dipelajari dari data latih.

5. Penggunaan Masking: Metode ini melibatkan pembuatan masker (mask) berdasarkan peta warna atau pembeda lainnya untuk mengisolasi objek dari latar belakang. Masker ini akan memberikan informasi tentang piksel mana yang termasuk dalam objek dan latar belakang.

Background removal memiliki banyak aplikasi praktis, seperti dalam fotografi, pengenalan wajah, periklanan, dan pembuatan grafis. Ketika latar belakang dihilangkan, objek utama dapat dipindahkan ke latar belakang yang berbeda, digabungkan dengan objek lain, atau digunakan untuk menghasilkan gambar atau komposisi visual yang menarik.

## Tahapan Penyelesaian Program 
Program di atas melakukan background removal pada citra 'pensil.png' menggunakan beberapa tahapan pemrosesan. Berikut adalah penjelasan tahapan secara rinci beserta fungsinya:

1. Mengimpor library dan menginisialisasi citra:
   
   import cv2
   import numpy as np
   
   image = cv2.imread('pensil.png')

   Tahap ini melibatkan impor library cv2 (OpenCV) untuk pengolahan citra dan numpy untuk manipulasi array. Selanjutnya, citra "pensil.png" diinisialisasi dengan menggunakan fungsi `cv2.imread()`.

2. Mengubah citra menjadi citra grayscale:

   gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

   Citra diubah menjadi citra grayscale menggunakan fungsi `cv2.cvtColor()`. Hal ini dilakukan untuk mengurangi kompleksitas pemrosesan, karena citra grayscale hanya memiliki satu saluran warna.

3. Thresholding untuk mendapatkan citra biner:
   
   _, thresh = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY_INV | cv2.THRESH_OTSU)

   Thresholding dilakukan untuk menghasilkan citra biner menggunakan fungsi `cv2.threshold()`. Dalam kasus ini, metode thresholding yang digunakan adalah metode Otsu yang secara otomatis menentukan ambang batas untuk memisahkan objek dari latar belakang.

4. Pemrosesan morfologi untuk menghapus derau:
  
   kernel = np.ones((3, 3), np.uint8)
   opening = cv2.morphologyEx(thresh, cv2.MORPH_OPEN, kernel, iterations=2)

   Operasi morfologi "opening" dilakukan menggunakan fungsi `cv2.morphologyEx()` untuk menghilangkan derau pada citra biner. Kernel yang digunakan adalah kernel persegi 3x3, dan dilakukan dua iterasi operasi opening.

5. Membuat masker (mask) menggunakan kontur:
   
   contours, _ = cv2.findContours(opening, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
   mask = np.zeros_like(image)
   cv2.drawContours(mask, contours, -1, (255, 255, 255), thickness=cv2.FILLED)

   Fungsi `cv2.findContours()` digunakan untuk menemukan kontur pada citra hasil operasi morfologi. Kontur-kontur ini kemudian digunakan untuk membuat masker (mask) dengan ukuran yang sama dengan citra asli. Setiap kontur diisi dengan warna putih (255) menggunakan `cv2.drawContours()`.

6. Menggabungkan citra asli dengan masker:
   
   result = cv2.bitwise_and(image, mask)

   Citra asli digabungkan dengan citra mask menggunakan operasi bitwise AND (`cv2.bitwise_and()`) untuk menghapus latar belakang. Hasilnya adalah citra yang hanya menampilkan objek tanpa latar belakang.

7. Menampilkan citra asli dan hasil background removal:
   
   cv2.imshow('Original Image', image)
   cv2.imshow('Background Removed', result)
   cv2.waitKey(0)
   cv2.destroyAllWindows()



