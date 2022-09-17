`docker service` in a swarm replaces `docker run` in containers

`docker service create alpine ping google.com`

`docker service ls`

`docker service ps <name>`

`docker service update <name> --replicas 3`
Running the `docker service ps <name>` command again would now show 3 replicas for the service

docker swarm leave --force
