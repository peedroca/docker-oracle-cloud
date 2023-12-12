# Docker on Oracle Cloud Plataform
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

## Deploy API on VM

1. Firstly, download you code on VM to create the image locally. I will use git for clone this repo on Oracle VM typing `git clone https://github.com/peedroca/docker-oracle-cloud.git` 
2. Go to cloned repo with `cd docker-oracle-cloud`, and than I will run the code above to generate and run my container. Maybe you need execute the command with sudo permission like: `sudo docker build ...`
3. I can test the container execution just typing `curl http://localhost/WeatherForecast`

## Open port to access API outside of VM

1. On cloud platform go to Instances > Primary VNIC > Subnet > Security Lists. 
2. Add an Ingress Rules with configuration:
```
{
    "Stateless": false,
    "Source Type": "CIDR",
    "Source CIDR": "0.0.0.0/0",
    "IP Protocol": "TCP",
    "Source Port Range": "All",
    "Destination Port Range": "80",
    "Description": "Sample API"
}
```
3. Test using the Public IP like `http://<public_ip>/WeatherForecast`.
