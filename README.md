## Postgres DB replication

### local (laptop)

```
$ docker stack deploy --compose-file=./docker-compose.yml testdb
Creating service test_portainer
Creating service test_primary
Creating service test_replica
Creating service test_app
Creating network test_cisnet
```

Check portainer on http://localhost:9000

```
docker stack ls
docker service ls
docker service ps test_primary
docker ps
```

Exec into PRIMARY to create a table aemployee
```
$ docker exec -ti iqjvpn1av6i4 psql postgresql://primaryuser:password@localhost:5432/testdb
testdb=> create table aemployee();
CREATE TABLE
testdb=> \d
                 List of relations
 Schema |        Name        | Type  |    Owner    
--------+--------------------+-------+-------------
 public | aemployee          | table | primaryuser
 ```

Exec into REPLICA to make sure the table exists
```
$ docker exec -ti 6c psql postgresql://primaryuser:password@localhost:5432/testdb
testdb=> \d
                 List of relations
 Schema |        Name        | Type  |    Owner    
--------+--------------------+-------+-------------
 public | aemployee          | table | primaryuser
```
# docker-database-replication
# docker-database-replication
