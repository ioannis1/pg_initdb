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

cluster:             ~postgres/green
purge_directory:     False
pport:               5434
initdb_options:      -k --locale=en_US.UTF-8 -E utf8


These are the default values for the variables; where, 
'cluster'          is the $PGDATA directory 
'purge_directory'  is whether to delete any pre-existing files from cluster directory. 
'pport'            is the port for postgres server 
'initdb_options'   are options to initdb(1)


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ioannis1.pg_initdb, cluster: ~postgres/main }

License
-------

BSD

Author Information
------------------
Ioannis Tambouras <ioannis@akroninc.net>

