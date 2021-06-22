# Ravn-Challenge-Backend-JuanAyquipa

# Ravn Challenge Backend

## Description

Simple API endpoint that optionally accepts an author’s name and returns a JSON.

## Table of Contents
- [Environment Variable](#environment-variable)
- [Challenge Resolution](#challenge-resolution)

## Environment Variable


<center>

| Environment Variable Key  | Environment Variable Value         |
| ------------------------- | ---------------------------------- |
| PORT                      | 3000                               |
| API_PREFIX                | api/count                          |
| ORM_CONNECTION            | mysql                              |
| ORM_HOST                  | localhost                          |
| ORM_USERNAME              | [Your DB Username]                 |
| ORM_PASSWORD              | [Your DB Password]                 |
| ORM_PORT                  | 3306                               |
| ORM_DATABASE              | postgres                           |
| ORM_TEST_DATABASE         | test                               |
| ORM_SCHEMA                | public                             |

</center>



## The challenge Resolution

### Part 1: SQL

1. Who are the first 10 authors ordered by date_of_birth?

```
SELECT * FROM authors ORDER BY date_of_birth LIMIT 10;
```

This SQL order the records by date_of_birth ascending by default. 

### Part 2: Basic API Endpoint

The endpoint can be found in `/api/count/all`. The API was developed in NodeJS using express.

### Part 3: API Performance

none

### Part 4: Build Docker Container and steps to deploy.

Provide a written guide on how you would build the docker image and deploy this to DockerHub.

#### Building the Docker Image:

Create a Dockerfile with the following code:

```
FROM node:12.18-alpine
ENV NODE_ENV=production
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent && mv node_modules ../
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

Once you have the Dockerfile created, you can build a container image of the API with the following command:

```
docker build -t ravn-challenge-backend .
```

- `-t ravn-challenge-backend` defines the tag of the container.
- `.` is the location of the Dockerfile.

In order to upload the container image to DockerHub, you first have to create a Docker Id, in case you don't have one. Once you have your Docker Id, you can log in to your terminal using the following command:

```
docker login
```

Images uploaded to Docker Hub must have this format: `username/image:tag`. So let's rename our image using the following command:

```
docker tag ravn-challenge <username>/ravn-challenge-backend:1.0.0
```

Now we can upload the image to DockerHub:

```
docker push <username>/ravn-challenge-backend:1.0.0
```

You can found the public image of this challenge in this URL: https://hub.docker.com/repository/docker/devcrecedigital/ravn-challenge-backend

