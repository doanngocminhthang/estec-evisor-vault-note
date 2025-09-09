(venv) PS D:\estec\project\estec_evisor\estec_evisor_code\EVisor---Backend---RnD> docker-compose logs postgres
>>
postgres  | The files belonging to this database system will be owned by user "postgres".
postgres  | This user must also own the server process.
postgres  |
postgres  | The database cluster will be initialized with locale "en_US.utf8".
postgres  | The default database encoding has accordingly been set to "UTF8".
postgres  | The default text search configuration will be set to "english".
postgres  |
postgres  | Data page checksums are disabled.
postgres  |
postgres  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
postgres  | creating subdirectories ... ok
postgres  | selecting dynamic shared memory implementation ... posix
postgres  | selecting default max_connections ... 100
postgres  | selecting default shared_buffers ... 128MB
postgres  | selecting default time zone ... Etc/UTC
postgres  | creating configuration files ... ok
postgres  | running bootstrap script ... ok
postgres  | performing post-bootstrap initialization ... ok
postgres  | syncing data to disk ... ok
postgres  |
postgres  |
postgres  | Success. You can now start the database server using:
postgres  |
postgres  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
postgres  |
postgres  | initdb: warning: enabling "trust" authentication for local connections
postgres  | initdb: hint: You can change this by editing pg_hba.conf or using the option -A, or --auth-local and --auth-host, the next time you run initdb.
postgres  | waiting for server to start....2025-09-09 08:35:48.225 UTC [48] LOG:  starting PostgreSQL 15.14 (Debian 15.14-1.pgdg13+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 14.2.0-19) 14.2.0, 64-bit
postgres  | 2025-09-09 08:35:48.228 UTC [48] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"  
postgres  | 2025-09-09 08:35:48.238 UTC [51] LOG:  database system was shut down at 2025-09-09 08:35:47 UTC      
postgres  | 2025-09-09 08:35:48.248 UTC [48] LOG:  database system is ready to accept connections
postgres  |  done
postgres  | server started
postgres  | CREATE DATABASE
postgres  |
postgres  |
postgres  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/ESTEC-User.csv
postgres  |
postgres  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/init.sh
postgres  |
postgres  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/init.sql
postgres  | CREATE TABLE
postgres  | psql:/docker-entrypoint-initdb.d/init.sql:25: error: \copy: parse error at end of line
postgres  |
postgres  | PostgreSQL Database directory appears to contain a database; Skipping initialization
postgres  |
postgres  | 2025-09-09 08:35:49.189 UTC [1] LOG:  starting PostgreSQL 15.14 (Debian 15.14-1.pgdg13+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 14.2.0-19) 14.2.0, 64-bit
postgres  | 2025-09-09 08:35:49.190 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres  | 2025-09-09 08:35:49.190 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres  | 2025-09-09 08:35:49.193 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"   
postgres  | 2025-09-09 08:35:49.200 UTC [29] LOG:  database system was interrupted; last known up at 2025-09-09 08:35:48 UTC
postgres  | 2025-09-09 08:35:49.429 UTC [29] LOG:  database system was not properly shut down; automatic recovery in progress
postgres  | 2025-09-09 08:35:49.432 UTC [29] LOG:  redo starts at 0/1509EE8
postgres  | 2025-09-09 08:35:49.444 UTC [29] LOG:  invalid record length at 0/1933288: wanted 24, got 0
postgres  | 2025-09-09 08:35:49.444 UTC [29] LOG:  redo done at 0/1932B10 system usage: CPU: user: 0.00 s, system: 0.00 s, elapsed: 0.01 s
postgres  | 2025-09-09 08:35:49.451 UTC [27] LOG:  checkpoint starting: end-of-recovery immediate wait
postgres  | 2025-09-09 08:35:49.531 UTC [27] LOG:  checkpoint complete: wrote 928 buffers (5.7%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.017 s, sync=0.057 s, total=0.083 s; sync files=305, longest=0.003 s, average=0.001 s; distance=4261 kB, estimate=4261 kB
postgres  | 2025-09-09 08:35:49.538 UTC [1] LOG:  database system is ready to accept connections

