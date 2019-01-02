# docker-nginx-simple
Simplest possible Nginx webserver running on top of Alpine Linux in a container

[Nginx](http://nginx.org) is a powerfull web server.

This container may be used to deliver static content only.

# Building the container

Clone this repository, go into the directory and run a command like: `docker build --tag nginx-simple .`

One can also use the docker-compose.yml file provided here: `docker-compose build`

# Using the container

## Normal usage

Use a command like this one:

  `docker run --detach --rm=true --volumes ./wwwroot/:/var/www/ --name=nginx --hostname=nginx nginx-simple`

Or use docker-compose:

  `docker-compose up -d`

## Debugging

Use a command like this one:

  `docker run -it --rm=true --volumes ./wwwroot/:/var/www/ --name=nginx --hostname=nginx --entrypoint=sh nginx-simple`

Or use docker-compose:

  `docker-compose up`

  -------------------------
  Additions - docker-compose.yaml, individual k8s artifact files created and updated with mix and match of kompose
  Image in deployment created from local private docker registry
  Purpose - To facilitate nfs storage for pv and pvcs with secured access to apis through https load balancer
  Update completed - nfs storage
   In minikube nfs mount only available if same is mounted from host to guest in say VirtualBox
   Redundant file k8sdeployment.yaml

  Once minikube is up and host:guest contains a folder mapping through VBox, configure nginx-pv.yaml
  kubectl create -f nginx-pv.yaml -f nginx-pvc.yaml -f nginx-deployment.yaml -f nginx-service.yaml
  Get cluster ip from kubectl cluster-info and nodeport of nginx service from kubectl get service
  In browser access cluster-ip:<nginx node port> to demonstrate it

  Update coming up - nginx over ssl and basic self signed certificate creation

  Troubleshoot
  -------------
  Troubleshoot nfs mount options in pv
rpcinfo 127.0.0.1 |egrep "service|nfs"
https://unix.stackexchange.com/questions/205529/nfs-mount-nfs-protocol-not-supported
