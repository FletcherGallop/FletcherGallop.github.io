---
layout: post
title: "A Quick Guide to: Kubernetes Concepts"
---
_A quick guide to the difference in key Kubernetes objects/concepts such as Deployment, DæmonSets and StatefulSets._

## New to Kubernetes?
Kubernetes is container orchestration, it's a good tool to use to deploy your containers and run deployments that scale and have different behaviours and dependencies. 

But, when you're starting out as I have, then it's hard to find documentation that isn't full of jargon. Reading the Kubernetes official documentation confused and frustrated me. Reading community blogs and guides gave me nothing but the process on how to replicate their work exactly. Nothing I found was breaking down to a level that I could understand. 

I've done a few projects with containers now, and if you read any of my other posts you can read about that adventure. I'm new to this, so I don't claim to be entirely correct. The purpose of this guide is to give you a human-readable, beginners guide to the key objects and concepts in Kubernetes.

Writing this has also pushed me to widen my understanding of the concepts and how they connect. 

### Cluster
This is what Google calls a grouping of Nodes, it runs on a compute engine, if deploying to GCP then it's an GCE host, if it's AWS then you'll be running on EC2 under the covers. 

Maybe that's too much jargon. 

Let's break it down further. 

A Cluster is a collection of machines that then run your Kubernetes objects. They are used as a collection, this means you can do scaling and other helpful things. 

### Node


### Pod

### Deployment
A deployment is 

### DæmonSet

### ReplicaSet

### StatefulSet

### PersistentVolume / Claim


