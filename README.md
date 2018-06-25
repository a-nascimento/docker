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

# Dockerfile ENTRYPOINT vs COMMAND instruction
