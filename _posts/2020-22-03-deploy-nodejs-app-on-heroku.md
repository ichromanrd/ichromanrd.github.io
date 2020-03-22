---
layout: post
title: "Deploy Node.js Application on Heroku"
date: 2020-03-22 18:15:00 +7
comments: true
categories:
---

Just out of my curiousity, I want to learn how to create and deploy Node.js app on Heroku. Here's how it's done.

## Prepare the Node.js Application

Prerequiresites: have Node.js installed on your system. Mine using node version 13.9.0.

There are few sub-steps on this:

### Create the app directory and npm init.

```bash
$ mkdir simple-node-app && cd simple-node-app
$ npm init
```

The command prompt will give some questions on setting up the node app, just entering the information accordingly.

`package.json` file will be created. Add this on the script block, so we only use `npm start` to run the app,

```javasript
// ...
"scripts": {
	"start": "node index.js",
},
// ...
```

### Add Express.js

We want to build simple web service, add Express.js

```bash
$ npm install express --save
```

Then create `index.js` containing this:

```javascript
var express = require('express');
var app = express();

app.get('/', function(req, res) {
    res.send('Hello World');
});

app.get('/api/v1/student', function(req, res) {
    res.send(
        { id: 1, name: 'Ichroman Raditya Duwila' }
    );
});

app.listen(process.env.PORT || 3000, function() {
    console.log('Simple node app runs');
});
```

### Init Heroku App


Make sure heroku-cli installed, and then do login Heroku:

```bash
$ heroku login
```

Then init heroku app,

```bash
$ heroku create:apps {app_name}
```

### Commit and Push!

Do not create `.gitignore` file and add the node_modules entry otherwise it will be included on commit. We don't want it. All ready, git add, commit and push,

```bash
$ git add . && git commit -a -m 'initial commit' && git push heroku master
```

Heroku will build the app. You can verify the build by,

```bash
$ heroku logs --tail
```

You can open the app by,

```bash
$ heroku open
```

### Note!

When deploying to heroku we need to use heroku-defined port instead of specifying it ourselves. It can be seen in this line of code.

```javascript
.listen(process.env.PORT || 3000)
```

Reference: [Stackoverflow](https://stackoverflow.com/questions/15693192/heroku-node-js-error-web-process-failed-to-bind-to-port-within-60-seconds-of)



The codes in this post can be checked out in this [repo](https://github.com/ichromanrd/simple-heroku-nodejs-app). Cheers!