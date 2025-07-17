<<<<<<< HEAD
# Docker

Java/j2EE
1.5,1.6,1.7

ear ---> Enterprize archive
war ---> web archive
jar ---> java archive

.ear ---> it is the combination of (frontend+backend) ---> catalogue+cart+shipping+user+payment
It can use only 1 db ---Oracle DB
.ear ---> multiple wars file + jar(dependies/libraries)

webspahere, weblogic,JBOSS ----> Application servers

servlet(base for any web frame woorks)+ JSP (java server pages)
100 mb ---> 120 mb

## release process
new features
defects

Business analyst(client side) + business analyst + developers + testing team + le support + l1 support + managers + leads + architect + build 
 realse manager  ----> co ordinate with all team members and make sure the realse is going as per the plan and continously update the client

  
  9-6 PM downtime
  application servers stopped
  build new application
  remove old ear 
  place new ear
  check the modules and versions
  restart the server

  if major defects

  slow, no response .... 
  restart 

  2.30 application was slow, no response 
  send the logs to developers 
  if the issue was not able to replicate

  Bridge --> Clients + L2 support + L1 support + Service Desk + Networking team + Linux team + DB team + testing team

jQuery and angularJs

here backend and frontend are separated
frontend ----> backend
API ---> rest API

war file ---> wildfly, jboss
it contain  only backend
 catalogue+cart+shipping+user+payment ---> if any component is not working or slow they will backend side = entre application we need to check here

 ## micro services
catalogue
cart
shipping
user
payment

* here all components are separted , if one component is not work remaning components are working
* every component can devlope in diffrent programming lanaguge
* loose copuling, less dependency

# real time example

Joint Families vs Small Families vs Individuals
================================================
15-20 members --> .ear file --> Physical Server --> Dedicated Host
Big House

Landed House
=============

advantages
==========
Privacy

Disadvantages
============
Costly
More time to construct
Maintanace --> Electricity, Water, Security etc.

Small Families
==============
4 members  --> VM --> Shared
small flat --> 1bhk or 2bhk

advantages
==========
less cost
less time to construct
no maintanance

disadvantages
============
privacy

Individuals --> Microservices
==============
hostels, pgs --> Containers

advantages
==========
least cost
less time
no maintanance

disadvantages
==========
0 privacy

## diagram

physical server:

hardware --> OS ---> application

- hardware means CPU, RAM, Motherboard
* we installed OS on hardware

VM ----> hardware ---> Host OS ---> hypervisior ---> guest OS ---> applications
* it blocks the resourc3 utilization
* hypervisior -- logically divides physical hardware into multiple servers
* guest os means we can use windows,ubunut or any os
* here we need to mange hypervisior
* os take more memory

vm physical server ---> hardware ---> host OS ---> containers

* It will give only what we want to run the application
* container/image ---> (bare min OS )+ system packages + application code and dependies
* it takes very less size
* it cannot block the resource utilization

## VM                         Containers
=======                       ==========  
costly							costly
more time						less time
more size						less size
more resources					less resources
resources block					dynamic resources allocation
hypervisior						no need of extra components                 
not protable                    portable
more security                   less security 

## Docker installation
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo

 sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl start docker
sudo systemctl enable  docker
sudo systemctl status  docker

docker ps ---permission denied
# It will work only for root not for normal user but  we can't take root for docker

add your normal group to docker group

sudo usermod -aG docker ec2-user
then
exit 
docker ps --- It gives running containers

AMI ---> OS + configuration(system packages + app runtime + app librairies )
image ---> bare min os + system packages + app runtime + app librairies

when you run AMI it is called server, server is running instance of AMI
container is running instance of image

docker images ---> It will show images that avaliable in system
docker pull <image_name>:<tag/version> ---To get/download the image
docker pull <image_name> --> It will take latest image
docker images 
* from where it is taking images (docker hub)
* now we need to create container from the image

docker create nginx ---> to create container
docker ps -a ----> It will all containsers including all status 
# start the container
docker start <container_id>
docker ps 
# to remove container
docker rm -f <container_ID>

# to remove image , if we remove image container also removed
docker rmi  nginx
# instead of create container, pull image ,start container we can use
docker run <image>:<tag> ---> But it block the terminal, It is foreground
docker run -d <image> ---> To dettaching the output to the screen, It will run in the background

# here nginx is running how we can access
we can get using ports
# docker diagram

docker run -d -p 80:80 <image>
# we cannot use same local port again
# to see the conatiner id's
docker ps -a -q
# to remove the CID 
docker rm -f `docker ps -a -q`

# docker gave random names while creating the conatiner. we want to give required name
docker run -d -p 80:80 --name: nginx nginx
# here name is unique

# how to login into container
docker exec -it nginx bash
-it --> interactive terminal
# checking the nginx configuration
cat /etc/nginx/nginx.conf
# to check container IP(server-check)
docker inspect nginx
# to check docker
docker inspect conatiner-name/CID
# too see the logs
docker logs nmginx

## How we can create custom images
===============================

Dockerfile ---> a set of instructions to create customised images

# 1st we need base image
FROM:
======
FROM almalinux:9

docker build -t from:v1 . ---> current docker has docker file
-t ---> tag  
. ----> log files
docker images
docker pull alpine ---> It gives very base min os 
# configure the image and install dependies
RUN:
=====
RUN commands

RUN instruction configure the image like installing packages and doing some configurations
RUN executes at the time of image building
we can have multiple run commands beacuse we will install lot of packages
docker build -t run:v1 .

# nginx run 
systemctl start nginx ---> It will run service files ---> etc/systemd/system/nginx.service
it command will execute 
CMD ["nginx", "-g", "daemon off";]

-g ---> means set the configuration directories

# what happen if i remove run:v1 in the file

docker rmi -f run:v1
docker images
docker build -t cmd:v1 
docker images.
here we gave base image is run:v1 but here we can't see image for that the it will docker hub

docker pull nginx ---> first it will check in locally is there any nginx image, if doesn't exstis it will check in docker hub
we will get error 
then go to run floder
docker build -t run:v1 .
docker images
CMD:
=====
It will run/executes at the time of container creation
i.e at the time of docker run
then
docker run -d cmd:v1
docker ps
but we cannot have multiple CMD commands. CMD should be only instrcution inside docker file

COPY:
======
It will copy the local code into container 
deamon off ---> run the deamon on background 
docker build -t copy:v1 .
docker ps
docker rm -f `docker ps -a -q `
docker run -d -p 80:80 --name copy nginx

ADD:
======
COPY and ADD both copies the code from local to conatiner, but it has 2 advantages
it can directly fetch the file from the internet 
it can directly untar the files into conatiners
docker rm -f copy
docker build -t add:v1 
docker run -d -p 80:80 --name add add:v1 

* here it will download the file but it can directly give the read acess no we need to do that
docker rm -f add
docker build -t add:v1 
docker run -d -p 80:80 --name add add:v1 
# to see the content
docker exec -it add bash
cd /usr/share/nginx/html

----------------------------------------
----------------------------------------
df -hT ---> here we are increasing /var
/var/lib/docker ---> here containers are stored/ home directory 
* imges count is increased then memory usage alos increased
* so here we need to increase the /var floder size

LABLE:
======
it is like a tag it can conatin key values pairs. 
It can used at the time of fliteration
ex: we have multiple images so we want filter using lables 
docker images  --filter label=COURSE="devops"
# how can you push the images to docker hub
log into dockerhub:

docker login -u lakshmi315

docker push label

it will give an error. for this we need to retag the lables
docker tag label:v1 lakshmi315/label:v1
docker push lakshmi315/label:v1

EXPOSE:
=======
It can be used for users to see the which port is open. 
This for doc purpose not for any funcxtionlity
docker build -t lakshmi315/expose:v1 .
docker inspect lakshmi315/expose:v1 ---> to check ports
docker push lakshmi315/expose:v1
--- her if we give run in the from command 1st it will check local so we can directly give
lakshmi315/run:v1
docker push lakshmi315/expose:v1 --- to push the image

ENV:
=====
this variables are accesable inside contaier
docker build -t lakshmi315/env:v1 .
docker run -d lakshmi315/env:v1
docker ps -a
It is exited beacause we haven't give any command to run
here i cannot use daemon beacuse we are not installling nginx instead i will give 
CMD ["sleep","1000"]
# to login into container
docker exec -it <container_id> bash
env ---> it will show envi variables

ENTYPOINT:
===========
 docker build -t entry:v1 .
docker run entry:v1
it continously running on foreground
docker ps -a 
we can overrides the CMD instrcutions 
we can't override the entrypoint instrcutions, if we try it will over rides 
docker run entry:v1 ping facebook.com
# to see th erros/full info
docker ps -a --no-trunc
"ping google.com ping facebook.com"  ---o/p for entrypont

 we can use combination of CMD and entrypoint for better results, Entrypoint will have command. default args can be suppied by CMD
 you can also overrides the default args throught the command line
 docker exec -it <container_id> bash ----> login we are getting root acess
 does containser have separate storage or it will use host storage ??
 it uses whatever the host it uss the host storage
 - if we give root acess to conainer it will block entire storage
user ----> for this we need to craete a user and use that user

WORKDIR:
===========
docker build -t workdir:v1 . 
docker build -t workdir:v1 --no-cache --progress=plain . --> for human reable
docker run -d workdir:v1
docker exec -it <CID> bash

ARGS:
======
It is like a env variable it contain key value pairs
docker build -t arg:v1 . --progress=plain --no-cache
here are we can able to acess the argfs and variables
docker run -d arg:v1
docker exec -it aa bash
env
Here we are not get the args .ARG is a build time variable
they can't be accsesed inside the containers.
ENV can be acessed build time and inside container also

# we can override also
docker build -t arg:v1 . --progress=plain --no-cache --build-arg trainer=lakshmi
arg instrcution variables can be overriden

In an exceptional case ARG can bethe 1st instrcution to supply to base OS in from 
you can't use that version after from instrcution
# how we can acess args inside container

ONBUILD:
========
while developing images you can put some conditions while others are using your images
docker build -t onbuild-test:v1 --progress=plain --no-cache .
docker run -d -p 80:80 onbuild-test:v1
<ip public ip> in browser

