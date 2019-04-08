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
<!-- I've worked this in the gcloud shell - so if you're not using gcloud shell, where I've got `$DEVSHELL_PROJECT_ID`, replace that with your google project ID. 
_Or, better yet, just do it in Google Cloud Shell_ -->

### NodeJS Container in Kubernetes with Google Kubernetes Engine

#### 1. You need to build your container first!

`docker build -t gcr.io/<project_id>/<image_name>:<version> .` 

_**Note:**_ Don't leave off the `.` that's what tells docker where to build.

What this command is doing is building the docker image from your dockerfile with the tag you've given it. 

#### 2. Docker and Google Container Registry

`gcloud auth configure-docker`

This changes the values in the the `config.json` in your `.docker` directory