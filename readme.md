# Set up
1. `docker stack deploy --compose-file docker-compose-all.yml stolon`
2. `docker exec -it stolon_proxy.1.x59gb8eboltqfc0q6pwf6fj6m bash`
3. `stolonctl --cluster-name=stolon-cluster --store-backend=etcdv3 --store-endpoints http://etcd-00:2379,http://etcd-01:2379,http://etcd-02:2379 init`
4. `psql --host localhost --port 5432 postgres -U postgres -W`
`password1`
5. `create table test (id int primary key not null, value text not null);`
6. `select * from test;`

# Shut down
1. `docker stack rm stolon`
2. `docker volume ls -q | xargs docker volume rm`