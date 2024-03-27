
```
apt-get install -y postgresql16 postgresql16-server postgresql16-contrib
```

```
/etc/init.d/postgresql initdb
```

```
systemctl enable --now postgresql
```

```
nano /var/lib/pgsql/data/postgresql.conf
```

```
systemctl restart postgresql
```

```
ss -tlpn | grep postgres
```

```
psql -U postgres
```

```
CREATE DATABASE prod;
```
```
CREATE DATABASE test;
```
```
CREATE DATABASE dev;
```

```
CREATE USER produser WITH PASSWORD 'P@ssw0rd';
```
```
CREATE USER testuser WITH PASSWORD 'P@ssw0rd';
```
```
CREATE USER devuser WITH PASSWORD 'P@ssw0rd';
```

```
GRANT ALL PRIVILEGES ON DATABASE prod to produser;
```
```
GRANT ALL PRIVILEGES ON DATABASE test to testuser;
```
```
GRANT ALL PRIVILEGES ON DATABASE dev to devuser;
```

```
pgqbench -U postgres -i prod
```
```
pgqbench -U postgres -i test
```
```
pgqbench -U postgres -i dev
```

```
systemctl restart postgresql
```
