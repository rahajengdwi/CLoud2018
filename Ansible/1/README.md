
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
   
5. Pada VM jalankan perintah

   <pre>sudo apt-get install openssh-server</pre>
   
6. Pada komputer host, buat folder ansible

   <pre>mkdir ansible
   cd ansible</pre>
   
7. Buat file `hosts`, dengan isi :

   <pre>worker1 ansible_host=192.168.1.9 ansible_ssh_user=worker1 ansible_become_pass=root
   worker2 ansible_host=192.168.1.16 ansible_ssh_user=worker2 ansible_become_pass=root
   database1 ansible_host=192.168.1.15 ansible_ssh_user=regal ansible_become_pass=bolaubi</pre>
   
8. Kemudian jalankan perintah

   <pre>ansible -i ./hosts -m ping all -k</pre>

   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/ping.png">
   
   Keterangan :
   
    i. parameter -i digunakan untuk digunakan untuk mendeclare ansible inventory. 
    ii. parameter -m digunakan untuk declare module command.
    iii. parameter -k digunakan untuk menanyakan password login ssh.
    iv. parameter all digunakan untuk penanda ansible dijalankan di host mana. Parameter all bisa diganti dengan nama host.
   
 9. Untuk <b>Shell Command</b>, jalankan perintah
 
 <pre>ansible -i ./hosts -m shell -a 'uname -a' all -k</pre>
 
 <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/shellcommand.png">
 
 10. Lakukan <b>Grouping Host</b> pada file `hosts` sebagai berikut :
 
 <pre>[worker]
worker1 ansible_host=192.168.1.9 ansible_ssh_user=worker1 ansible_become_pass=root
worker2 ansible_host=192.168.1.16 ansible_ssh_user=worker2 ansible_become_pass=root

[db]
database1 ansible_host=192.168.1.15 ansible_ssh_user=regal ansible_become_pass=bolaubi</pre>
