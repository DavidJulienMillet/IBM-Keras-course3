# Docker configuration for IBM courses

## Install docker and docker compose for ubuntu

Install curl

```sudo apt update && sudo apt upgrade```

```sudo apt install curl```

Install docker 

```sudo apt-get remove docker docker-engine docker.io containerd runc```

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - ```

``` 
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable" 
```

Install the docker engine

``` sudo apt-get update ```

``` sudo apt-get install docker-ce docker-ce-cli containerd.io ```

Install docker compose

```sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose ```

``` sudo chmod +x /usr/local/bin/docker-compose```

## Architecture

```
IBM
|-- readme.md
|-- docker-compose.yml
|-- docker_entrypoints
|-- |-- jupyter_entrypoint.sh
|-- docker_passwords
|-- |-- jupyter_password.txt
|-- dockerfiles
|-- |-- jupyter_dockerfile

|-- docker_volumes
|-- |-- course3
|-- |-- |-- requirements.txt
|-- |-- |-- venv/
|-- |-- |-- notebooks
|-- |-- course4
|-- |-- |-- requirements.txt
|-- |-- |-- venv/
|-- |-- |-- notebooks
```

## Launch the notebook

Change the file IBM/docker_passwords/jupyter_password.txt.example to jupyter_password.txt, changing the password you want for jupyter token.

Run command with cdcker compose

``` docker-compose up -d ```

Stop and remove the container with

``` docker-compose down ``` 


or directly with docker run

``` 
sudo docker run \
--rm \
--volume ~/Desktop/IBM/docker_passwords/jupyter_password.txt:/run/secrets/sec_jupyter \
--volume ~/Desktop/IBM/docker_volumes/course3:/project \
--name cont_ibm3 -d \
--env CONT_PORT=8883 \
--publish 8883:8883 \
img_ibm_jupyter
```
and stop and remove the container with

``` sudo docker stop cont_ibm3 ``` 

## Access the notebook

Access notebook of the course 2 concerning spark through the browser address
localhost:8882

Access notebook of the course 3 concerning keras through the browser address
localhost:8883

Access notebook of the course 4 concerning pytorch through the browser address
localhost:8884

Access notebook of the course 5 concerning tensorflow through the browser address
localhost:8885

And make identification with the password you wrote in
IBM/docker_passwords/jupyter_password.txt

