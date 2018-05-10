
1. Buat file `nginx-git-curl.yml` dengan isi :

<pre>- hosts: worker
  tasks:
    - name: Install git-nginx-curl
      become: yes #untuk menjadi superuser
      apt: name={{ item }} state=latest update_cache=true
      with_items:
        - nginx
        - git
        - curl</pre>
        
2. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts nginx-git-curl.yml -k</pre>
   
   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/nginx-git-curl.png">
   
3. Buat file `php7.yml` dengan isi :

<pre>- hosts: worker
  tasks:
    - name: PHP | Install Ondrej PHP PPA
      become: yes #untuk menjadi superuser
      apt_repository: repo='ppa:ondrej/php' update_cache=yes
    - name: PHP | Install PHP 7.2
      become: yes #untuk menjadi superuser
      apt: pkg=php7.2 state=latest
      tags: ['common']</pre>
      
4. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts php7.yml -k</pre>
   
   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/php7.png">
   
5. Buat file `php7-module.yml` dengan isi :

<pre>- hosts: worker
  tasks:
    - name: PHP | Install PHP Modules
      become: yes #untuk menjadi superuser
      apt: pkg={{ item }} state=latest
      tags: common       
      with_items:
        - php7.2-cli
        - php7.2-curl
        - php7.2-mysql
        - php7.2-fpm
        - php7.2-mbstring
        - php7.2-xml</pre>
        
6. Kemudian jalankan perintah

   <pre>nsible-playbook -i hosts php7-module.yml -k</pre>
   
   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/php7-module.png">
