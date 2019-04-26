---
layout: post
title: "Docker From Scratch Part 4: Docker-Compose"
---

_Final Step in the Docker From Scratch Project! Time to add in some Docker-Compose, quick guide to adding Docker-Compose to a Docker project_

## What've we got?

So far we have:

- Created an App in [Part 2]()
- Containerised our App in [Part 3]()

Now it's time to put the containerised applications into Docker-Compose!

You can follow this along without having read the previous, all you need are your applications and their accompanying Dockerfiles. If you don't have that, then check out the previous posts!

## What do we do now?!

Well, hopefully you have the five minutes it'll take us to get this done! Might sound like I'm underestimating the time this takes. But no, really, it's that easy. 

What we're doing now is we're going to be adding in Docker-Compose to the mix, and what this means is that we'll be running all our containers under the same deployment, building them and running them with one command. 

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

_Feel free to message me at @fletchergallop on Twitter for any questions or comments! - Thanks!_