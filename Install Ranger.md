Here's how to quickly install Ranger in your HDP cluster. Use this bash [script](https://gitlab.com/saurabhlambe/Ranger-stuff/-/blob/01f5a8da2b704aa7899ce0ddcecf3c4680ad5fc0/install_postgres_9_6.sh) to install Postgres-9.6 or follow these steps to install it manually.

1. Install the Postgres JDBC driver and let Ambari server know about it:
```bash
yum install postgresql-jdbc -y && chmod 644 /usr/share/java/postgresql-jdbc.jar && ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar
```

2. Create a user role, database, and set password to the user:
```bash
psql
CREATE DATABASE ranger;
CREATE USER ranger WITH PASSWORD 'bigdata';
GRANT ALL PRIVILEGES ON DATABASE ranger TO ranger;
```

3. Let postgres know about the users who will access the database:
```bash
echo "local all postgres,ranger,rangerlogger trust
host all postgres,ranger,rangerlogger 0.0.0.0/0 trust
host all postgres,ranger,rangerlogger ::/0 trust" >> /var/lib/pgsql/data/pg_hba.conf
```
Note: when using Postgres-9.6, the file would be ```/var/lib/pgsql/9.6/data/pg_hba.conf```.

4. Refresh postgres configs:
```bash
su postgres -c '/usr/bin/pg_ctl -D /var/lib/pgsql/data reload'
```
Note: for Postgres-9.6, restart the service:
```bash
systemctl restart postgresql-9.6
```

5. Proceed with the new service installation wizard in Ambari.
