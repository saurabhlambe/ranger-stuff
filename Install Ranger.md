Here's how to quickly install Ranger in your HDP cluster. Here we shall user Postgres as the back-end database for Ranger.

1. Install the Postgres JDBC driver and let Ambari server know about it:
```bash
yum install postgresql-jdbc -y && chmod 644 /usr/share/java/postgresql-jdbc.jar && ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar
```

2. Create a user role, database, and set password to the user:
```bash
psql
CREATE DATABASE rangerdb;
CREATE USER rangerdba WITH PASSWORD 'bigdata';
GRANT ALL PRIVILEGES ON DATABASE rangerdb TO rangerdba;
```

3. Let postgres know about the users who will access the database:
```bash
echo "local all postgres,rangerdba,rangerlogger trust
host all postgres,rangerdba,rangerlogger 0.0.0.0/0 trust
host all postgres,rangerdba,rangerlogger ::/0 trust" >> /var/lib/pgsql/data/pg_hba.conf
```

4. Refresh postgres configs:
```bash
su postgres -c '/usr/bin/pg_ctl -D /var/lib/pgsql/data reload'
```

5. Proceed with the new service installation wizard in Ambari
