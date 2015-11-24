FROM ubuntu:latest
MAINTAINER adtelhar@ncsu.edu

# Create file and write to it
RUN touch myfile.txt && echo 'Hello message from arvind' > myfile.txt

# Update the system and install socat
RUN apt-get -y update && apt-get -y install socat

#Listen on port 9001
CMD socat TCP4-LISTEN:9001 SYSTEM:'cat myfile.txt'
