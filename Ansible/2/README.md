1. Buat file `my.cnf` pada folder ansible di komputer host dengan isi :

<pre>#
# These groups are read by MariaDB server.
# Use it for options that only the server (but not clients) should see
#
# See the examples of server my.cnf files in /usr/share/mysql/
#

# this is read by the standalone daemon and embedded servers
[server]

# this is only for the mysqld standalone daemon
[mysqld]

#
# * Basic Settings
#
user		= mysql
pid-file	= /var/run/mysqld/mysqld.pid
socket		= /var/run/mysqld/mysqld.sock
port		= 3306
basedir		= /usr
datadir		= /var/lib/mysql
tmpdir		= /tmp
lc-messages-dir	= /usr/share/mysql
skip-external-locking

# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
#bind-address		= 127.0.0.1

#
# * Fine Tuning
#
key_buffer_size		= 16M
max_allowed_packet	= 16M
thread_stack		= 192K
thread_cache_size       = 8
# This replaces the startup script and checks MyISAM tables if needed
# the first time they are touched
myisam_recover_options  = BACKUP
#max_connections        = 100
#table_cache            = 64
#thread_concurrency     = 10

#
# * Query Cache Configuration
#
query_cache_limit	= 1M
query_cache_size        = 16M

#
# * Logging and Replication
#
# Both location gets rotated by the cronjob.
# Be aware that this log type is a performance killer.
# As of 5.1 you can enable the log at runtime!
#general_log_file        = /var/log/mysql/mysql.log
#general_log             = 1
#
# Error log - should be very few entries.
#
log_error = /var/log/mysql/error.log
#
# Enable the slow query log to see queries with especially long duration
#slow_query_log_file	= /var/log/mysql/mariadb-slow.log
#long_query_time = 10
#log_slow_rate_limit	= 1000
#log_slow_verbosity	= query_plan
#log-queries-not-using-indexes
#
# The following can be used as easy to replay backup logs or for replication.
# note: if you are setting up a replication slave, see README.Debian about
#       other settings you may need to change.
#server-id		= 1
#log_bin			= /var/log/mysql/mysql-bin.log
expire_logs_days	= 10
max_binlog_size   = 100M
#binlog_do_db		= include_database_name
#binlog_ignore_db	= exclude_database_name

#
# * InnoDB
#
# InnoDB is enabled by default with a 10MB datafile in /var/lib/mysql/.
# Read the manual for more InnoDB related options. There are many!

#
# * Security Features
#
# Read the manual, too, if you want chroot!
# chroot = /var/lib/mysql/
#
# For generating SSL certificates you can use for example the GUI tool "tinyca".
#
# ssl-ca=/etc/mysql/cacert.pem
# ssl-cert=/etc/mysql/server-cert.pem
# ssl-key=/etc/mysql/server-key.pem
#
# Accept only connections using the latest and most secure TLS protocol version.
# ..when MariaDB is compiled with OpenSSL:
# ssl-cipher=TLSv1.2
# ..when MariaDB is compiled with YaSSL (default in Debian):
# ssl=on

#
# * Character sets
#
# MySQL/MariaDB default is Latin1, but in Debian we rather default to the full
# utf8 4-byte character set. See also client.cnf
#
character-set-server  = utf8mb4
collation-server      = utf8mb4_general_ci

#
# * Unix socket authentication plugin is built-in since 10.0.22-6
#
# Needed so the root database user can authenticate without a password but
# only when running as the unix root user.
#
# Also available for other users if required.
# See https://mariadb.com/kb/en/unix_socket-authentication-plugin/

# this is only for embedded server
[embedded]

# This group is only read by MariaDB servers, not by MySQL.
# If you use the same .cnf file for MySQL and MariaDB,
# you can put MariaDB-only options here
[mariadb]

# This group is only read by MariaDB-10.1 servers.
# If you use the same .cnf file for MariaDB of different versions,
# use this group for options that older servers don't understand
[mariadb-10.1]</pre>

2. Buat file `mysql.yml` dengan isi :

<pre>- hosts: db
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
      mysql_db: name=hackathondb state=present</pre>
      
3. Kemudian jalankan perintah

   <pre>ansible-playbook -i hosts mysql.yml -k</pre>
   
   <img src="https://github.com/rahajengdwi/CLoud2018/blob/master/Ansible/img/mysql.png">
