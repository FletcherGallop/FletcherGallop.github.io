---
layout: post
title: "Docker From Scratch Part 4: Docker Compose"
---

_Final Step in the Docker From Scratch Project! Time to add in some Docker Compose, quick guide to adding Docker Compose to a Docker project_

## What've we got?

So far we have:

- Created an App in [Part 2](/Docker-From-Scratch-Part2)
- Containerised our App in [Part 3](/Docker-From-Scratch-Part3)

Now it's time to put the containerised applications into Docker Compose!

You can follow this along without having read the previous, all you need are your applications and their accompanying Dockerfiles. If you don't have that, then check out the previous posts!

## What do we do now?!

Well, hopefully you have the five minutes it'll take us to get this done! Might sound like I'm underestimating the time this takes. But no, really, it's that easy. 

What we're doing now is we're going to be adding in Docker Compose to the mix, and what this means is that we'll be running all our containers under the same deployment, building them and running them with one command. 

Previously we were running a command for each container, now we're going to be constructing a `docker-compose.yml` file. 

We made three apps in the previous posts, react-app, api-server and used a postgres image from DockerHub. And that's what I'll be using in this post too, so depending on your containers you'll have to edit accordingly. 

Our commands:

#### React App
```bash
docker build -t react-app .
docker run -p 3000:3000 react-app
```

#### API Server
```bash
docker build -t api-server .
docker run -d -p 3000:3000 api-server
```

#### Postgres

```bash
docker pull sameersbn/postgresql:10-1
docker run --name postgresql -itd --restart always \
 --env 'PG_TRUST_LOCALNET=true' \
 --env 'DB_NAME=<DB_NAME>' \
 --env 'DB_USER=<DB_USER>' \
 --env 'DB_PASS=<DB_PASSWORD>' \
 --publish 5432:5432 sameersbn/postgresql:10-1
```

Now, to put them in `docker-compose.yml`:

```yml
version: '3'
services:
  react:
    build: ./react-app
    ports:
     - "3000:3000"
    environment:
     - REACT_APP_API_URL=http://localhost:8000
  api:
    build: ./postgres-api
    ports: 
     - "8000:8000"
  postgres:
    image: "sameersbn/postgresql:10-1"
    ports: 
     - "5432:5432"
    environment: 
     - DB_USER=<DB_USER>
     - DB_NAME=<DB_NAME>
     - DB_PASS=<DB_PASSWORD>
```

### Breaking it Down 

`version: '3'` - This is just the docker-compose version we are using. Version 3 is the latest version at the time of writing this.

`services` - These are the different containers we will be deploying, given as an array of service objects. 

`react` service: 
```yaml
react:
    build: ./react-app
    ports:
     - "3000:3000"
    environment:
     - REACT_APP_API_URL=http://localhost:8000
```

What's going on here? Well, we have a `build` section which is telling Docker Compose that in the `./react-app` directory there is a Dockerfile it needs to build. 

Next, we have a `ports` section, this is a list of all the port mappings you need in this service. As we did when we ran `docker run -p 3000:3000 react-app` we need to specify the port that's exposed and used by the react app service. 

Then, finally, we have the `environment` section, this is where you can give Docker Compose the different environment variables you use in this service. In the case of the React UI we made, this is just the URL for the API server.   

`api` service:
```yaml
api:
    build: ./postgres-api
    ports: 
     - "8000:8000"
```

The `api` service is nice and straightforward, we build from the Dockerfile in the `./postgres-api` directory, then we map the port `"8000:8000"`, the port the server runs on.  

`postgres` service:
```yaml
postgres:
    image: "sameersbn/postgresql:10-1"
    ports: 
     - "5432:5432"
    environment: 
     - DB_USER=<DB_USER>
     - DB_NAME=<DB_NAME>
     - DB_PASS=<DB_PASSWORD>
```

This one is a little different to the other two, it isn't using `build` it uses `image` instead. This just means that instead of using a Dockerfile we've made it's going to use a Docker image from DockerHub.  

But like the others, we also have here port mapping `"5432:5432"` and environment variables, `DB_USER, DB_NAME` and `DB_PASS`. 

## Making the Docker Compose Happen

Now that we have our `docker-compose.yml` file, all we need to do is run `docker-compose build` and `docker-compose up` to run it all!

If you installed Docker Desktop or Docker Toolbox then you will already have Docker Compose installed. 

So in your terminal, go to the location of your `docker-compose.yml` file, then run:

```bash
docker-compose build && docker-compose up
```

This runs both commands, first `build` to build the deployment and then `up` to start it. Nice and simple!

What this means as well, is that now all your apps running in the same deployment will have their own "network". It's a fun benefit of using a tool like Docker Compose. But we can talk about that more another time. What it means for now is that the react app will be able to access the api server on `localhost`. 

## Cleaning Up

As usual for CLI applications, we can use `ctrl-c` to stop it running. Then, follow that with:

`docker-compose down` 

This will stop your containers, but it also removes the stopped containers as well as any networks created. There are other arguments you can add to this command such as `--rmi all` which will remove all images used by any services. Check out more [here](https://docs.docker.com/compose/reference/down/).

## And That's It!

We did it! We now have our docker containers running using Docker Compose! It all now happens with one file and one command. 

This also brings us to the end of the Docker From Scratch Series! I hope you enjoyed it and followed along! 

_Feel free to message me at @fletchergallop on Twitter for any questions, comments or suggestions! - Thanks!_