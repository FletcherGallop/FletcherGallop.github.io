---
layout: post
title: "Docker From Scratch Part 2: Making the Sample App"
---

_Building a basic ReactJS + NodeJS API Server + PostgreSQL Database application ready for Docker! And some lessons I learnt along the way._

## Introduction

Next step in my Docker learning journey was to actually <strong>build</strong> the application I was going to Docker-ise!

Without an application, it was just me reading and regurgitating documentation and things I'd read. There's no better way to learn than by doing. 

I'm familiar with using ReactJS and so I thought this would be a good framework to build my application with, I also had a NodeJS backend Express server. Final component was the database, my supportive manager suggested that I use a PostgreSQL database. 

## Getting Started

If you want to follow my lead on this I'll be adding in code snippets so you can run it yourself. 

The point of this project was to do things from scratch, hence the title. 

### Why did I make an app when I could have just found one online?

There were reasons to this - such as the added learning both myself and my manager would gain by going it the long way. 

Including the fact that I hadn't done much databasing before. My idea of using a database was mostly limited to AWS Managed Services such as DynamoDB and Athena (which is SQL, but just two queries). 

So according to my experience so far, interacting with a database is more about using an API than it is about querying. 

Though, I did soon fix that by making my API server to talk to the PostreSQL server. 

## React UI

I started with the React front end, I'm more familiar with React than any other technologies in this space, unless you want to include Mobile Development. 

There is a lot in this space, but I use, [`create-react-app`](https://github.com/facebook/create-react-app) to bootstrap my react applications. 

`create-react-app` is a node package, follow the install instructions on the page.

Or use 

```bash
npx create-react-app my-app
```

### npx vs npm

**npm** - Is the package manager, so when you run something like `npm start` that is running a script as dictated by your config file. Or you can use it to install packages etc.

**npx** - Is a node runner, so whether you have the package installed or not, this will pull down the package and run it, then toss it when it's done. 

### Building up your UI

I didn't spend too much time in this space, I wanted an app that basically just gave me buttons and forms to interact with my APIs. 

There are many places to look for guides to doing this. 

But remember that for React, you want to separate different layers into different files. If you application gets complex, I'd recommend looking at something like [redux](https://redux.js.org/basics/usage-with-react). It helps you separate your front end into the MVC model.

## Node Express Server

For a Node Express server I use `npm init`, then do the rest myself. Express servers are easy to get started, they become more tricky as you increase the complexity of the application.

### Separate Your Routes From Your Server!

When you're starting to build your node server, it'll be easier at first to have everything in the one file. But after a certain size you'll soon regret that. 

I recommend splitting into something like the following:

```
.
+-- server.js
+-- routes/
|   +-- misc.js
|   +-- users.js
+-- package.json
```

Then in your `server.js` you'll have something like:
```javascript
app.get('/', misc.root);
app.get('/health', misc.health);
//Get all users ordered by id
app.get('/users', users.get_users);
```

In `routes/misc.js`: 
```javascript
module.exports = {
    root: function(req, res) {
        return res.json({info: 'NodeJS with Postgres API'})
    },
    health: function(req, res) {
        res.json({info: 'NodeJS with Postgres API - Health Check - Under Construction', status: 'UNDER_CONSTRUCTION'})
    }
}
```


### Use a Watcher or Hot Reloader
This is essentially just live reloading the server application, helpful when in development. Means when you fix that bug, it reloads those changes on your server so you don't then spend another 20 minutes try to fix a bug you've alread fixed!

Recommended:
```bash
npx nodemon server.js
```

## PostgreSQL
To use PostgreSQL you'll need both a client and a server to run it locally. 

1. Download [PostgreSQL](https://www.postgresql.org/download/)
2. Choose a PostgreSQL app, I've used [PSequel](http://www.psequel.com/)

Once you've got those, start PostgreSQL, on MacOS it'll be in the top right hand of your screen in the menu bar. 

Then use PSequel or some other client to interact. Have a go at creating tables and data. 

There are more tutorials on this elsewhere to get you going with PostgreSQL. 

## DONE!

So, now we're created:

1. React Application using `npm create-react-app`
2. Node Express Server using `npm init` 
3. PostgreSQL Database using chosen client

Follow me into the [next blog](https://fletchergallop.github.io/Docker-From-Scratch-Part3/) where I'll talk about docker-ising these apps!

_Feel free to message me at my social media accounts for any questions or comments! - Thanks!_