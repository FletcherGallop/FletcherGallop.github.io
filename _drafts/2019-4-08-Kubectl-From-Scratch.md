---
layout: post
title: "Doing the Kubectl"
---

_Moving from Docker to Kubernetes_

### Introduction: Kubernetes

This was another straightforward decision for me. Once you have a Docker application it's a natural next step to move to orchestrating that.

There are several choices when it comes to container orchestration, with most platforms offering similar tools. 

The major player in the game right now though, is *Kubernetes*! With the runner up being Docker Swarm. Read more about which is right for you [here](https://medium.freecodecamp.org/how-to-choose-the-right-container-orchestration-and-how-to-deploy-it-41844021c241) in an article by FreeCodeCamp.

| Platform | Tool |
|:---------|-----:|
| AWS      | EKS  |
| GCP      | GKE  |
| Azure    | AKS  |

### What happened to Docker?

I'm not moving away from Docker, Kubernetes is a next step. I'm currently working towards my GCP Cloud Engineer Certification. More because I think certifications are a good marker or milestone. 
To do a Google Cloud certification you need to know a bit about kubernetes, it's a Google Cloud mainstay. 

### Why use Kubernetes?
Kubernetes is an orchestration tool, what this means is that you can bring things like auto-scaling to containers. Kubernetes has a few main concepts you need to know:

- Pod
- Deployment
- Service

### Working with Kubernetes and Docker

To put your Docker application into Kubernetes it's nice and straight forward. I've been working on a few labs for this now, so I thought I'd boil it down to a few commands for you!

I worked this lab using Google Cloud shell, a nifty tool given to you for free by Google Cloud Platform - of course, anything you make with it may have charges!

### NodeJS Container in Kubernetes with Google Kubernetes Engine

#### 1. You need to build your container first!

```bash
docker build -t gcr.io/<project_id>/<image_name>:<version> .
```

_**Note:**_ Don't leave off the `.` that's what tells docker where to build.

What this command is doing is building the docker image from your dockerfile with the tag you've given it. 

#### 2. Docker and Google Container Registry

```bash
gcloud auth configure-docker
```

This changes the values in the the `config.json` in your `.docker` directory

#### 3. Publishing to GCR

```bash
docker push gcr.io/<project_id>/<image_name>:<version>
```

#### 4. Creating a Pod using Kubectl

```bash
kubectl run <deployment-name> \
--image=gcr.io/<project_id>/<image_name>:<version>
```

##### Helpful Commands

```bash
kubectl get deployments
```

```bash
kubectl get pod
```

#### 5. Exposing your pod to External Traffic

```bash
kubectl expose deployment <deployment-name> \
--name=<deployment_name> \
--type=LoadBalancer \
--port=80 \ 
--target-port=8080
```

```bash
kubectl get svc <deployment-name>
```

#### 6. And don't forget to _Clean Up_

```bash
kubectl delete deployment <deployment-name>
```
_This deletes the deployment_

```bash
gcloud container clusters delete <cluster-name>
```

_**Note: Only run the command below if you want to delete EVERYTHING.**_
I created a Project just for this lab, and I suggest you do too. If you have other resources in this project or on the machine you are using, I highly recommend **against** running this command. 
```bash
kubectl delete services,pods --all
```

Otherwise use: 
```bash
kubectl delete services,pods name=<deployment-name>
```

