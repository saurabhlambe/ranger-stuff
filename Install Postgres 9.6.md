Here's how to install Postgres 9.6 in order to set up a back-end database for Ranger.

1. Install the Postgres repository
```bash
yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm -y
```

2. Install Postgres server package
```bash
yum install postgresql96-contrib postgresql96-server -y
```

3. Initialize the Postgres DB
```bash
/usr/pgsql-9.6/bin/postgresql96-setup initdb
```
