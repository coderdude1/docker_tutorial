# General notes working thru the tutorial

# Overview goes here

# Services
added the docker-compose.yml

## Hierarchy of distributed services
* Stack
* Services
* Container

docker-compose.yml is used to configure the various runtime config options like
instant count, restart rules, network mapping, etc

Commands to create the services
    `docker swarm init`
    `docker stack deploy -c docker-compose.yml getstartedlab`
    `docker service ls`

In the default example settings, there is 5 containers, running the same image, on the same host
    Get the service id and name
    `docker service ls`

A single container running in a service is called a task. Tasks are given unique IDs that numerically increment, up to the number of replicas you defined in the docker-compose.yml
    lists the tasks for the service
    ` docker service ps getstartedlab_web`

Using curl or webrowser will show the container id that responded to the request.  Each invocation will have a different id, showing the load balancing
## Scaling
simply update the replica count in the docker-compose.yml file and run the following to update the currently running services 
    `docker stack deploy -c docker-compose.yml getstartedlab`

## SHutdown the swarm
take down the app
    `docker stack rm getstartedlab`

shutdown the swarm
    `docker swarm leave --force`

##TLDR
A service is a an image docker swarm manages for you. You might ask it to run three instances of this image, and docker swarm will do so (if it can).

A cluster is made up of nodes which are either workers (that run the services), or managers (control the scheduling of services across the nodes). Note that a node can be both a worker and a manager