
Buat file `clone-repo.yml` dengan isi :

<pre>- hosts: worker
  tasks:
    - name: Clone Repo
      become: yes 
      shell: git clone https://github.com/udinIMM/Hackathon.git && mv Hackathon /var/www/html
    - name: Composer install
      become: yes
      shell: cd /var/www/html/Hackathon && composer install
    - name: Setting Laravel
      become: yes
      copy: src=.env dest=/var/www/html/Hackathon
    - name: Composer Update
      become: yes
      shell: cd /var/www/html/Hackathon && php artisan key:generate && chmod -R 777 storage && php artisan migrate:refresh && composer update</pre>
      
2. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts clone-repo.yml -k</pre>
