# Tugas-Face-Recognition-PML-STEI-ITB-Kelompok-2I. Pendahuluan
Deepface adalah suatu framework untuk pengenalan wajah (face recognition) yang membungkus state-of-the-art model-model pengenalan wajah yang telah dikembangkan sebelumnya seperti VGG-face, Google FaceNet, OpenFace, Facebook Deepface, DeepID, ArcFace dan Dlib. Pada tugas ini anda akan mengeksplorasi Deepface Library sehingga mendapatkan prosedur dan konfigurasi terbaik untuk task pengenalan wajah.

I.1. Menginstal library Deepface
Untuk menggunakan Deepface terlebih dahulu menginstall library Deepface sebagai berikut:
	!pip install deepface
from deepface import DeepFace


I.2. Menyiapkan sample dataset
Menyiapkan foto-foto yang akan digunakan sebagai database referensi dan data pengujian. Data pengujian terdiri dari data tes anggota kelas dan bukan anggota kelas. Sample dataset dapat disimpan di GDrive, cara mengaksesnya sebagai berikut:
	from google.colab import drive
drive.mount('/content/drive')


Berikut sample gambar yang digunakan:
Tabel 1 Database
No	database	test_data_anggota	test_data_non_anggota
1	 	 	 
2	 	 	

3	 	 	 
4	 	 	 
5	 	 	 


	import glob
import os

img_anggota_path = 'drive/MyDrive/dataset/test_data_anggota/'
img_non_anggota_path = 'drive/MyDrive/dataset/test_data_non_anggota/'
img_database_path = 'drive/MyDrive/dataset/database/'
ext = ['jpeg', 'jpg', 'jfif', 'png']

files_test_anggota = []
files_test_non_anggota = []
files_database = []
[files_test_anggota.extend(glob.glob(img_anggota_path + '*.' + e)) for e in ext]
[files_test_non_anggota.extend(glob.glob(img_non_anggota_path + '*.' + e)) for e in ext]
[files_database.extend(glob.glob(img_database_path + '*.' + e)) for e in ext]

print('------------- gambar tes anggota -----------------')
counter = 0;
for img_test in files_test_anggota:
  counter = counter + 1;
  print(str(counter) + '  ' + img_test)

print('------------- gambar tes non anggota -----------------')
counter = 0;
for img_test in files_test_non_anggota:
  counter = counter + 1;
  print(str(counter) + '  ' + img_test)

print('------------- gambar database -----------------')
counter = 0;
for img_db in files_database:
  counter = counter + 1;
  print(str(counter) + '  ' + img_db)

	------------- gambar tes anggota -----------------
1  drive/MyDrive/dataset/test_data_anggota/Adiyasa nurfalah-2.jpeg
2  drive/MyDrive/dataset/test_data_anggota/Adiyasa nurfalah-3.jpeg
3  drive/MyDrive/dataset/test_data_anggota/Rahman Indra Kesuma.jpeg
4  drive/MyDrive/dataset/test_data_anggota/Riyanto riyanto3.jpeg
5  drive/MyDrive/dataset/test_data_anggota/Lathifah arief.jpeg
6  drive/MyDrive/dataset/test_data_anggota/Riyanto riyanto.jpeg
7  drive/MyDrive/dataset/test_data_anggota/Rahman Indra Kesuma(3).jpeg
8  drive/MyDrive/dataset/test_data_anggota/Arief sartono 14.jpg
9  drive/MyDrive/dataset/test_data_anggota/Arief sartono 13.jpg
10  drive/MyDrive/dataset/test_data_anggota/Arief sartono 10.jpg
11  drive/MyDrive/dataset/test_data_anggota/Arief sartono 16.jpg
12  drive/MyDrive/dataset/test_data_anggota/Arief sartono 11.jpg
13  drive/MyDrive/dataset/test_data_anggota/Arief sartono 15.jpg
14  drive/MyDrive/dataset/test_data_anggota/Adiyasa nurfalah-2.jpg
15  drive/MyDrive/dataset/test_data_anggota/Arief sartono 12.jpg
16  drive/MyDrive/dataset/test_data_anggota/Adiyasa nurfalah-3.jpg
17  drive/MyDrive/dataset/test_data_anggota/Ahmad Luky Ramdani(1).jpg
18  drive/MyDrive/dataset/test_data_anggota/Arief sartono 5.jpg
19  drive/MyDrive/dataset/test_data_anggota/Arief sartono 2.jpg
20  drive/MyDrive/dataset/test_data_anggota/Handoko supeno (2).jpg
21  drive/MyDrive/dataset/test_data_anggota/Baud Prananto7.jpg
22  drive/MyDrive/dataset/test_data_anggota/Arief sartono 7.jpg
23  drive/MyDrive/dataset/test_data_anggota/Baud Prananto3.jpg
24  drive/MyDrive/dataset/test_data_anggota/Yaya Setiyadi_3.jpg
25  drive/MyDrive/dataset/test_data_anggota/Mina Ismu Rahayu (3).jpg
26  drive/MyDrive/dataset/test_data_anggota/Imam Ekowicaksono.jpg
27  drive/MyDrive/dataset/test_data_anggota/Arief sartono 17.jpg
28  drive/MyDrive/dataset/test_data_anggota/Arief sartono 6.jpg
29  drive/MyDrive/dataset/test_data_anggota/Baud Prananto5.jpg
30  drive/MyDrive/dataset/test_data_anggota/Muhammad Khaerul Naim 1.jpg
31  drive/MyDrive/dataset/test_data_anggota/Arief sartono 9.jpg
32  drive/MyDrive/dataset/test_data_anggota/Yaya Setiyadi_2.jpg
33  drive/MyDrive/dataset/test_data_anggota/Kemas Muhammad Irsan Riza (2).jpg
34  drive/MyDrive/dataset/test_data_anggota/Reza Budiawan 2.jpg
35  drive/MyDrive/dataset/test_data_anggota/Meza silvana.jpg
36  drive/MyDrive/dataset/test_data_anggota/Arief sartono 8.jpg
37  drive/MyDrive/dataset/test_data_anggota/Lathifah Arief.jpg
38  drive/MyDrive/dataset/test_data_anggota/Arief sartono 3.jpg
39  drive/MyDrive/dataset/test_data_anggota/Meredita susanty(1).jpg
40  drive/MyDrive/dataset/test_data_anggota/Baud Prananto4.jpg
41  drive/MyDrive/dataset/test_data_anggota/Baud Prananto.jpg
42  drive/MyDrive/dataset/test_data_anggota/Mina Ismu Rahayu (2).jpg
43  drive/MyDrive/dataset/test_data_anggota/Arief sartono 4.jpg
44  drive/MyDrive/dataset/test_data_anggota/Imam ekowicaksono_1_.jpg
45  drive/MyDrive/dataset/test_data_anggota/Handoko supeno.jpg
46  drive/MyDrive/dataset/test_data_anggota/Muhammad Khaerul Naim 2.jpg
47  drive/MyDrive/dataset/test_data_anggota/Ahmad Luky Ramdani(2).jfif
48  drive/MyDrive/dataset/test_data_anggota/Rahman Indra Kesuma(2).jfif
49  drive/MyDrive/dataset/test_data_anggota/Meza silvana.jfif
50  drive/MyDrive/dataset/test_data_anggota/Rahman Indra Kesuma(1).jfif
51  drive/MyDrive/dataset/test_data_anggota/Baud prananto.jfif
52  drive/MyDrive/dataset/test_data_anggota/Varuliantor Dear 2.png
------------- gambar tes non anggota -----------------
1  drive/MyDrive/dataset/test_data_non_anggota/Rio Dewanto 002.jpeg
2  drive/MyDrive/dataset/test_data_non_anggota/silas.jpeg
3  drive/MyDrive/dataset/test_data_non_anggota/Arkhana 001.jpeg
4  drive/MyDrive/dataset/test_data_non_anggota/gozali.jpeg
5  drive/MyDrive/dataset/test_data_non_anggota/Johnny Depp 002.jpeg
6  drive/MyDrive/dataset/test_data_non_anggota/Chicco Jerikho 001.jpeg
7  drive/MyDrive/dataset/test_data_non_anggota/Chicco Jerikho 002.jpeg
8  drive/MyDrive/dataset/test_data_non_anggota/Johnny Depp 001.jpeg
9  drive/MyDrive/dataset/test_data_non_anggota/revalina.jpeg
10  drive/MyDrive/dataset/test_data_non_anggota/Putri Marino.jpeg
11  drive/MyDrive/dataset/test_data_non_anggota/Rina Nose 002.jpeg
12  drive/MyDrive/dataset/test_data_non_anggota/Larissa Chou 001.jpeg
13  drive/MyDrive/dataset/test_data_non_anggota/Raditya Dika 003.jpeg
14  drive/MyDrive/dataset/test_data_non_anggota/Larissa Chou 002.jpeg
15  drive/MyDrive/dataset/test_data_non_anggota/Arkhana 002.jpeg
16  drive/MyDrive/dataset/test_data_non_anggota/Rio Dewanto 001.jpeg
17  drive/MyDrive/dataset/test_data_non_anggota/Raditya Dika 001.jpeg
18  drive/MyDrive/dataset/test_data_non_anggota/Johnny Depp 003.jpeg
19  drive/MyDrive/dataset/test_data_non_anggota/Putri Marino 002.jpeg
20  drive/MyDrive/dataset/test_data_non_anggota/Benedict Cumberbatch 002.jpeg
21  drive/MyDrive/dataset/test_data_non_anggota/Volodymyr Zelensky.jpeg
22  drive/MyDrive/dataset/test_data_non_anggota/Rina Nose 003.jpeg
23  drive/MyDrive/dataset/test_data_non_anggota/Rina Nose 001.jpeg
24  drive/MyDrive/dataset/test_data_non_anggota/Larissa Chou 003.jpeg
25  drive/MyDrive/dataset/test_data_non_anggota/Rio Dewanto 003.jpeg
26  drive/MyDrive/dataset/test_data_non_anggota/Amber Heard 003.jpeg
27  drive/MyDrive/dataset/test_data_non_anggota/Amber Heard 002.jpeg
28  drive/MyDrive/dataset/test_data_non_anggota/Benedict Cumberbatch 003.jpeg
29  drive/MyDrive/dataset/test_data_non_anggota/Benedict Cumberbatch 001.jpeg
30  drive/MyDrive/dataset/test_data_non_anggota/Vladimir Putin.jpeg
31  drive/MyDrive/dataset/test_data_non_anggota/Amber Heard 001.jpeg
32  drive/MyDrive/dataset/test_data_non_anggota/IMG20191017193225.jpg
33  drive/MyDrive/dataset/test_data_non_anggota/gozali(1).jpg
34  drive/MyDrive/dataset/test_data_non_anggota/galgadot -2.jpg
35  drive/MyDrive/dataset/test_data_non_anggota/yao ming (1).jpg
36  drive/MyDrive/dataset/test_data_non_anggota/titi.jpg
37  drive/MyDrive/dataset/test_data_non_anggota/sandiaga-uno.jpg
38  drive/MyDrive/dataset/test_data_non_anggota/dian.jpg
39  drive/MyDrive/dataset/test_data_non_anggota/ridwan-kamil.jpg
40  drive/MyDrive/dataset/test_data_non_anggota/airin rachmi diany 2.jpg
41  drive/MyDrive/dataset/test_data_non_anggota/claus.jpg
42  drive/MyDrive/dataset/test_data_non_anggota/yao ming (3).jpg
43  drive/MyDrive/dataset/test_data_non_anggota/galgadot -1.jpg
44  drive/MyDrive/dataset/test_data_non_anggota/yao ming (4).jpg
45  drive/MyDrive/dataset/test_data_non_anggota/teuku wisnu.jfif
46  drive/MyDrive/dataset/test_data_non_anggota/Bambanf.png
47  drive/MyDrive/dataset/test_data_non_anggota/Hasanudin.png
48  drive/MyDrive/dataset/test_data_non_anggota/Raditya Dika 002.png
49  drive/MyDrive/dataset/test_data_non_anggota/Presiden Susilo Bambang Yudhoyono.png
50  drive/MyDrive/dataset/test_data_non_anggota/airin rachmi diany.png
51  drive/MyDrive/dataset/test_data_non_anggota/Junaedi.png
------------- gambar database -----------------
1  drive/MyDrive/dataset/database/Adiyasa nurfalah.jpeg
2  drive/MyDrive/dataset/database/Riyanto riyanto2.jpeg
3  drive/MyDrive/dataset/database/Kemas Muhammad Irsan Riza (1).jpeg
4  drive/MyDrive/dataset/database/Muhammad Khaerul Naim 3.jpg
5  drive/MyDrive/dataset/database/Meredita susanty.jpg
6  drive/MyDrive/dataset/database/Yaya Setiyadi_1.jpg
7  drive/MyDrive/dataset/database/Meza Silvana.jpg
8  drive/MyDrive/dataset/database/Varuliantor Dear.jpg
9  drive/MyDrive/dataset/database/Mina Ismu Rahayu(1).jpg
10  drive/MyDrive/dataset/database/Handoko supeno-_2_.jpg
11  drive/MyDrive/dataset/database/Reza Budiawan(1).jpg
12  drive/MyDrive/dataset/database/Arief Sartono.jpg
13  drive/MyDrive/dataset/database/Dewi tresnawati.jpg
14  drive/MyDrive/dataset/database/Baud Prananto6.jpg
15  drive/MyDrive/dataset/database/Sulthoni Ashiddiiqi.jpg
16  drive/MyDrive/dataset/database/Ahmad Luky Ramdani.jfif
17  drive/MyDrive/dataset/database/Lathifah arief.jfif
18  drive/MyDrive/dataset/database/Rahman Indra Kesuma.jfif
19  drive/MyDrive/dataset/database/Imam ekowicaksono.jfif

 
I.3. Verifikasi Wajah
Untuk membandingkan kesamaan dua wajah dilakukan dengan menginput dua gambar yang akan dibandingkan, misalnya img1.jpg dan img2.jpg
	img1_path = 'drive/MyDrive/dataset/test_data_anggota/Adiyasa nurfalah-2.jpeg'
img2_path = 'drive/MyDrive/dataset/database/Adiyasa nurfalah.jpeg'

df = DeepFace.verify(img1_path, img2_path)

if df['verified'] == True:
  print('Hasil: Wajah yang sama')
else:
  print('Hasil: Wajah yang beda')

	Output:
Hasil: Wajah yang sama


	img1_path = 'drive/MyDrive/dataset/test_data_non_anggota/Raditya Dika 003.jpeg'
img2_path = 'drive/MyDrive/dataset/database/Riyanto riyanto2.jpeg'

df = DeepFace.verify(img1_path, img2_path)

if df['verified'] == True:
  print('Hasil: Wajah yang sama')
else:
  print('Hasil: Wajah yang beda')

	Output:
Hasil: Wajah yang beda


I.4. Pengenalan Wajah
Pada Deepface pengenalan wajah melakukan pencarian gambar yang tersimpan dalam folder database yang berisi kumpulan gambar referensi.
	img_path = 'drive/MyDrive/dataset/test_data_anggota/Arief sartono 10.jpg'

df = DeepFace.find(img_path, db_path = img_database_path)
print('Gambar yang mirip: ' + df.iloc[0,0])

	Output:

Gambar yang mirip: drive/MyDrive/dataset/database//Arief Sartono.jpg

 
Selain dengan cara seperti di atas, dapat juga dilakukan dengan mencari jarak yang paling dekat terhadap gambar-gambar yang ada di database. Berikut contohnya:
	def cari_kesamaan_gambar(img_test, files_database):
    
    ret = 'tidak ditemukan';
    min_val = 1;
    for img_db in files_database:

        df = DeepFace.verify(img1_path = img_test, img2_path = img_db)
        d = df['distance']

        if df['verified'] == True:
          if d < min_val:
            min_val = d;
            ret = os.path.basename(img_db)

        if df['verified'] == True:
          print(os.path.basename(img_test) + ' ' + os.path.basename(img_db) + ', Jarak: ' + str(df['distance']))
        else:
          print(os.path.basename(img_test) + ' ' + os.path.basename(img_db) + ', Jarak: ' + str(df['distance']))

    return ret
img_test = files_test_anggota[0]
ret = cari_kesamaan_gambar(img_test, files_database)
print('----------------------------------------------------------------------------')
print('Gambar ' + os.path.basename(img_test) + ' paling mendekati dengan: ' + str(ret))

	Output:

Adiyasa nurfalah-2.jpeg Adiyasa nurfalah.jpeg, Jarak: 0.1845578692533667
Adiyasa nurfalah-2.jpeg Riyanto riyanto2.jpeg, Jarak: 0.32797312843480353
Adiyasa nurfalah-2.jpeg Kemas Muhammad Irsan Riza (1).jpeg, Jarak: 0.26328849099175566
Adiyasa nurfalah-2.jpeg Muhammad Khaerul Naim 3.jpg, Jarak: 0.35967998023713
Adiyasa nurfalah-2.jpeg Meredita susanty.jpg, Jarak: 0.6735942574397717
Adiyasa nurfalah-2.jpeg Yaya Setiyadi_1.jpg, Jarak: 0.2350044404773035
Adiyasa nurfalah-2.jpeg Meza Silvana.jpg, Jarak: 0.39550654242280703
Adiyasa nurfalah-2.jpeg Varuliantor Dear.jpg, Jarak: 0.2609275262964671
Adiyasa nurfalah-2.jpeg Mina Ismu Rahayu(1).jpg, Jarak: 0.3800541719045414
Adiyasa nurfalah-2.jpeg Handoko supeno-_2_.jpg, Jarak: 0.32496067876887513
Adiyasa nurfalah-2.jpeg Reza Budiawan(1).jpg, Jarak: 0.44408465710739353
Adiyasa nurfalah-2.jpeg Arief Sartono.jpg, Jarak: 0.3656540549186218
Adiyasa nurfalah-2.jpeg Dewi tresnawati.jpg, Jarak: 0.46865269781178354
Adiyasa nurfalah-2.jpeg Baud Prananto6.jpg, Jarak: 0.25723125872311237
Adiyasa nurfalah-2.jpeg Sulthoni Ashiddiiqi.jpg, Jarak: 0.294072081470954
Adiyasa nurfalah-2.jpeg Ahmad Luky Ramdani.jfif, Jarak: 0.2949240692334252
Adiyasa nurfalah-2.jpeg Lathifah arief.jfif, Jarak: 0.49104544365336844
Adiyasa nurfalah-2.jpeg Rahman Indra Kesuma.jfif, Jarak: 0.3267417231630768
Adiyasa nurfalah-2.jpeg Imam ekowicaksono.jfif, Jarak: 0.3374931687412922
----------------------------------------------------------------------------
Gambar Adiyasa nurfalah-2.jpeg paling mendekati dengan: Adiyasa nurfalah.jpeg

I.5. Menghitung Akurasi
Perhitungan akurasi dilakukan terhadap data tes gambar yang termasuk anggota kelas dan gambar bukan anggota kelas. Berikut cara menghitungnya:
Akurasi anggota kelas
	jumlah_benar_anggota = 0
jumlah_total_anggota = 0
counter = 0;

N = len(files_test_anggota)
for img_test in files_test_anggota:
  counter = counter + 1
  df = DeepFace.find(img_test, img_database_path, silent = True, enforce_detection = False)
  if df.empty:
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: unknown (Salah)')
  else:   
    img_inp = os.path.basename(img_test).split(' ');
    img_out = os.path.basename(df.iloc[0,0]).split(' ');
    if img_inp[0] == img_out[0]:  
      jumlah_benar_anggota = jumlah_benar_anggota + 1;  
      print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0]) + ' (Benar)')
    else:
      print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0])+ ' (Salah)')

  jumlah_total_anggota = jumlah_total_anggota + 1;

akurasi_anggota = 100 * jumlah_benar_anggota / jumlah_total_anggota;
print('----------------------------------------');
print('Akurasi Anggota: ' + str(akurasi_anggota));

	Output:

1/52 Adiyasa nurfalah-2.jpeg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
2/52 Adiyasa nurfalah-3.jpeg - Terdeteksi: Baud Prananto6.jpg (Salah)
3/52 Rahman Indra Kesuma.jpeg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
4/52 Riyanto riyanto3.jpeg - Terdeteksi: Reza Budiawan(1).jpg (Salah)
5/52 Lathifah arief.jpeg - Terdeteksi: Dewi tresnawati.jpg (Salah)
6/52 Riyanto riyanto.jpeg - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
7/52 Rahman Indra Kesuma(3).jpeg - Terdeteksi: unknown (Salah)
8/52 Arief sartono 14.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
9/52 Arief sartono 13.jpg - Terdeteksi: unknown (Salah)
10/52 Arief sartono 10.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
11/52 Arief sartono 16.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
12/52 Arief sartono 11.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
13/52 Arief sartono 15.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
14/52 Adiyasa nurfalah-2.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
15/52 Arief sartono 12.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
16/52 Adiyasa nurfalah-3.jpg - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
17/52 Ahmad Luky Ramdani(1).jpg - Terdeteksi: Meza Silvana.jpg (Salah)
18/52 Arief sartono 5.jpg - Terdeteksi: unknown (Salah)
19/52 Arief sartono 2.jpg - Terdeteksi: unknown (Salah)
20/52 Handoko supeno (2).jpg - Terdeteksi: Handoko supeno-_2_.jpg (Benar)
21/52 Baud Prananto7.jpg - Terdeteksi: unknown (Salah)
22/52 Arief sartono 7.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
23/52 Baud Prananto3.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
24/52 Yaya Setiyadi_3.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Benar)
25/52 Mina Ismu Rahayu (3).jpg - Terdeteksi: unknown (Salah)
26/52 Imam Ekowicaksono.jpg - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
27/52 Arief sartono 17.jpg - Terdeteksi: unknown (Salah)
28/52 Arief sartono 6.jpg - Terdeteksi: unknown (Salah)
29/52 Baud Prananto5.jpg - Terdeteksi: unknown (Salah)
30/52 Arief sartono 9.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
31/52 Yaya Setiyadi_2.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Benar)
32/52 Kemas Muhammad Irsan Riza (2).jpg - Terdeteksi: Varuliantor Dear.jpg (Salah)
33/52 Reza Budiawan 2.jpg - Terdeteksi: Reza Budiawan(1).jpg (Benar)
34/52 Meza silvana.jpg - Terdeteksi: unknown (Salah)
35/52 Arief sartono 8.jpg - Terdeteksi: unknown (Salah)
36/52 Lathifah Arief.jpg - Terdeteksi: unknown (Salah)
37/52 Arief sartono 3.jpg - Terdeteksi: unknown (Salah)
38/52 Meredita susanty(1).jpg - Terdeteksi: Meredita susanty.jpg (Benar)
39/52 Baud Prananto4.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
40/52 Baud Prananto.jpg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
41/52 Mina Ismu Rahayu (2).jpg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Benar)
42/52 Arief sartono 4.jpg - Terdeteksi: Varuliantor Dear.jpg (Salah)
43/52 Imam ekowicaksono_1_.jpg - Terdeteksi: Reza Budiawan(1).jpg (Salah)
44/52 Handoko supeno.jpg - Terdeteksi: Handoko supeno-_2_.jpg (Benar)
45/52 Muhammad Khaerul Naim 2.jpg - Terdeteksi: unknown (Salah)
46/52 Muhammad Khaerul Naim 1.jpg - Terdeteksi: Muhammad Khaerul Naim 3.jpg (Benar)
47/52 Ahmad Luky Ramdani(2).jfif - Terdeteksi: Varuliantor Dear.jpg (Salah)
48/52 Rahman Indra Kesuma(2).jfif - Terdeteksi: Varuliantor Dear.jpg (Salah)
49/52 Meza silvana.jfif - Terdeteksi: Meza Silvana.jpg (Benar)
50/52 Rahman Indra Kesuma(1).jfif - Terdeteksi: Sulthoni Ashiddiiqi.jpg (Salah)
51/52 Baud prananto.jfif - Terdeteksi: Baud Prananto6.jpg (Benar)
52/52 Varuliantor Dear 2.png - Terdeteksi: unknown (Salah)
----------------------------------------
Akurasi Anggota: 34.61538461538461
Akurasi bukan anggota:
	jumlah_benar_non = 0
jumlah_total_non = 0
counter = 0;

N = len(files_test_non_anggota)
for img_test in files_test_non_anggota:
  counter = counter + 1
  df = DeepFace.find(img_test, img_database_path, silent = True, enforce_detection = False)
  if df.empty:
    jumlah_benar_non = jumlah_benar_non + 1; 
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: unknown (Benar)')
  else:    
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0])+ ' (Salah)')
  
  jumlah_total_non = jumlah_total_non + 1;

akurasi_non = 100 * jumlah_benar_non / jumlah_total_non;
print('----------------------------------------');
print('Akurasi Non Anggota: ' + str(akurasi_non));

	1/51 Raditya Dika 003.jpeg - Terdeteksi: Baud Prananto6.jpg (Salah)
2/51 Johnny Depp 001.jpeg - Terdeteksi: unknown (Benar)
3/51 gozali.jpeg - Terdeteksi: Dewi tresnawati.jpg (Salah)
4/51 Chicco Jerikho 002.jpeg - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
5/51 Chicco Jerikho 001.jpeg - Terdeteksi: Meza Silvana.jpg (Salah)
6/51 Benedict Cumberbatch 001.jpeg - Terdeteksi: unknown (Benar)
7/51 Benedict Cumberbatch 002.jpeg - Terdeteksi: unknown (Benar)
8/51 Arkhana 002.jpeg - Terdeteksi: unknown (Benar)
9/51 Amber Heard 002.jpeg - Terdeteksi: unknown (Benar)
10/51 Amber Heard 003.jpeg - Terdeteksi: unknown (Benar)
11/51 Arkhana 001.jpeg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
12/51 Amber Heard 001.jpeg - Terdeteksi: unknown (Benar)
13/51 Benedict Cumberbatch 003.jpeg - Terdeteksi: unknown (Benar)
14/51 Vladimir Putin.jpeg - Terdeteksi: unknown (Benar)
15/51 Volodymyr Zelensky.jpeg - Terdeteksi: unknown (Benar)
16/51 silas.jpeg - Terdeteksi: unknown (Benar)
17/51 Rina Nose 003.jpeg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
18/51 Rio Dewanto 003.jpeg - Terdeteksi: unknown (Benar)
19/51 Rina Nose 002.jpeg - Terdeteksi: unknown (Benar)
20/51 Rio Dewanto 001.jpeg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
21/51 Rio Dewanto 002.jpeg - Terdeteksi: unknown (Benar)
22/51 Rina Nose 001.jpeg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
23/51 revalina.jpeg - Terdeteksi: Dewi tresnawati.jpg (Salah)
24/51 Raditya Dika 001.jpeg - Terdeteksi: Sulthoni Ashiddiiqi.jpg (Salah)
25/51 Putri Marino.jpeg - Terdeteksi: Meredita susanty.jpg (Salah)
26/51 Putri Marino 002.jpeg - Terdeteksi: Meredita susanty.jpg (Salah)
27/51 Larissa Chou 003.jpeg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
28/51 Larissa Chou 002.jpeg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
29/51 Larissa Chou 001.jpeg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
30/51 Johnny Depp 003.jpeg - Terdeteksi: unknown (Benar)
31/51 Johnny Depp 002.jpeg - Terdeteksi: unknown (Benar)
32/51 gozali(1).jpg - Terdeteksi: unknown (Benar)
33/51 galgadot -1.jpg - Terdeteksi: unknown (Benar)
34/51 galgadot -2.jpg - Terdeteksi: unknown (Benar)
35/51 dian.jpg - Terdeteksi: Dewi tresnawati.jpg (Salah)
36/51 claus.jpg - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
37/51 IMG20191017193225.jpg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
38/51 airin rachmi diany 2.jpg - Terdeteksi: Dewi tresnawati.jpg (Salah)
39/51 yao ming (3).jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Salah)
40/51 yao ming (4).jpg - Terdeteksi: Varuliantor Dear.jpg (Salah)
41/51 yao ming (1).jpg - Terdeteksi: unknown (Benar)
42/51 titi.jpg - Terdeteksi: Meredita susanty.jpg (Salah)
43/51 sandiaga-uno.jpg - Terdeteksi: Arief Sartono.jpg (Salah)
44/51 ridwan-kamil.jpg - Terdeteksi: Varuliantor Dear.jpg (Salah)
45/51 teuku wisnu.jfif - Terdeteksi: Sulthoni Ashiddiiqi.jpg (Salah)
46/51 Hasanudin.png - Terdeteksi: Handoko supeno-_2_.jpg (Salah)
47/51 Bambanf.png - Terdeteksi: Arief Sartono.jpg (Salah)
48/51 airin rachmi diany.png - Terdeteksi: unknown (Benar)
49/51 Raditya Dika 002.png - Terdeteksi: Mina Ismu Rahayu(1).jpg (Salah)
50/51 Presiden Susilo Bambang Yudhoyono.png - Terdeteksi: Baud Prananto6.jpg (Salah)
51/51 Junaedi.png - Terdeteksi: Varuliantor Dear.jpg (Salah)
----------------------------------------
Akurasi Non Anggota: 41.1764705882353

Akurasi total:
	akurasi_total = 100 * (jumlah_benar_anggota + jumlah_benar_non) / (jumlah_total_anggota + jumlah_total_non);
print('----------------------------------------');
print('Akurasi Total: ' + str(akurasi_total));

	Output:

----------------------------------------
Akurasi Total: 37.86407766990291

II. Eksplorasi
Beberapa eksplorasi yang dapat dilakukan antara lain:
•	Model yang digunakan
•	Metrik yang digunakan
•	Detektor wajah yang digunakan
	models = ["VGG-Face", "Facenet", "OpenFace", "DeepFace", "DeepID", "Dlib", "ArcFace"]
metrics = ["cosine", "euclidean", "euclidean_l2"]
backends = ['opencv', 'ssd', 'dlib', 'mtcnn', 'retinaface']


Berikut fungsi yang dipanggil untuk menghitung akurasi:
	def hitung_akurasi(nama_model, nama_detector, nama_metrik):
  jumlah_benar = 0
  jumlah_total = 0

  for img_test in files_test_anggota:
    df = DeepFace.find(img_test, img_database_path, model_name = nama_model, detector_backend = nama_detector, distance_metric = nama_metrik, silent = True, enforce_detection = False)
    if df.empty == False:  
      img_inp = os.path.basename(img_test).split(' ');
      img_out = os.path.basename(df.iloc[0,0]).split(' ');
      if img_inp[0] == img_out[0]:  
        jumlah_benar = jumlah_benar + 1;  
    jumlah_total = jumlah_total + 1; 

  for img_test in files_test_non_anggota:
    df = DeepFace.find(img_test, img_database_path, model_name = nama_model, detector_backend = nama_detector, distance_metric = nama_metrik, silent = True, enforce_detection = False)
    if df.empty:
      jumlah_benar = jumlah_benar + 1; 
    jumlah_total = jumlah_total + 1;
    
  akurasi = 100 * jumlah_benar / jumlah_total;
  return akurasi;


II.1. Eksplorasi Model
Berikut adalah eksplorasi model-model Deepface dengan metrics = "cosine" dan backends detektor = "opencv"
	import matplotlib.pyplot as plt

nama_detektor = backends[0]
nama_metrik = metrics[0]

tabel_akurasi_model = []
for model in models:
  akurasi = hitung_akurasi(model, nama_detektor, nama_metrik);
  tabel_akurasi_model.append(akurasi)
  print('Akurasi model ' + model + '  ' + str(akurasi))

plt.bar(models, tabel_akurasi_model)
plt.ylabel('Akurasi')
plt.show()

	Output:

Akurasi model VGG-Face  37.86407766990291
Akurasi model Facenet  65.04854368932038
Akurasi model OpenFace  48.54368932038835
Akurasi model DeepFace  35.922330097087375
Akurasi model DeepID   45.63106796116505
Akurasi model Dlib  49.51456310679612
Akurasi model ArcFace  58.25242718446602


 

II.2. Eksplorasi Detektor Wajah
Detektor wajah sangat penting dalam pengenalan wajah, oleh karena itu detektor wajah perlu dieksplorasi untuk mendapatkan hasil terbaik.
	import matplotlib.pyplot as plt

idx_model_terbaik = tabel_akurasi_model.index(max(tabel_akurasi_model))
nama_model = models[idx_model_terbaik]

#nama_model = models[0]
nama_metrik = metrics[0]

tabel_akurasi_detektor = []
for nama_detektor in backends:
  akurasi = hitung_akurasi(nama_model, nama_detektor, nama_metrik);
  tabel_akurasi_detektor.append(akurasi)
  print('Akurasi menggunakan detektor ' + nama_detektor + '  ' + str(akurasi))

plt.bar(backends, tabel_akurasi_detektor)
plt.ylabel('Akurasi')
plt.show()

	Output:

Akurasi menggunakan detektor opencv  65.04854368932038
Akurasi menggunakan detektor ssd  66.99029126213593
Akurasi menggunakan detektor dlib  72.81553398058253
Akurasi menggunakan detektor mtcnn  70.87378640776699
Akurasi menggunakan detektor retinaface  71.84466019417475

 


II.3. Eksplorasi Metrik Jarak
Metrik jarak digunakan untuk mengukur kesamaan dari gambar test dengan gambar pada database. Berikut perbandingan hasil akurasi menggunakan metrik jarak yang berbeda:
	#id_model_terbaik = tabel_akurasi_model.index(max(tabel_akurasi_model))
#id_detektor_terbaik = tabel_akurasi_detektor.index(max(tabel_akurasi_detektor))

#nama_model = models[id_model_terbaik]
#nama_detektor = backends[id_detektor_terbaik]

nama_model = models[1]
nama_detektor = backends[2]

tabel_akurasi_metrik = []
for nama_metrik in metrics:
  akurasi = hitung_akurasi(nama_model, nama_detektor, nama_metrik);
  tabel_akurasi_metrik.append(akurasi)
  print('Akurasi menggunakan metrik ' + nama_metrik + '  ' + str(akurasi))

plt.bar(metrics, tabel_akurasi_metrik)
plt.ylabel('Akurasi')
plt.show()

	Output:

Akurasi menggunakan metrik cosine  72.81553398058253
Akurasi menggunakan metrik euclidean  68.93203883495146
Akurasi menggunakan metrik euclidean_l2  70.87378640776699

 


III. Hasil Terbaik
Berdasarkan eksplorasi yang dilakukan diperoleh konfigurasi terbaik sebagai berikut:
•	Nama model : Facenet
•	Nama detektor : dlib
•	Nama metrik: cosine
dengan akurasi 72.8%


	nama_model = 'Facenet'
nama_detektor = 'dlib'
nama_metrik = 'cosine'

jumlah_benar_anggota = 0
jumlah_total_anggota = 0
counter = 0;

N = len(files_test_anggota)
for img_test in files_test_anggota:
  counter = counter + 1
  df = DeepFace.find(img_test, img_database_path, model_name = nama_model, detector_backend = nama_detektor, distance_metric = nama_metrik, silent = True, enforce_detection = False)
  if df.empty:
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: unknown (Salah)')
  else:   
    img_inp = os.path.basename(img_test).split(' ');
    img_out = os.path.basename(df.iloc[0,0]).split(' ');
    if img_inp[0] == img_out[0]:  
      jumlah_benar_anggota = jumlah_benar_anggota + 1;  
      print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0]) + ' (Benar)')
    else:
      print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0])+ ' (Salah)')

  jumlah_total_anggota = jumlah_total_anggota + 1;

akurasi_anggota = 100 * jumlah_benar_anggota / jumlah_total_anggota;
print('----------------------------------------');
print('Akurasi Anggota: ' + str(akurasi_anggota));

jumlah_benar_non = 0
jumlah_total_non = 0
counter = 0;

N = len(files_test_non_anggota)
for img_test in files_test_non_anggota:
  counter = counter + 1
  df = DeepFace.find(img_test, img_database_path, model_name = nama_model, detector_backend = nama_detektor, distance_metric = nama_metrik, silent = True, enforce_detection = False)
  if df.empty:
    jumlah_benar_non = jumlah_benar_non + 1; 
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: unknown (Benar)')
  else:    
    print(str(counter) + '/' + str(N) + ' ' + os.path.basename(img_test) + ' - Terdeteksi: ' + os.path.basename(df.iloc[0,0])+ ' (Salah)')
  
  jumlah_total_non = jumlah_total_non + 1;

akurasi_non = 100 * jumlah_benar_non / jumlah_total_non;
print('----------------------------------------');
print('Akurasi Non Anggota: ' + str(akurasi_non));

akurasi_total = 100 * (jumlah_benar_anggota + jumlah_benar_non) / (jumlah_total_anggota + jumlah_total_non);
print('----------------------------------------');
print('Akurasi Total: ' + str(akurasi_total));


	Output:

1/51 Adiyasa nurfalah-2.jpeg - Terdeteksi: unknown (Salah)
2/51 Adiyasa nurfalah-3.jpeg - Terdeteksi: Baud Prananto6.jpg (Salah)
3/51 Rahman Indra Kesuma.jpeg - Terdeteksi: Arief Sartono.jpg (Salah)
4/51 Riyanto riyanto3.jpeg - Terdeteksi: unknown (Salah)
5/51 Lathifah arief.jpeg - Terdeteksi: unknown (Salah)
6/51 Riyanto riyanto.jpeg - Terdeteksi: unknown (Salah)
7/51 Rahman Indra Kesuma(3).jpeg - Terdeteksi: unknown (Salah)
8/51 Arief sartono 14.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
9/51 Arief sartono 13.jpg - Terdeteksi: unknown (Salah)
10/51 Arief sartono 10.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
11/51 Arief sartono 16.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
12/51 Arief sartono 11.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
13/51 Arief sartono 15.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
14/51 Adiyasa nurfalah-2.jpg - Terdeteksi: unknown (Salah)
15/51 Arief sartono 12.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
16/51 Adiyasa nurfalah-3.jpg - Terdeteksi: unknown (Salah)
17/51 Ahmad Luky Ramdani(1).jpg - Terdeteksi: unknown (Salah)
18/51 Arief sartono 5.jpg - Terdeteksi: unknown (Salah)
19/51 Arief sartono 2.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
20/51 Handoko supeno (2).jpg - Terdeteksi: unknown (Salah)
21/51 Baud Prananto7.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
22/51 Arief sartono 7.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
23/51 Baud Prananto3.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
24/51 Yaya Setiyadi_3.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Benar)
25/51 Mina Ismu Rahayu (3).jpg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Benar)
26/51 Imam Ekowicaksono.jpg - Terdeteksi: unknown (Salah)
27/51 Arief sartono 17.jpg - Terdeteksi: unknown (Salah)
28/51 Arief sartono 6.jpg - Terdeteksi: unknown (Salah)
29/51 Baud Prananto5.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
30/51 Muhammad Khaerul Naim 1.jpg - Terdeteksi: Muhammad Khaerul Naim 3.jpg (Benar)
31/51 Arief sartono 9.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
32/51 Yaya Setiyadi_2.jpg - Terdeteksi: Yaya Setiyadi_1.jpg (Benar)
33/51 Kemas Muhammad Irsan Riza (2).jpg - Terdeteksi: unknown (Salah)
34/51 Reza Budiawan 2.jpg - Terdeteksi: Reza Budiawan(1).jpg (Benar)
35/51 Arief sartono 8.jpg - Terdeteksi: unknown (Salah)
36/51 Lathifah Arief.jpg - Terdeteksi: unknown (Salah)
37/51 Arief sartono 3.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
38/51 Meredita susanty(1).jpg - Terdeteksi: Meredita susanty.jpg (Benar)
39/51 Baud Prananto4.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
40/51 Baud Prananto.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
41/51 Mina Ismu Rahayu (2).jpg - Terdeteksi: Mina Ismu Rahayu(1).jpg (Benar)
42/51 Arief sartono 4.jpg - Terdeteksi: Arief Sartono.jpg (Benar)
43/51 Imam ekowicaksono_1_.jpg - Terdeteksi: unknown (Salah)
44/51 Handoko supeno.jpg - Terdeteksi: unknown (Salah)
45/51 Muhammad Khaerul Naim 2.jpg - Terdeteksi: Muhammad Khaerul Naim 3.jpg (Benar)
46/51 Ahmad Luky Ramdani(2).jpg - Terdeteksi: Varuliantor Dear.jpg (Salah)
47/51 Baud prananto.jpg - Terdeteksi: Baud Prananto6.jpg (Benar)
48/51 Rahman Indra Kesuma(1).jpg - Terdeteksi: Sulthoni Ashiddiiqi.jpg (Salah)
49/51 Rahman Indra Kesuma(2).jpg - Terdeteksi: unknown (Salah)
50/51 Meza silvana.jfif - Terdeteksi: Meza Silvana.jpg (Benar)
51/51 Varuliantor Dear 2.png - Terdeteksi: unknown (Salah)
----------------------------------------
Akurasi Anggota: 50.98039215686274
1/52 Rio Dewanto 002.jpeg - Terdeteksi: unknown (Benar)
2/52 silas.jpeg - Terdeteksi: unknown (Benar)
3/52 Arkhana 001.jpeg - Terdeteksi: unknown (Benar)
4/52 gozali.jpeg - Terdeteksi: unknown (Benar)
5/52 Johnny Depp 002.jpeg - Terdeteksi: unknown (Benar)
6/52 Chicco Jerikho 001.jpeg - Terdeteksi: unknown (Benar)
7/52 Chicco Jerikho 002.jpeg - Terdeteksi: unknown (Benar)
8/52 Johnny Depp 001.jpeg - Terdeteksi: unknown (Benar)
9/52 revalina.jpeg - Terdeteksi: unknown (Benar)
10/52 Putri Marino.jpeg - Terdeteksi: unknown (Benar)
11/52 Rina Nose 002.jpeg - Terdeteksi: Meredita susanty.jpg (Salah)
12/52 Larissa Chou 001.jpeg - Terdeteksi: unknown (Benar)
13/52 Raditya Dika 003.jpeg - Terdeteksi: unknown (Benar)
14/52 Larissa Chou 002.jpeg - Terdeteksi: unknown (Benar)
15/52 Arkhana 002.jpeg - Terdeteksi: unknown (Benar)
16/52 Rio Dewanto 001.jpeg - Terdeteksi: unknown (Benar)
17/52 Raditya Dika 001.jpeg - Terdeteksi: unknown (Benar)
18/52 Johnny Depp 003.jpeg - Terdeteksi: unknown (Benar)
19/52 Putri Marino 002.jpeg - Terdeteksi: unknown (Benar)
20/52 Benedict Cumberbatch 002.jpeg - Terdeteksi: unknown (Benar)
21/52 Volodymyr Zelensky.jpeg - Terdeteksi: unknown (Benar)
22/52 Rina Nose 003.jpeg - Terdeteksi: unknown (Benar)
23/52 Rina Nose 001.jpeg - Terdeteksi: unknown (Benar)
24/52 Larissa Chou 003.jpeg - Terdeteksi: unknown (Benar)
25/52 Rio Dewanto 003.jpeg - Terdeteksi: unknown (Benar)
26/52 Amber Heard 003.jpeg - Terdeteksi: unknown (Benar)
27/52 Amber Heard 002.jpeg - Terdeteksi: unknown (Benar)
28/52 Benedict Cumberbatch 003.jpeg - Terdeteksi: unknown (Benar)
29/52 Benedict Cumberbatch 001.jpeg - Terdeteksi: unknown (Benar)
30/52 Vladimir Putin.jpeg - Terdeteksi: unknown (Benar)
31/52 Amber Heard 001.jpeg - Terdeteksi: unknown (Benar)
32/52 IMG20191017193225.jpg - Terdeteksi: unknown (Benar)
33/52 gozali(1).jpg - Terdeteksi: unknown (Benar)
34/52 galgadot -2.jpg - Terdeteksi: unknown (Benar)
35/52 yao ming (1).jpg - Terdeteksi: unknown (Benar)
36/52 titi.jpg - Terdeteksi: unknown (Benar)
37/52 sandiaga-uno.jpg - Terdeteksi: unknown (Benar)
38/52 dian.jpg - Terdeteksi: unknown (Benar)
39/52 ridwan-kamil.jpg - Terdeteksi: Arief Sartono.jpg (Salah)
40/52 airin rachmi diany 2.jpg - Terdeteksi: unknown (Benar)
41/52 claus.jpg - Terdeteksi: unknown (Benar)
42/52 yao ming (3).jpg - Terdeteksi: unknown (Benar)
43/52 galgadot -1.jpg - Terdeteksi: unknown (Benar)
44/52 yao ming (4).jpg - Terdeteksi: unknown (Benar)
45/52 teuku wisnu.jpg - Terdeteksi: unknown (Benar)
46/52 teuku wisnu.jfif - Terdeteksi: unknown (Benar)
47/52 Bambanf.png - Terdeteksi: unknown (Benar)
48/52 Hasanudin.png - Terdeteksi: unknown (Benar)
49/52 Raditya Dika 002.png - Terdeteksi: unknown (Benar)
50/52 Presiden Susilo Bambang Yudhoyono.png - Terdeteksi: unknown (Benar)
51/52 airin rachmi diany.png - Terdeteksi: unknown (Benar)
52/52 Junaedi.png - Terdeteksi: Varuliantor Dear.jpg (Salah)
----------------------------------------
Akurasi Non Anggota: 94.23076923076923
----------------------------------------
Akurasi Total: 72.81553398058253

Akurasi Total (Nilai akurasi Anggota Kelas dan Non Anggota Kelas) = 72.81553398058253
