Dockerfile (includes best practises)

Avoid the latest tag, use explicit image references

#Exmaple 
FROM node:12-alpine3.14

FROM node@sha256:720290b95fdd62f15dbb36a0c4224572af95b48a16fb156dd271b156b189321c


#To build the docker image
docker build -t hello-world .
#To run the container
docker run -p 8081:8081 hello-world

#########You should not need to change the app code in any way########

We can bind the mount  to /app directory so that ,no need to build the image every time.

 docker run -it -v "$(pwd)/source_dir:/app/target_dir" ubuntu bash
 
###########The app should be running as a non-privileged user##########

sudo groupadd docker

sudo usermod -aG docker [non-root user]

In docker file

RUN useradd -u 8888 [non-root user]

 

USER [non-root user]

 

#####The app should be automatically restarted if crashes or is killed######

docker run --restart=always


#####The app should maximize all of the available CPUs #######

docker run -d -p 8081:80 --memory="256m" node

docker run -d -p 8081:80 --memory-reservation="256m" node

########Timezone should be in IST ##########

ENV TZ=IST

RUN ln -snf /usr/share/zoneinfo/$TZ  /etc/localtime && echo $TZ > /etc/timezone
