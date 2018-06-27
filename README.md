# docker

This repository will be used for any docker code

Template folder contains a base structure for building docker files

# OS X build a docker machine (once docker machine is installed https://docs.docker.com/machine/)
# https://docs.docker.com/machine/get-started/#create-a-machine

docker-machine create --driver virtualbox default
docker-machine ls
docker-machine env default
eval $(docker-machine env default)
docker run busybox echo hello world     # executes hello world on busybox container in default docker machine
docker run -d -p 8000:80 nginx          # runs nginx on default machine inside docker container. container continues running.
docker-machine stop default             # stops default machine
docker-machine start default
docker-machine ip default
docker-machine rm default

# Compose references
# https://docs.docker.com/compose/compose-file/#compose-file-structure-and-examples

# Ways to make changes / save a container
# This one is not the best practice
* run vm (docker-machine create --driver virtualbox <name of machine>)
* bind shell to machine (eval $(docker-machine env <name of machine>))
* ensure machine is started (docker-machine ls
* start machine (docker-machine start <name of machine>)
* download image/os to docker-machine (docker pull alpine)
* run image (docker run -i -t alpine)
* if need to get into machine later (docker-ssh <node name>)
* adjust image from inside (mkdir average)
* add script [file in docker/average repo (vi average/average.js)
* save file
* get hostname of container should be a hash value (hostname) -or- (docker ps [from outside the container])
* leave containter (exit)
* save container changes [a sha2 hash will return] (docker commit -m "installed node and wrote average application" <container hostname>
* run command on new container image (docker run <container sha2 hash> averages/average.js 3 4 5)

# Best practice - Dockerfile
create Dockerfile
docker build <name> <dir>   # build from Dockerfile directory and tagging a name [ex. docker build andrewnascimento/test .]

# Helpful
docker network ls
docker network create --driver bridge my-network

# bridge networks do not allow container linking (container linking [via --link] is deprecated)
# there is also overlay network

# data volumes (the -v will create a local volume for the data to persist through when the container is killed) - sharing volume between containers
docker run -d -p 5984:5984 -v $(pwd)/data:/usr/local/var/lib/couchdb --name new-couchdb klaemo/couchdb

## DIDN'T WORK IN EXAMPLE - must be versioning
# data volume containers - docker containers that house a volume to be shared between containers
docker create -v /usr/local/var/lib/couchdb --name db-data debian:jessie /bin/true
# won't show in $(docker ps) [will show in $(docker ps -a)]
docker ps -a
docker run -d -p 5984:5984 -v /usr/local/var/lib/couchdb --name db1 --volmes-from db-data klaemo/couchdb
docker run -d -p 5985:5984 -v /usr/local/var/lib/couchdb --name db2 --volumes-from db-data klaemo/couchdb
curl -X PUT http://192.168.99.100:5984/db
curl -H 'Content-Type: application/json' -X POST http://192.168.99.100:5984/db -d '{"value": "Hello OReilly"}'
curl http://192.168.99.100:5985/db/faeed6d7f714f9c140a0d5e98a00049e
## flocker? 

## Docker-compose
docker-compose up   # starts all containers controlled by specific compose file
docker-compose stop # stops all containers controlled by specific compose file
docker-compose rm   # kills all containers controlled by specific compose file
docker-compose up -d   # detached start of all containers controlled by specific compose file

