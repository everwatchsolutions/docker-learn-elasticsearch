# Learning Elasticsearch
## Intro

This project uses Docker and Docker Compose to launch you into an environment with spark locally installed and some data prepopulated.

## Install software

### mac
1. install Docker (http://docs.docker.com/mac/started/)

### homebrew (mac)
1. brew install docker-machine
1. brew install docker
1. brew install docker-compose
1. docker-machine create --driver virtualbox learn-elasticsearch
1. docker-machine env learn-elasticsearch
1. eval "$(docker-machine env learn-elasticsearch)"
1. export DOCKER_CERT_PATH=$HOME/.docker/machine/machines/learn-elasticsearch
1. export DOCKER_MACHINE_NAME=learn-elasticsearch


## Running it with compose ...
from the project directory.  The build will take a long time...

1. docker-compose up

