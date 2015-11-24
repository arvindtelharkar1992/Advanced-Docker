# Advanced-Docker

## 1. Socat for File I/O
The Dockerfiles under image1 and image2 folders contain the composition and cconfiguration details of the images which will be used in spinning up the linked containers.The names of the containers would be container1 and container2.
The following are the commands for spinning up container1:
```
docker build -t image1 .
docker run -idt --name container1 image1
```
The following are the commands for spinning up container2:
```
docker build -t image2 .
docker run -it --link container1:aliascontainer --name container2 image2
```
Note that image1 and image2 here are the names of the images and not the folders(as here)
After running container2, the message 'Hello message from arvind' should be visible

## 2. Ambassador Pattern
Two Digital Ocean Droplets(remote instances) have been used for this purpose. One of the instances has the docker-compose file under AmbassadorServer while the other has the docker-compose file under AmbassadorClient.
The Structure of the client and the server is as follows:
Server: There is a redis server and a redisAmbassador which are linked to each other.
Client: There is a redis client and a redisAmbassador which are also linked to each other.
Additionally, both the redisAmbassadors are linked to each other for which the IP address and port of one of the instances has been specified while creating the link.

Note: Please ensure that docker-compose is installed on both the instances.

For running the server, the following command needs to be executed:
```
docker-compose up
```
Running the above command will start the redis server on port 6379 of the first instance.

Now login to the second instance and run the following command to run the client:
```
docker-compose run myRedisClient
```
This will give a redis prompt from where you can set/get keys such as
```
>set mykey arvind
```
Now you can open the redis-cli on the first instance where the redis-server is running and 'get' the value
```
>get mykey
```

This should give "arvind" as the output

## 3. Blue Green Deployment

In addition to the deployment workshop, a post-receive hook has been added for green.git and blue.git for deploying the 
dockerized node.js app given. The post-receive hook will then appropriately build the image from the Dockerfile, push to the local registery, pull from registery , stop and restart the App. The changes made and pushed to the green or blue slice can be checked using curl command. Note that forever also needs to be installed globally to complete this process..
In short, the steps can be summarized as follows:
- Make a commit to the App folder
- push the change either to green or blue.
- Keep running the infrastructure file using
```
nodejs infrastructure.js
```





[ScreenCast:Advanced Docker](https://www.youtube.com/watch?v=2m7GGcp5Aug)
