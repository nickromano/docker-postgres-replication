# Docker Postgres Replication

[Postgres Docs: Streaming Replication](https://wiki.postgresql.org/wiki/Streaming_Replication) implemented using docker containers.

### Setup Containers

Creates two docker containers: master / follower

```bash
./setup-master-and-follower
```

Make some changes on the `master` db.

```bash
$ docker exec -it pgmaster psql -U postgres -c "CREATE DATABASE test;"
CREATE DATABASE
```

And changes will be reflected on the `follower`.

```bash
$ docker exec -it pgfollower psql -U postgres -c "SELECT datname FROM pg_database WHERE datistemplate = false;"

 datname
----------
 postgres
 test
(2 rows)
```

## Cleanup

Stop the containers and remove the data volumes.

```bash
docker stop $(docker ps -q)
docker volume rm masterdata
docker volume rm followerdata
```
