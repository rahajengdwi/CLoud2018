
Buat file `.env` pada folder ansible di komputer hosts dengan isi :

<pre>APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:rUSmIhQ2jp9bremjUuDeZz9wToEBOu0rJk8zuFdErCA=
APP_DEBUG=true
APP_LOG_LEVEL=debug
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=192.168.1.15
DB_PORT=3306
DB_DATABASE=hackathondb
DB_USERNAME=regal
DB_PASSWORD=bolaubi

BROADCAST_DRIVER=log
CACHE_DRIVER=file
SESSION_DRIVER=file
QUEUE_DRIVER=sync

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=</pre>

2. Buat file `clone-repo.yml` dengan isi :

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
      
3. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts clone-repo.yml -k</pre>
