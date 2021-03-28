# Set up
1. `docker stack deploy --compose-file docker-compose-all.yml stolon`
Await until all the services become started
`docker service ls`
2. `docker exec -it $(docker ps | grep stolon_proxy | awk '{print $1}' | head -n 1) bash` e. g. `docker exec -it stolon_proxy.1.x59gb8eboltqfc0q6pwf6fj6m bash`
3. `stolonctl --cluster-name=stolon-cluster --store-backend=etcdv3 --store-endpoints http://etcd-00:2379,http://etcd-01:2379,http://etcd-02:2379 init`
Await appearing two nodes in status
`stolonctl --cluster-name stolon-cluster --store-endpoints http://etcd-00:2379,http://etcd-01:2379,http://etcd-02:2379 --store-backend etcdv3 status`
4. `psql --host localhost --port 5432 postgres -U postgres -W`
`password1`
5. `create table test (id int primary key not null, value text not null);`
6. `select * from test;`

# Shut down
1. `docker stack rm stolon`
2. `docker volume ls -q | xargs docker volume rm`

# Check logs
`docker service logs -f stolon_keeper1`
`docker service logs -f stolon_keeper2`