# play-with-docker

Play With Docker gives you the experience of having a free Alpine Linux Virtual Machine in the cloud
where you can build and run Docker containers and even create clusters with Docker features like Swarm Mode.

Under the hood DIND or Docker-in-Docker is used to give the effect of multiple VMs/PCs.

A live version is available at: http://play-with-docker.com/

## Requirements

Docker 1.13+ is required. You can use docker-machine with the following command:

```
docker-machine create -d virtualbox --virtualbox-boot2docker-url https://github.com/boot2docker/boot2docker/releases/download/v1.13.0-rc1/boot2docker.iso <name>
```

The docker daemon needs to run in swarm mode because PWD uses overlay attachable networks. For that
just run `docker swarm init`.

It's also necessary to manually load the IPVS kernel module because as swarms are created in `dind`, 
the daemon won't load it automatically. Run the following command for that purpose: `sudo lsmod xt_ipvs`

Notes:
* Docker for Mac not include docker 1.13 for now, you can build a new Docker environment with Docker Machine


## Installation

Start the Docker daemon on your machine and run `docker pull docker:1.12.2-rc2-dind`. 

1) Install go 1.7.1 with `brew` on Mac or through a package manager.

2) `go get`

3) `go build`

4) Run the binary produced as `play-with-docker`

5) Point to http://localhost:3000/ and click "New Instance"

You can build and run the project with docker:
1) `./build.sh`

2) `docker run -v /var/run/docker.sock:/var/run/docker.sock --name  -p3000:3000 -d franela/play-with-docker:latest`

Notes:

* There is a hard-coded limit to 5 Docker playgrounds per session. After 1 hour sessions are deleted.
* If you want to override the DIND version or image then set the environmental variable i.e.
  `DIND_IMAGE=docker:dind`

