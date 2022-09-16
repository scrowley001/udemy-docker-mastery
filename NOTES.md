on the default bridge network, container cannot speak to each other via DNS by default. You have to pass the --link flag and specify the container your new one is able to speak to. --link <container_name>:<alias> OR --link <container_name or ID>
command -- docker container run -d --name second_nginx --link first_nginx:firstng nginx:alpine

To inspect a network/container and find a certain section. Similar to jq. ( -f or --format )
command -- docker network inspect -f '{{ .Driver }}' new_network

Start a container called es2, put it on the new_netork, create a network alias of 'search' (acts as a load balancer). Could also use '--net' instead of '--network' or '--network-alias'
command -- docker container run -d --name es2 --network new_network --network-alias search elasticsearch:2

The will start up a new alpine container on the new_network, run nslookup on the dns name 'seach' and then close the container
command -- docker container run --rm --net new_network alpine nslookup search

If you are running an alternate command other than the default command, and its not a shell, you then don't need to provide the '-it' flag e.g.
`docker container run -it --network new_network centos:7 ping google.com`
OR
`docker container run --network new_network centos:7 ping google.com`

`docker image build -t custom-nginx .`

`docker container run -d --name custom --rm -P custom-nginx`

To run a Ubuntu machine and then be able to exec onto it, run this: 

`docker container run -d --name ubuntu-vol-test -it -v pg_vol:/var/log/test ubuntu bash`

1. Notice the volume section. Previously this volume was attached to another postgres container.
2. Inside the Postgres container at /var/logs/pg I created a file called test and put some text in there. 
3. I stopped the container and reattached the volume to the Ubuntu container at a different location and the file was still there with the text inside. 
4. So when you create a volume first and places files in there, the files inside that location are what is saved to the volume. 
5. So if you run the -v with the same named volume on a new container, the file location can be different, but all the files inside will be the same.