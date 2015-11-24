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
After running container2, the message 'Hello message from arvind' should be visible

## 2. Ambassador Pattern





[ScreenCast:Advanced Docker](https://www.youtube.com/watch?v=2m7GGcp5Aug)
