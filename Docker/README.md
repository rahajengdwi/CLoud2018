# Soal
Nana adalah mahasiswa semester 6 dan sekarang sedang mengambil matakuliah komputasi awan. Saat mengambil matakuliah komputasi awan dia mendapatkan materi sesilab tentang Docker. Suatu hari Nana ingin membuat sistem reservasi lab menggunakan Python Flask. Dia dibantu temannya, Putra awalnya membuat web terlebih dahulu. Web dapat di download [disini](https://cloud.fathoniadi.my.id/reservasi.zip).

Setelah membuat web, Putra dan Nana membuat Custom Image Container menggunakan Dockerfile. Mereka membuat image container menggunakan base container ubuntu:16.04 kemudian menginstall aplikasi flask dan pendukungnya agar website dapat berjalan [1].

[JAWABAN](https://github.com/rahajengdwi/CLoud2018/blob/master/Docker/1.md)

Setelah membuat custom image container, mereka kemudian membuat file docker-compose.yml. Dari custom image yang dibuat sebelumnya mereka membuat 3 node yaitu worker1, worker2, dan worker3 [2].

[JAWABAN](https://github.com/rahajengdwi/CLoud2018/blob/master/Docker/2.md)

Setelah mempersiapkan worker, mereka kemudian menyiapkan nginx untuk loadbalancing ketiga worker tersebut (diperbolehkan menggunakan images container yang sudah jadi dan ada di Docker Hub) [3].

[JAWABAN](https://github.com/rahajengdwi/CLoud2018/blob/master/Docker/3.md)

Karena web mereka membutuhkan mysql sebagai database, terakhir mereka membuat container mysql (diperbolehkan menggunakan images container yang sudah jadi dan ada di Docker Hub) yang dapat diakses oleh ke-3 worker yang berisi web mereka tadi dengan environment:

<pre>username : userawan
password : buayakecil
nama database : reservasi</pre>

Selain setup environmet mysql, mereka juga mengimport dump database web mereka menggunakan Docker Compose dan tak lupa membuat volume agar storage mysql menjadi persisten[4].

[JAWABAN](https://github.com/rahajengdwi/CLoud2018/blob/master/Docker/4.md)
