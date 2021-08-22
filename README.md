![image](https://user-images.githubusercontent.com/14609656/130365730-d9a819ee-21bd-460d-acf7-234f212bb3bb.png)


https://www.youtube.com/watch?v=3c-iBn73dDE


## Run

mongo-express runs on
http://localhost:8080/

node app runs on
http://localhost:3000/


## Local flow
To test local flow, there's two ways:
### 1. node app on host, mongo + mongo-express on Docker

stop all containers

run node app
```
npm start
```

run mongo + mongo-express using docker-compose
```
docker-compose -f docker-compose.yaml up
```

### 2. all node app + mongo + mongo-express on Docker
- Node app image is in AWS ECR

stop all containers

run containers using docker-compose, this does the following:
- gets node app image from private container repo AWS ECR
- gets mongo and mongo-express from Dockerhub
- starts all of them in the same network
```
docker-compose -f mongo.yaml up
```

## Dev server flow

To test "dev server" flow,
stop all containers

start a new terminal

go to `docker_dev_server/`

login to AWS ECR
```
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 656985594497.dkr.ecr.us-east-2.amazonaws.com
```

run containers using docker-compose
```
docker-compose -f docker-compose.yaml up
```


## AWS ECR account
l******@live.com
password in LastPass

https://us-east-2.console.aws.amazon.com/ecr/repositories/private/656985594497/my-app?region=us-east-2


## UI flow for quick test

Mongo-express: http://localhost:8080/
- `user-account` db (create if not exist)
    - `users` collection (create if not exist)

UI: http://localhost:3000/
- edit fields, save

result:
-> new user must be on users collection

UI: Edit user and save
-> changes must be saved

To test volumes:
- restart containers (e.g. docker-compose down then up)
- `user-account` db, `users` collection, and created user must all exist
