https://docs.docker.com/
--------------------------section 1------------------------
##########################video-1##############################

Linux refers to the kernel not the os 
kernel is between hardware and the os 
drivers are on the kernel 

microsoft windows os and kernel is one package

unix the kernel is package with whatever os depending on the owner company

macos darwin based which is a unix-like system also packaged with os and hardware apple offers a bigger package

#########################video-2###############################

histrionically there where no pc only servers there were only unix 


 ---------->they need isolation , multi-host environment  
server ----> chroot(root jail),
----------->to distribute system resources

choot is beyond permission its literally isolated each user will have his dedicated file-system replica that can be used by a specific user 

ulimit can set limits on server resources but doesnt apply to cpu resources because its shared  

nice/renice they are the best cpu resources management 
40 years old tools boom !!

1998 ---> vmware

complete isolation , hypervisor made complete isolation between every machine each will have his cpu resources memory networking ......
----------------------> vm1
pc on steroids -------> vm2
----------------------> vm2

hardware virtualization   

machine (with installed hyper-visor i.e vmware) 
can host multiple Virtual machine is built on it with complete resource isolation 

os virtualization (chroot)
Linux/unix in base , they give access to make  isolation spaces for multi-users so each user work is not mixed or corrupted by other users 

from 2002
on Linux level
Control Groups (cgroups)
Linux Namespaces 

2008
Linux containers (lxc)
self contained environment on the kernel level that's why it need someone who knows code who knows kernel interfaces since it was low level interaction with kernel every thing was on Linux(kernel)

That's were dockers emerged 
this is a boooom ! 
Docker made the concept of containers accessible to a larger audience, Now we can any application any tool with complete isolation any container will ave its file-system completely de-coupled from the machine they operate on kernel level which made any container portable to any linux kernel whatever the distribution was, any container only sees (it-self) they are allowed certain memory , disk spaces with a cpu resources to run and they accommodate to that, in short they did every thing lxc could provide in term of accessibility 


###########################video 3#######################333
docker client: tool which i interact with 
docker server: interpret the commands forwarded from the client and handles the cgroups and namespaces the lxc to create the container 



installation guide : 
docker desktop : lite weight linux vm is installed so the docker engine(docker backend server) could be hosted since docker installed on kernel it communicates with the kernel level so it need the vm and a docker client as an interface to give commands to the docker.
docker desktop used in windows and Macos the desktop as said will be a lite weight vm that runs the docker engine and the docker client will be on the system

if we already have linux as our OS we only just need the engine 
no need for linux desktop except if we need a layer of isolation if want the docker environment to run as if it is sand-boxed since the docker engine will not run directly on our kernel but on the docker desktop lite weight kernel   



--------------------------section 2------------------------
##########################video-4##############################
docker image ---> Consider it as the template for the docker container 

docker pull busybox -> it contains some commands and diagnostic tools for troubleshooting linux

docker images -> list all available images

docker images are pulled from docker registry(docker-hub)

docker run busybox -> if busybox is not on the system it will automatically pull and run the container, container in that sense will run as a process in the background completely isolated with its allocated resources and gives a big  
hola bitch !!!  

image has two types 
predefined to run a certain command on container run command

containers that can run multiple commands they are designed to run as per given input (CLI argument), so the container just not start up (msh hay2om ya3ny)

docker run busybox echo "hello word"   <- CLI arguments  
it will execute it then stops !!
container has more usages this is just a trivial example

docker run busybox ls -l ---> will list the container file-system its like chroot that created a private file-system replica but now it on a container 

container will never continue running as long as the command it executes finish 

RULE--> container lifetime is command run time execution it doesn't matter if the command exists successfully or failed the container will seize to run 
(container lifetime = command runtime)

docker ps ->  list all running container process 
-a -> all container regardless there state 
containers have unique ids



docker run busybox sleep 5 
docker run busybox sleep infinity -> sleeps until its manually terminated 

docker run --detach busybox sleep infinity -> detach from my current bash process(entry point bare in mind that ps also shows the entry point command to the container) , detaches from current terminal (-d) 


docker exec container ID nc -zv  google.com 80 (nc:net-cat is like Swiss knife of networking , here nc checks if port 80 is open in host google.com), i can use containers that has nc with a little bit older version 

docker exec -it container ID sh (attach a shell to the container, as long as the shell type is available )
it-> stands for interactive terminal ? i think so 

-------------- container operations --------------

docker stop  ID --> its stopped but not removed its on my system

docker start ID--> start the container directly without needing to detach or pass sleep infinity again 

docker stop ID
---------------> docker rm -f ID (combines both stop and rm)
docker rm   ID
after removing the we will need to us run command if we want the container it is completely removed 

-------------------- operations on image level ------------
good practice remove all non used images because it occupies space
docker images 
docker rmi image id 

if container uses an image there will be an error in removing the image 
we can use -f but its not a good practice since it forcefully remove the image 
 

docker containers runs in an instant very very fast unlike a virtual machine a whole os will startup

docker container ---> The running container which is based on a docker image 



##########################video-5##############################
1st example of docker container was the busy box is that the only use, is our approach only revolves around using a container that has commands which i need to use that's not available to my system ?? 

to create a server a daemon, web server most used example we want web server just to host a static website an ad or something very very simple  

I don't want to install the web server on my machine i want to sandbox it to run it in an isolated environment 

nginx is many things but now lets look at it as a web-server 

now we will run nginx through a docker container 

docker run -d nginx (p.s unlike busybox is not configured to run any command its a container with a diagnostics and networking tool kit for debugging so the commands are for us to be executed so if no commands were directed to the container it just turn down in nginx container it is configured to run the nginx service so it continue on running upon the container run command)

docker ps --> will list port its listens on 

the nginx container is a web-server so it listens on a port, the problem is that it listens on the port but on the container network internal network created for that container so the pc will not be able to access the web-server because its on a different network

docker run -d -P nginx
-P -> random port is opened on the host system and is mapped to the container port this is called port mapping or port forwarding (NAT) the traffic now 8080 is dealt with as its the port of the container hence the word mapping or even forwarding it forward the traffic to the container so it could listen to any request from any where (0.0.0.0:8080->80) and reply to the request 0.0.0.0 means any where(any ip)

docker run -d -p 8080:80
-p -> to decide which port to open on host system 
host port:container port

--name mywebserver --> to name the container 

docker run -d -p 8080:80 --name mywebserver nginx 

docker ps

##########################video-6##############################

volume : a combination of files that resides somewhere on the disk (بالعربي معنها مجلد والترجمه مش هتقرب الموضوع هنا)

Files in the container are not persistent if the container deleted any data on the container is also deleted 
**is there any difference between stopped and deleted ??** 
The data is lost when the container is removed, not when it's stopped or restarted.
Basically, if you do `docker ps`, **if the containers keeps the same id (the big ugly hexadecimal id)**, the data is not lost.
It gets complicated when somehow your docker containers are not managed by you, but by some kind of automated-managing method. Tools like these usually start new containers if there is failure. In that case you should mount a volume to store your data on the host.

docker run  -it busybox sh

vim hello.txt

exit or terminate the sh shell the container in our case the busybox container will seize to exist since the container entry point command is killed which was the sh shell (parent process of the container)

file created in a layer called ephemeral layer a volatile layer that lives as long as the container lives 

docker run  -it busybox sh
now lets do the opposite lets delete something very critical in our container such as 
rm /bin/env 
exit 
docker run  -it busybox sh 
ls -l --> the /bin/env --> booom!!  its there 

that's why its a very strong concept its a very safe environment (sand boxed environment)for experimenting if that happened on the host machine its impossible to retrieve and its a headache to retrieve if there are backups 

I want my files persistent because sometimes its a database container so the files must be persistent !! so if the container is closed and the image is removed the files are still persistent 
*for that we use* 
volumes ---> named volumes , anonymous volumes
bind mount 

volumes -> named volumes (the who has name or the defined volumes)

docker manages this files 
/var/lib/docker/volumes --> only accesses by root user , contains docker volumes so it can have multiple volumes for multiple containers  

volume can be used by multiple containers,multiple user can't write in the same file in the same time its a corner case actually the os wont be able to handle something like that it may create locking issues 

docker volume create mydata 
sudo -l /var/lib/docker/volumes 
now the files is accessed by host through that path and through the container internally 

docker run -it -v mydata:/opt busybox sh  
-->
-->
-->
vi /opt/hello.txt 
exit 
docker ps --> why use this line ? 

docker run -it -v mydata:/tmp alpine sh
ls -l /tmp/hello/txt
cat /tmp/hello.txt 
exit 

cat /var/lib/docker/volumes/mydata/\_data/hello.txt
--> \_data is created by the docker engine inside the volume and stores files in it

docker run -d -it -v mydata:/tmp alpine sleep infinity 
docker run -d -it -v mydata:/opt busybox sleep infinity 
docker ps

docker exec -it ID_1 sh 
vi /opt/hello.txt
exit ---> (the container will still be working since the entry point is still running the sleep inifinity)


docker exec -it ID_2 sh 
cat /tmp/hello.txt
exit

docker run -it -v dbdata:/data busybox sh
--> docker will create everything the volume , the directory that's inside the container if its not there by default everything u want it will be there thanks to the docker engine 
ls -ld /data/
exit

docker volume ls 
--> a good practice in sense of house keeping of my system is to delete unused systems, it can consume disk space out of thin air  
--> you need to make sure for safety measures that the volume is not used by any container 
for i in 'docker ps -a | awk {'print $1'}
for>do 
for>docker rm -f $i
for>do 
or
docker volume rm mydata
docker volume dbdata 

##########################video-7##############################

volumes -> Anonymous volumes

both types of volumes are managed by the docker engine except that the name is managed by me in named volumes 

like named container anonymous volumes can be used by multiple container as long as its not used in the same time that's the main difference 

so before named volumes what happened is there were a container which is used to create a volume and another container which is the application and the volume was referenced to through the container.If you create multiple containers consecutively that each use anonymous volumes, each container creates its own volume. Anonymous volumes aren't reused or shared between containers automatically. To share an anonymous volume between two or more containers, you must mount the anonymous volume using the random volume ID.
To mount a volume with the `docker run` command, you can use either the `--mount` or `--volume` flag.
```console
$ docker run --mount type=volume,src=<volume-name>,dst=<mount-path> 
$ docker run --volume <volume-name>:<mount-path>
```



docker manages the anonymous volumes,anonymous are only deleted when the container is deleted (-v), it doesn't have a name so we need to remove the container with -v 

named volumes offers everything anonymous offers in addition to complete decouple of volume from container hence deleting the volume wont affect the container and can be created with name as its only identifier it doesn't need to be tangled to a container


90% named volumes will be used 
or bind mounts

docker run -it -v /myvol busybox sh 
exit
docker ps -> no traces of the container 
->p.s we need to stress that the container is there but stopped so it doesn't have a pid so ps doesn't show it that's why on just stopping the container the volume persist unlike deleting it the volume will also be deleted 
sudo ls -l /var/lib/docker/volumes --> esmo mor3b kda and that to guarantee uniqueness  

docker ps -a 
docker rm **-v** container id ---> container is deleted 
-v must be used to delete the volume 
sudo ls -l /var/lib/docker/volumes 




##########################video-7##############################
bind mount 

docker run --name static-site -v \<path-of-directory-to-bind\>

docker run --name static-site -v $(pwd):/usr/share/nginx/html:ro -p 8080:80 -d nginx 

we mounted our directory which contains the static website to the nginx html directory that is used by nginx container to sources from it the website it will host (serve)
ro -----> read only if i want to make the container read-only only the host machine can edit the files 
/usr/share/nginx/html --> default path where nginx goes to see if there is an html file to serve 

docker run -v mywebdata:/usr/share/nginx/html:ro -P -d nginx 
mywebdata --> volume will be created automatically 
-P --> will automatically open a port on my host pc

bind mount and volume how are they different 
--->
--->
--->
--->
--->
--->











##########################video-8##############################

we agreed on that the container lives in an isolated namespace so needed to map the container ports to our host machine so we could access nginx container 

docker run -d nginx 

docker ps -> to retrieve container ID 
docker exec -it containerID sh 
ifconfig or ip addr (for modern versions of linux if docker container contains a package manager i can install it but once the container is closed everything is lost since i can't add anything to the image which is the container is based from) 
exit

docker inspect containerID/container name ---> we can find our container ip 

docker run -it alpine sh 
ping 172.07.02 -> nginx container 
apk add curl
curl 172.17.0.2 --> http request to nginx 
if it replies with html page that means that nginx is accessible through the containers network called bridge network 
and of type bridge its a virtual network used by docker as long as the container are on the same host they can communicate over that virtual network,docker install a virtual network interface (virtual network adapter)called docker_0 it has an ip address,its of type bridge which allows containers to communicate and assign ips to all  containers on the host machine which is part of a certain docker network

ping container name ---> it will not work because we need some kind of mapping or resolving to workout the resolution of container name to its ip some kind of DNS docker offer something called service discovery but it not a DNS 

docker network ls  --> types of network that docker offer 
docker network create my_bridge --driver bridge 
docker network 

docker ps 
docker network connect my_bridge containerID  -> new network new ip so two different completely isolated so i can segregation between multiple networks of container on the host machine another level and type of isolation docker networks 

docker run -it --network my_bridge alpine sh 
ping containerID
ping containerName --> now it works what happened is when creating a new network docker gives you something called service discovery which something that maps the names and ips on that network so i can ping any container with its name directly as long as Iam on the network, Default bridge will not offer this service !!!!!!

##########################video-9##############################
Host network
Docker will make the container use the host machine network adapter(network interface) as its own, now the container as it left its isolation the docker container is now as its running on the system so it can be used and accessed directly through local host without natting (mapping) of ports 

the story in windows/macos as main os is different since the host of docker is a lite vm which make docker operate, so we cant use docker engine directly since we don't have access to the kernel does that mean we cant access the containers from local host? 
No now the containers is viewed as just a service/process on the system that has a port that allows it to communicate with other process or services and all the container will share the same host pc private ip because they are all now treated as just a process on the host not an isolated one so these services are accessed through there dedicated ports 
(host-ip : port)

for security concerns don't use host network because we have now access to the host network and the isolation hugely affected of-course

mac-Vlan network 
container takes different ip from the range of my network interfaces 
and takes a mac-address 

docker network create -d macvlan --subnet=192.168.2.0/24 \      --gateway=192.168.2.1 -o parent=ens18 pub_net 
--> --subnet=192.168.2.0/24  my private network name  

this network is not isolated as bridge network

docker run -it -d --network pub_net httpd
docker inspect containerID
container is accessed through container ip and port from browser 

some application work in layer data-link layer like wireshark package sniffing app monitor packet in a network, so if we need to run such application we the mac-vlan type of network (security application solution)

mac-vlan and host can access the internet through the network since its dealt with as device on the network so it can access and be accessed 
---------------------------vs------------------------------
bridge also can access the network but can't be accessed from outside 

none full isolation to the container no communication at all 
docker run -it --network none alpine sh 
it is used to test malicious software testing for example





--------------------------section 3------------------------
#########################video-11##############################

docker containers data is ephemeral, all changes on file system is deleted after the container is deleted that's why used volumes and Bind mounts so why that happens......

image is designed to be for multiple users not one user only..
imagine if there is an image designed to use port 8000 but i changed the configuration to be 80 and other users used it it will create conflicts in our application and will need thorough inspection to see were the problem is....so the image is something like standard template that is being used as foundation to build on

file-systems -> dictates how an OS should deal with the files on the disk (adding , modifying , deleted)

docker uses UFS -> union file-system 
UFS -> is consisted of layers unlike normal filesytems deals the the file as its flat just access the file directly here in UFS the files are in layers that are read only, when we add files there are an additional layer (R/W) thats added on the top
(outer most layer) and its deleted when the container is deleted 

what if edited a file from the read-only layer the base layer of the image that's the container is based from it ?
the UFS copy the read-only file and an outer most layer is created with our modification and that outer most layer shadowed the read-only layer same goes for deleting a layer(file) from the read-only layers it will be shadowed with a layer on top with the deletion record of that layer..... but that wont affect if we created a new container based on the same image changes wont be reflected 

in volumes and bind mount -> the files are handled in the same manner of the OS file system 

docker run -it ubuntu bash 
touch test 
exit

docker diff containerID ---> shows the differences between the container and the image file (A:add , c:change , D:delete)

docker start containerID 
docker exec -it containerID bash
rm /etc/legal 

docker diff containerID

docker exec -it containerID bash
apt update 
apt install -y curl
exit

docker diff containerID ---> BOOM!! big number of files(layers) is added over the image 

docker commit containerID  mod_ubuntu:1.0 
-> will generate a sha256 for the image , there are a sha256 unique for every layer of the image. we only see the latest layer sha256 and it will refer to the image #themoreyoufuckaroundthemoreyouknow 
(outer most layer sha 256 = image sha256 )

we should use another name because we will be creating a new image so we take the top layers (our changes on the file-system)
and union it with the original read-only layers and create a new image with new name so we don't create conflicts with the ubuntu base image because it may be used across multiple domains in the project  **(DOCKER IMAGES ARE IMMUTABLE)** 

docker run -it mod_ubuntu:1.0 bash 
curl ---> is installed 

docker image ls --> ubuntu mode is nearly twice the size 
1- Docker images are immutable 
2- A copy of the file will happen to exist in the top layer of the UFS and it will represent the recent updates 
3- this scenario will happen for an file even if its the same file again 
4- Any file operation = new layer = n number of duplicate of the same file 
thats why we might end up with a huge image because of that replication behavior 


**we need tracking to that modification done on the image here the Docker file will play a crucial role** 

##########################video-12##############################
Docker file : docker offers a very simple to-do website to use as a playground for docker file its in java-script

Docker file is useful so can track what layers are added to the image and changes made for an image


1- clone the project from docker repository 
getting-started-app

cd getting-started-app
vim Dockerfile

**FROM node:18-alpine** --> constant updates and security patches, maintenance headache are not mine to worry about so if there is a base image with my needed runtime (in our case nodejs)  available please use it and reinvent the wheel, From is also used to determine the base image Iam going to build my image on 

**WORKDIR /app** --> mdkir /app ; cd /app 

**COPY . .** --> copy files and directories from current working directory with respect to the image to /app in our case , we can use paths instead of . .
- `COPY <host-path> <image-path>` - this instruction tells the builder to copy files from the host and put them into the container image.

**ADD** --> can copy and download from URLs and decompress TAR archives, also can download and if the downloaded is compressed its decompressed and added to the image, if i want the file compressed then i must use COPY  

(we need some dependencies and the image we are using already handled the needed tools like **yarn** its there as a part of the node-18 image its used to install the dependencies thats why its recommended to use an image with a runtime environment because any application will need dependencies to run) 

**RUN** --> yarn install --production && yarn cache clean
cache cleans 
-> discard any extra module and files thats not needed to reduce image size and we tended to use && to reduce the layers because if each are used with RUN it will be extra layers with potential to multiple duplicates because the new layer might need file from lower layers so copies overhead will be added to the image size 

**ENTRYPOINT** ["node"] --> the parent process of the container as long as that process is running the container will run, ["node"] is the file i want the container start so when we hit the command docker run , that file (command node) will execute the scripts under src/index.js we can also take that approach 
[] means its a list so we can pass whatever scripts we want to the node command to run it ["node","src/index.js"]

**CMD** ["src/index.js"] --> CMD is used as a best practice because the command here will be considered as a sub process of the entry point so now that container could run any script its the same as passing it as argument to the container like we did it earlier with busybox the only difference is that it didn't have an entrypoint command that persists 

**EXPOSE 3000**  --> just an indication that the app listens on port 3000 but this line doesn't mean that we exposed that port 
so if i wanted to expose the app it will be through mapping port 3000 to an port on the host pc

**docker build** **-t getting-started .**--> expect a file named Dockerfile with the same case's(capitalization) in the current working directory , if it has another name we use **-f** , **-t** is the tag and the **.** means the docker file is in current working directory this is where i will build 

docker image ls 
docker run -d -p 3000:3000 getting-started

docker run getting-started -e "console.log('hello')"
-> we did over ride the CMD command that was used in the Dockerfile and thats why is used as a best practice to use ENTRYPOINT and CMD since in that manner we could pass any other script or command to the node command to execute 


The documentation states for `CMD`-
> The main purpose of a CMD is to provide defaults for an executing container.

and for `ENTRYPOINT`:

> An ENTRYPOINT helps you to configure a container that you can run as an executable.

So, what's the difference between those two commands?

Docker has a default entrypoint which is `/bin/sh -c` but does not have a default command.
When you run docker like this: `docker run -i -t ubuntu bash` the entrypoint is the default `/bin/sh -c`, the image is `ubuntu` and the command is `bash`.
**The command is run via the entrypoint. i.e., the actual thing that gets executed is `/bin/sh -c bash`. This allowed Docker to implement `RUN` quickly by relying on the shell's parser.**


Later on, people asked to be able to customize this, so `ENTRYPOINT` and `--entrypoint` were introduced.

Everything after the image name->(**`ubuntu`) in the example above, is the command and is passed to the entrypoint.** **When using the `CMD` instruction, it is exactly as if you were executing**  
**`docker run -i -t ubuntu <cmd>`**  
The parameter of the entrypoint is `<cmd>`.

You will also get the same result if you instead type this command `docker run -i -t ubuntu`: a bash shell will start in the container because in the [ubuntu Dockerfile](https://github.com/dockerfile/ubuntu/blob/master/Dockerfile) a default `CMD` is specified:  
`CMD ["bash"]`.

**Example ..........**
As everything is passed to the entrypoint, you can have a very nice behavior from your images. this is a good, it shows how to use an image as a "binary". When using `["/bin/cat"]` as entrypoint and then doing `docker run img /etc/passwd`, you get it, `/etc/passwd` is the command and is passed to the entrypoint so the end result execution is simply `/bin/cat /etc/passwd`.

Another example would be to have any cli as entrypoint. For instance, if you have a redis image, instead of running `docker run redisimg redis -H something -u toto get key`, you can simply have `ENTRYPOINT ["redis", "-H", "something", "-u", "toto"]` and then run like this for the same result: `docker run redisimg get key`.

```
docker run -d ubuntu:14.04 /bin/bash -c "while true; do echo hello  world;done"
```

> bash interprets the following options when it is invoked:
> -c string
> If the -c option is present, then commands are read from string. If there are arguments after the string, they are assigned to the positional parameters, starting with $0.

Without the `-c`, the `"while true..."` string is taken to be a filename for `bash` to open.

Resources:
https://docs.docker.com/reference/dockerfile/#entrypoint
https://docs.docker.com/build/building/best-practices/
https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/



##########################video-13##############################



we were introduced to a docker file to build a nodejs image and the process is similar for any application weather its ruby .net it doesn't now we need to publish our image so we can move it around so we need to move it a place where we can pull it from. 

To push a docker image we need docker registry 
public registry -> any one can pull it  
private registry -> need credentials to pull images from it  

the Dockerhub is an example of a docker registry 

docker login registry url or (just go with the steps docker is completely integrated with Dockerhub)

docker push getting-started --> **will fail** 

docker pull ubuntu --> ubuntu == `docker.io/library/ubuntu:latest`
docker.io --> registry
library --> username , namespace , organization name 
`library is a namespace used by google`
ubuntu:latest --> ubuntu = image(repo) name , latest = (tag)

when we use ubuntu directly docker implicitly uses the whole as represented above and that is only applicable from docker official images since if the path is not explicitly used docker will use its namespace to search for the required image 

1- change the tag (name) 
2- docker.io is not mandatory aslong as we are pushing into    docker hub

docker tag getting-started:latest username/getting-started:latest 
--> renamed using docker tag or by simply rebuilding the image but it takes more time 

docker push username/getting-started:latest

docker pull username/getting-started:latest

run the image and test it 
docker run -d -p 3000:3000 image-name 

any other platform except for docker its like github we go and create a repo on the platform and create a repo and use it to push our image like in red-hat quay

docker login quay.io

**docker tag username/getting-started:latest**
**quay.io\/username/getting-started:latest**

**push quay.io\/username/getting-started:latest**

we may use another repositories in order for better integration when using tool like open shift so quay.io will offer better integration 
same as gitlab and github



https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image/

--------------------------section 4------------------------
##########################video-14##############################

getting-started-app on docker github repo we need to fork it and clone the repo that we now own to use it in our pipeline 


1- getting-started-app -> direct.
2- .github/workflows -> sub-directory. this is how github understands that i want to create a pipeline workflow its a must !! for github to understand that i want a pipeline to automate or execute commands on it
3- create a yml file under the workflows 
![[../7-References/Code/CICD pipeline/Docker+CI.html]]
```HTML
Go to [https://github.com/docker/getting-started-app](https://github.com/docker/getting-started-app)

Fork it

In the terminal, run:

git remote set-url origin https://github.com/abohmeed/getting-started-app.git

cat Dockerfile

Add the new file in VS Code:

# .github/workflows/docker-image.yml

name: Docker Image CI

on:

  push:

    branches:

      - main

  pull_request:

    branches:

      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

    - name: Checkout code

      uses: actions/checkout@v3

    - name: Set up Docker Buildx

      uses: docker/setup-buildx-action@v3

    - name: Log in to GitHub Container Registry

      uses: docker/login-action@v3

      with:

        registry: ghcr.io

        username: ${{ github.repository_owner }}

        password: ${{ secrets.GITHUB_TOKEN }}

    - name: Build and push Docker image

      uses: docker/build-push-action@v5

      with:

        context: .

        push: true

        tags: |

          ghcr.io/${{ github.repository_owner }}/abohmeed/getting-started:latest

          ghcr.io/${{ github.repository_owner }}/abohmeed/getting-started:${{ github.sha }}
```

git add -A
git commit -m ""
git push --> using ssh authentication easier 

best practice in docker is to avoid using latest as version tag because we might be lost if multiple occurs.. 

##########################video-15##############################

running docker images on a cloud service called elastic beanstalk its a platform as a service 

cloud providers has 3 types of services:

IaaS 
Paas
Saas 

##########################video-16##############################

docker compose used to host docker container without the need for docker run or port forwarding just as we did in AWS beanstalk 

We will something similar to PaaS we will multiple docker container locally without needing to connect them or even use docker run through whats called docker compose 

Its (docker compose) a pool written in python to deal with micro-service application

the problem is how will the container communicate internally for micro-services like database and how and which containers will be able to communicate with the outside world, Docker compose can handle all of that through making networks volumes all is configured through yml file and docker compose will run it, its not exactly a Paas like beanstalk but very similar to it so we can do all of the above without writing even one docker command.... 

We will work on a Microservice weather application 
Authentication service (GO) --> so the user needs login  
Database used (MySQL) --> we can use any SQL Database 
UI service --> html and CSS 
weather service --> retrieve the weather data using 
OPEN-weather API

Imagine making a VM for each service total shit show !! .

Multi-stage build is used in Go docker file and the reason for that is to minimize my image size and that what makes me Batman of Docker 

Multi-stage docker: Best practices 
from is what defines the base image 
we use **from** twice, Go is a compiled language so we take the binary which is the output of the build from the first container and **just add the artifact** to the **2nd image** so the 1st image is just a buffer for building so we were able to discard all the build tools that would have been only used once, thats the 1st catch and the 2nd is security wise is better since less tools less vulnerabilities  


docker compose is a python application so can use 
pip 
apt 
yum 
brew 

vim docker-compose.yml --> default name use by docker compose

docker compose will deal with the container as a service .. 


![[../../4-References/Code/docker-compose/Docker+compose.html]]

```html
Clone the weather app from GitLab:

git clone https://gitlab.com/abohmeed/moderndevops-weatherapp.git

Install docker-compose:

brew install docker-compose

Create the `docker-compose.yaml` file as follows:

services:

  auth:

    restart: always  --> optional, here it states on undefined action  
     do an automatic restart		

    build: ./auth   

    depends_on:

      - db

    environment: 

      DB_HOST: db

      DB_USER: root

      DB_PASSWORD: my-secret-pw

      DB_NAME: authdb

    networks:

      - app-net -> bridge network so container could commincate by name which is the service name 

  ui:

    restart: always

    build: ./UI

    depends_on:

      - auth

      - weather

    environment:

      AUTH_HOST: auth

      AUTH_PORT: 8080

      WEATHER_HOST: weather

      WEATHER_PORT: 5000

    ports:

      - "3000:3000"

    networks:

      - app-net

  weather:

    restart: always

    build: ./weather

    environment:

      APIKEY: 6d92c50bdamsh81137f3b87ace1fp1d53eejsnfe818b9dbc83

    networks:

      - app-net

  db:

    restart: always

    image: mysql:8.0.25

    environment:

      MYSQL_ROOT_PASSWORD: my-secret-pw --> when database starts for the first time it must be configured with a password

      MYSQL_DATABASE: authdb

    networks:

      - app-net

    volumes:

      - ./db-data:/var/lib/mysql

networks:

  app-net:

    driver: bridge

volumes:

  db-data:

Run the file:

docker-compose up -d  --> -d in detach mode if its in foreground the terminal will be flooded with logs of the yml command execution by default as we said the docker-compase looks for a file called 
------- docker-compose.yml ---------- in the project working directory
running this command more than once is completely fine if a service is already up its just passes to the next step in the build

docker logs --> to print the logs if there is a problem or if a container fails sometime port mapping could cause a problem when conflicts happens to multiple containers listening on the same mapped port

Show the status

docker-compose ps

Bring the application down:

docker-compose down --> delete and removes everything the docker-compose created
```

security best practice in docker compose 
is to put the authentication which user names and passwords and api keys in environment variables instead of plain text so instead of exporting every environment variable we can create

vim .env --> docker compose recognize this file when created within the the project directory this file is added to .gitignore 

![[../../Attachments/Screenshot from 2025-04-13 00-37-38.png]]

![[../../Attachments/Screenshot from 2025-04-13 00-38-19.png]]





how does docker compose build the yml file is it sequential i don't think so why is that ??? 
because we used and stated the network and volumes that where defined at the end of the file so it must have another approach ??????????


