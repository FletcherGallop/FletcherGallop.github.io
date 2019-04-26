---
layout: post
title: "Docker From Scratch Part 3: Doing the Docker"
---

_Time to do the Docker!_

## Introduction 

In the [previous post](https://fletchergallop.github.io/Docker-From-Scratch-Part2/) we created a three part application using Node, ReactJS and PostgreSQL. 

Now it's time to Docker-ise! 

Docker makes everything so nice and straight forward. 

Putting the application into Docker was so straight-forward, and in no more than maybe 30 lines of code and a image from DockerHub I was up and running in Docker.

Docker have good documentation and getting started guides. There are also a lot of people in this space who publish blogs and guides!



These are the full Dockerfiles:

### `react-app.Dockerfile`
```yaml
FROM node:10-alpine

#Create app directory
WORKDIR /app

#Bundle app src
COPY . /app

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```
### `api-server.Dockerfile`
```yaml
FROM node:10-alpine

#Create app directory
WORKDIR /app

#Bundle app src
COPY . /app

RUN npm install

EXPOSE 8000

CMD ["npm", "start"]
```

For the PostgreSQL application I used an image from DockerHub: [sameersbn/postgresql](https://hub.docker.com/r/sameersbn/postgresql/)

To use this you include different environment variables when you run the container. (Commands given [below](#now-its-time-to-do-the-docker))

## Breaking it Down

### 1. Pick your base image

This is just as simple as knowing what your application needs to run. In my case, I had two node apps. So both were:

```yaml
FROM node:10-alpine
```

Essentially, this is saying, node version 10, alpine edition. Alpine is a Linux distribution. It's more lightweight than a full image, so you'll see `-alpine` a lot in Docker Projects. 

### 2. Create Working Directory
```yaml
#Create app directory
WORKDIR /app
```
From this point on, your container will be working from `/app`. Just like we do from the terminal (on MacOS), this is now our working directory.

### 3. Copy Source Files
```yaml
#Copy app source
COPY . /app
```
What we're doing here is just copying all the files in the current directory into the `/app` directory on the container. 
### 4. Install Dependencies
```yaml
#Install Dependencies
RUN npm install
```
This is just running `npm install` on the container, this means that you will now have your node package dependencies installed on the container! Simple as. 

### 5. Expose Port
```yaml
#Expose port for app
EXPOSE 3000
```
We need to expose a port to talk to our container! This means now that when we run this container if we go to https://localhost:3000/ we will see our react-app. 
### 6. Run!

```yaml
#Run the start command
CMD ["npm", "start"]
```

You'll notice that we used `RUN` and `CMD`, these look to be doing similar things. But there is a convention here. 

- **`RUN`**: is an image build step. It's not lost, so when we do it for `npm install` that means the container will keep those changes, ie, it'll keep the `node_modules/`
- **`CMD`**: is what the container will run on default when it is lauched. It can be overriden when starting the container. So, in our case it's `npm start`, but we could do something instead like `docker run api-server <some-other-command>`. 

## Now It's Time to Do the Docker!

### React App
```bash
docker build -t react-app .
docker run -p 3000:3000 react-app
```
This is firstly building the react-app from the Dockerfile, adding `-t react-app` gives it a helpful tag to use later. 

Then it's running the image as a container mapping up port `3000` on the container to the same port on my local machine. 

### API Server
```bash
docker build -t api-server .
docker run -d -p 3000:3000 api-server
```
Nothing you haven't seen before! 

### Postgres

```bash
docker pull sameersbn/postgresql:10-1
docker run --name postgresql -itd --restart always \
 --env 'PG_TRUST_LOCALNET=true' \
 --env 'DB_NAME=<DB_NAME>' \
 --env 'DB_USER=<DB_USER>' \
 --env 'DB_PASS=<DB_PASSWORD>' \
 --publish 5432:5432 sameersbn/postgresql:10-1
```

This runs the postgresql image from DockerHub with a few different environment variables. Giving it the database configuration variables, name, user and password is important. This now means that the container will make this database with the user credentials and it'll be ready for us to use! The username and password are also given to the api server to use (done in the local  `.env` file). 


## DONE!

So, now we're running our apps in Docker! 

Follow me into the [next blog](https://fletchergallop.github.io/Docker-From-Scratch-Part4/) where I'll talk about using Docker-Compose to run our apps together!

_Feel free to message me at @fletchergallop on Twitter for any questions or comments! - Thanks!_