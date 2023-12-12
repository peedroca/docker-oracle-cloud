# docker-oracle-cloud
Let's create a simples REST API using Docker, Oracle Cloud Instance with Ubuntu OS and Autonomous Database.

## Accessing VM on Oracle Cloud

1. Elevate permissions of private key with `chmod 400 <key_name>.key`
2. Use SSH to enter on CLI of VM with `ssh -i <key_name>.key <username>@<public_ip>`

## Generating docker image

1. On root folder, create the image running:
```
docker build -t sampleapi -f docker/Dockerfile backend/sampleapi/
```
2. Run container with
```
docker run -d -p 80:80 --name sampleapi sampleapi
```
