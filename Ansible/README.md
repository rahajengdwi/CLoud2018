# SOAL
1. Buat 3 VM, 2 Ubuntu 16.04 sebagai worker, 1 Debian 9 sebagai DB server

   [JAWABAN](https://github.com/rahajengdwi/CLoud2018/tree/master/Ansible/1)

2. Pada vm Debian install Mysql dan setup agar koneksi DB bisa diremote dan memiliki<br/> 
   <b>user: username:</b> regal<br/> 
   <b>password:</b> bolaubi
   
   [JAWABAN](https://github.com/rahajengdwi/CLoud2018/tree/master/Ansible/2)

3. Pada worker: <ol>3.1. Install Nginx<br/>
      3.2. Install PHP 7.2<br/>
      3.3. Install composer<br/>
      3.4. Install Git
    </ol>dan pastikan worker dapat menjalankan Laravel 5.6
    
    [JAWABAN](https://github.com/rahajengdwi/CLoud2018/tree/master/Ansible/3)
    
4. Clone https://github.com/udinIMM/Hackathon pada setiap worker dan setup database pada .env mengarah ke DB server.

   [JAWABAN](https://github.com/rahajengdwi/CLoud2018/tree/master/Ansible/4)
   
5. Setup root directory nginx ke folder Laravel hasil clone repo diatas

   [JAWABAN](https://github.com/rahajengdwi/CLoud2018/tree/master/Ansible/5)
   
# Hasil

  Worker1
  
  <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/Screenshot%20from%202018-05-10%2014-35-10.png">

  Worker2
  
  <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/Screenshot%20from%202018-05-10%2014-35-04.png">
