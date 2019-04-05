---
layout: post
title: "Docker From Scratch Part 1: Kick-Off"
---

_Started a new job, and with some time before the first full-time client engagement kicked off, what better to do than to learn some Docker! A brief summary of lessons learnt in professional project management._

### Introduction
I started my new job! About a month ago now. _But_, I joined earlier than expected, so what could I do but learn some new things? 

What did I pick? - *Docker*!

Why? - Because I'd always wanted to have a go, but had never found the right project that allowed for the extra time it would take to pick up Docker. 

I'm going to be telling you a bit about what I learnt about running projects successfully in a professional environment, and I hope you can learn from my lessons and follow me along through my next posts about the technical content. 

### Purpose of this Project
Docker From Scratch is all about me learning Docker, you guessed it, from scratch. 

There wasn't too much that I needed to do in order to get to the Docker part, or at least, that was my first impression. 

The goals of the project were:
    - To have a go at Docker-ising an application with multiple components
    - Build the application to Docker-ise. 

### Starting the Project
> The project was simple. It was to learn! Simple objective, right?

*WRONG!* First thing I learnt in my project was requirements are better defined earlier! This was something that I hadn't caught on to until later in the project, after the third or fourth changed "requirement" lead to even more scope creep. 

### Managing the Scope

This was an internal project my client was my manager, but regardless of that. They were a tough client. Throwing up new ideas and changing requirements. Adding in standards. 

When you have a client, you need to be able to stop them and hold them to their requirements. Things do sometimes change as you progress through but you should always be mindful of scope creep!

Scope creep is defined as "a dreaded thing that can happen on any project, wasting money, decreasing satisfaction, and causing the expected project value to not be met." (PMI, 2009)

### Estimates aren't for the Faint of Heart

Or rather, estimates are more about how much you know yourself and how much you know the task. 

I started with the brief that the project would be maybe a week, we had a week till the next client project kicked off. That would be all the time I had to play with Docker From Scratch. 

About two days in, after a day to build the app, and then look at databasing, and start to look into the API server. My manager asked me what my estimate would be now. 

We started a table on the whiteboard:

![Estimates](../images/estimates_whiteboard.jpg)

And then after a few back and forths we added that column on the far rigth - _certainty_. This was about how confident I felt in the accuracy of my estimate. 

> It's hard to know how long an activity takes before you've done it before. 

When we pushed paused on the Docker From Scratch project it had already taken longer than the 14 day worst case estimate. 

### Keep Track of What You're Learning

When you take on a learning project, make sure you keep track of what you're learning. If that's through commit messages, that's fine. But better still is to keep a local file - you can commit it too, but it's more for you than anyone else. As you're going along with your project, keep note of useful commands, websites (_if you remember_). But add in a bold heading with **"Key Learning Points"**, and under it, start a list, as you go along add in notes to self. 

In my project I had points like:
1.  _Git_ - Use `git remote prune origin` when suffering with dead references in origin.
2. REST APIs should return a representation of any object created when a POST method is used.
 
I'll go over the technical side to those learning points later in the _Docker From Scratch_ series.

### Bits and Pieces I Picked Up

Every project you run should be run like a professional project. This was a big thing that I think would have improved things significantly. Knowing the practices and putting them into action are two different things. But it is well worth it. 

- Getting your requirements nailed down early leads to better management of scope and limits potential scope creep.

- Estimates are helpful for timelining a project, but don't be afraid to put a bigger number than you think sounds right. It's better to deliver earlier than expected than later. So overbudgetting time is better then underbudgetting. 

- As technical people we're always learning and it's important to remember that, and to learn from experiences rather than beat yourself up for not being 100% from the start. Keep track of the things you learn along the way, that way, when you look back you can see all your improvements. 

- Failures aren't always failures. If something fails, take a step back, reflect, do a retrospective, and next time you come to the same situation you'll know what to do differently. That's the magic of _Continuous Improvement_.

### Next Up

I'll be writing up the technical aspects of this project next, so if you want to learn about what I did and how to learn Docker from Scratch follow along. 

___

#### Sources

1. [PMI Scope Creep](https://www.pmi.org/learning/library/top-five-causes-scope-creep-6675)
