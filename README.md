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