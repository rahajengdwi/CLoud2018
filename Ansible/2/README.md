
1. Buat file `mysql.yml` dengan isi :

- hosts: db
  tasks:
    - name: Install Mysql
      become: yes #untuk menjadi superuser
      become_user: root
      become_method: su
      apt: name={{ item }} state=latest update_cache=false
      with_items:
        - mysql-server
        - python-mysqldb
    - name: Backup my.cnf
      become: yes
      become_user: root
      become_method: su
      shell: mv /etc/mysql/mariadb.conf.d/50-server.cnf /etc/mysql/mariadb.conf.d/50-server.cnf.bak
    - name: Copy File
      become: yes
      become_user: root
      become_method: su
      copy: src=my.cnf dest=/etc/mysql/mariadb.conf.d/50-server.cnf
    - name: Restart Mysql
      become: yes
      become_user: root
      become_method: su
      shell: /etc/init.d/mysql restart
    - name: Mysql User
      become: yes
      become_user: root
      become_method: su
      mysql_user:
        login_user: root
        login_password: bolaubi
        name: "{{ item.name }}"
        host: "{{ item.host | default('localhost') }}"
        password: bolaubi
        priv: "*.*:ALL,GRANT"
        #priv: "{{ item.priv | default('*.*:ALL,GRANT') | join('/') }}"
        append_privs: "yes"
      with_items:
        - { name: regal, host: 192.168.1.15 }
        - { name: regal, host: 192.168.1.9 }
        - { name: regal, host: 192.168.1.16 }
    - name: Make DB-Table
      become: yes
      become_user: root
      become_method: su
      mysql_db: name=hackathondb state=present
      
2. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts mysql.yml -k</pre>
   
   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/mysql.png">
