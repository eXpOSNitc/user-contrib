## Docker based setup instructions for SIL NIT-C
### Install Docker

Follow instructions here to install Docker on host machine https://docs.docker.com/get-docker/
### Create Dockerfile
Dockerfile contains instructions on how to Docker will setup the container,

Create a folder, which will be mapped into the docker image

```    
    mkdir compilerlab
    cd compilerlab
```

Create a `Dockerfile` with following contents

```
FROM ubuntu:20.04

RUN apt-get update \
    && apt-get install -y bison flex libreadline-dev libc6-dev libfl-dev wget vim build-essential \
    && wget "https://silcnitc.github.io/files/xsm_expl.tar.gz" \
    && tar -xzf xsm_expl.tar.gz \
    && cd xsm_expl && make \
    && sed -i '1s/^/#!\/usr\/bin\/env bash \n/' /xsm_expl/xsm \
    && cd /xsm_expl/xfs-interface && ./init

WORKDIR /xsm_expl
```

The given Dockerfile installs the dependencis required for SILC on a base Ubuntu 20.04 container


Build the container image by running
```
    docker build -t silc:ubuntu20.04 .
```
### Start the container instance

Start an instance of Container and map the local folder into `files` directory inside the container
```
  # on linux
  docker run -v $PWD:/xsm_expl/files -d --name silc -i silc:ubuntu20.04 
  # on windows
  docker run -v %cd%:/xsm_expl/files -d --name silc -i silc:ubuntu20.04
  # on powershell
  docker run -v get-location:/xsm_expl/files -d --name silc -i silc:ubuntu20.04
```

### Connecting to the container
Connect to the container
```
  docker start silc
  docker exec -it silc /bin/bash
```
The usage instructions for the XSM simulator can be found here.
