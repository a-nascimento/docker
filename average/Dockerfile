# FROM selects base image to use, must be first instruction
FROM alpine
# MAINTAINER sets the owner, does not affct functionality
LABEL andrewnascimento <afn3286@gmail.com>
# RUN issue commands in image
RUN apk update && apk add nodejs
RUN mkdir average
# ADD add local files to image, must be in current or directory below current dir
ADD average.js average/
# WORKDIR set current working directory
WORKDIR /average/
# ENTRYPOINT defines main process that will be run inside the containter (in JSON list)
# can't include environment vars
ENTRYPOINT ["node","average.js"]

