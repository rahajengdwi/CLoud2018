
1. Install virtualbox di komputer host
    
    <pre>sudo apt-get install virtualbox</pre>
    
2. Download Ubuntu 16.04 dan Debian 9 yang akan digunakan

   [Ubuntu 16.04](http://releases.ubuntu.com/16.04/)
   
   [Debian 9](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
   
3. Buat 3 Virtual Machine pada virtualbox yang sudah di install (2 VM Ubuntu 16.04 sebagai worker dan 1 VM Debian 9 sebagai DB server)

    <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/vm.png">
    
4. Pada komputer host jalankan perintah

    <pre>sudo apt install ansible
   sudo apt-get install sshpass</pre>
