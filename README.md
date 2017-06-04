Role ioannis1.pg_initdb
=========

Uses initdb(1) to initialise a postgres cluster. If postmaster was already running at cluster it will be stopped.

Pre-conditions:
- Ansible is executing as unix user 'postgres'
- pg_config exists in the PATH, which is prepended with  ~postgres/dist-pg/bin/

Post-conditions:
- /var/log/postgresql exists
- No postmaster is running at new cluster 
- creates directory $PGDATA/conf.d  
- modifies postgresql.conf to include conf.d
- New port number is specified inside conf.d/io_1.conf 
- New {{cluster | basename}} is specified inside conf.d/io_1.conf 
- New port number is specified inside ~/.bash_pg if file exists

Requirements
------------


Role Variables
--------------

These are the default values for the variables; where, 

purge_directory:     False
cluster:             ~postgres/green
port:                5432
initdb_options:      -k --locale=en_US.UTF-8 -E utf8
postgresql_conf:     True


where,

cluster           $PGDATA directory 
purge_directory   whether to delete any pre-existing files from cluster directory. 
port              port of postgres server 
initdb_options    options to initdb(1)
postgresql_conf   Modifies postgresql.conf in order to 'include' conf/io_1.conf. Set it to 'False'
                  to disable modification and keep official configurations parameters untached.


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ioannis1.pg_initdb, cluster: ~postgres/main, purge_directory: True }

License
-------

BSD

Author Information
------------------
Ioannis Tambouras <ioannis@akroninc.net>

