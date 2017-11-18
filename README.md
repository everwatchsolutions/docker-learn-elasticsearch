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

### Using elasticsearch

#### Submit some documents to index

PUT http://**address**:9200/megacorp/employee/1

{
        "first_name" : "John",
        "last_name" :  "Smith",
		 "age" :        25,
        "about" :      "I love to go rock climbing",
        "interests": [ "sports", "music" ]
}

* megacorp is index name
* employee is type name
* 1 is the document id


PUT http://**address**:9200/megacorp/employee/2    {"first_name" : "Jane","last_name": "Smith","age" : 32,"about" : "I like to collect rock albums", "interests": [ "music" ]}PUT http://**address**:9200/megacorp/employee/3    {"first_name" : "Douglas","last_name": "Fir","age" : 35,"about": "I like to build cabinets", "interests": [ "forestry" ]}

#### View the documents in kibana

http://**address**:5601

* set the index that you want to view to megacorp
* view the data under the discover tab

#### Retreive a single document

GET http://**address**:9200/megacorp/employee/1

> {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "1",
> "_version": 5,
> "found": true,
> "_source": {
> "first_name": "John",
> "last_name": "Smith",
> "age": 25,
> "about": "I love to go rock climbing",
> "interests": [
>   "sports",
>   "music"
> ],
> }
> }

#### Search

GET http://**address**:9200/megacorp/employee/_search?q=last_name:Smith

> {
> "took": 6,
> "timed_out": false,
> "_shards": {
> "total": 5,
> "successful": 5,
> "skipped": 0,
> "failed": 0
> },
> "hits": {
> "total": 2,
> "max_score": 0.2876821,
> "hits": [
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "2",
> "_score": 0.2876821,
> "_source": {
> "first_name": "Jane",
> "last_name": "Smith",
> "age": 32,
> "about": "I like to collect rock albums",
> "interests": [
>   "music"
> ],
> }
> },
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "1",
> "_score": 0.2876821,
> "_source": {
> "first_name": "John",
> "last_name": "Smith",
> "age": 25,
> "about": "I love to go rock climbing",
> "interests": [
>   "sports",
>   "music"
> ],
> }
> }
> ],
> }
> }

#### Query DSL

POST http://**address**:9200/megacorp/employee/_search

 {
        "query" : {
            "match" : {
                "last_name" : "Smith"
            }
} }

> {
> "took": 6,
> "timed_out": false,
> "_shards": {
> "total": 5,
> "successful": 5,
> "skipped": 0,
> "failed": 0
> },
> "hits": {
> "total": 2,
> "max_score": 0.2876821,
> "hits": [
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "2",
> "_score": 0.2876821,
> "_source": {
> "first_name": "Jane",
> "last_name": "Smith",
> "age": 32,
> "about": "I like to collect rock albums",
> "interests": [
>   "music"
> ],
> }
> },
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "1",
> "_score": 0.2876821,
> "_source": {
> "first_name": "John",
> "last_name": "Smith",
> "age": 25,
> "about": "I love to go rock climbing",
> "interests": [
>   "sports",
>   "music"
> ],
> }
> }
> ],
> }
> } 

#### full text

POST http://**address**:9200/megacorp/employee/_search

{
        "query" : {
            "match" : {
                "about" : "rock climbing"
            }
} }


> {
> "took": 4,
> "timed_out": false,
> "_shards": {
> "total": 5,
> "successful": 5,
> "skipped": 0,
> "failed": 0
> },
> "hits": {
> "total": 2,
> "max_score": 0.53484553,
> "hits": [
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "1",
> "_score": 0.53484553,
> "_source": {
> "first_name": "John",
> "last_name": "Smith",
> "age": 25,
> "about": "I love to go rock climbing",
> "interests": [
>   "sports",
>   "music"
> ],
> }
> },
>   {
> "_index": "megacorp",
> "_type": "employee",
> "_id": "2",
> "_score": 0.26742277,
> "_source": {
> "first_name": "Jane",
> "last_name": "Smith",
> "age": 32,
> "about": "I like to collect rock albums",
> "interests": [
>   "music"
> ],
> }
> }
> ],
> }
> }




