---
layout:     post
title:      "MEAN Basic"
subtitle:   "MEAN Basic"
date:       2016-03-11 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# MEAN

MangoDB, ExpressJS, Angular, Node.js

 

## Setup express server

	mkdir mean-todo
	cd mean-todo
	mkdir src

	npm init

>package.json will be create which keeps third party node modules up to date, manage dependencies

make a dir named "public" to keep all the public resorses, like image 

	cd public

	git clone git@github.com/treehouse/angular-basics.git .

>The point at the end copy the content of this repo in the folder but not the angular-basics folder


Install Express

	npm install express --save-exact

>express is located in node_modules folder

Create app.js file 
	
	nano src/app.js

>Node will start the server with this file

Ignore node_modules

	echo 'node_modules' >> .gitignore

Set the app.js by adding the following code:

    'use strict';
    //to use express we need to require express
    var express = require('express');

    //create an instance of express server, this instance allow us to setup the server when we need
    var app = express();

    //specific the folder should read
    app.use('/', express.static('public'));

    //app listern to port 3000
    app.listen(3000, function(){
        console.log("server is running");
    })



Start the server by 

	node src/app.js



Other way to start the node server is using nodemon, it will automatcally restart the server when change occoured:

	npm install -g nodemon 

Start server 

	nodemon

check if server running by 

	localhost:3000



## Setup Express Routes

Add the foloowing code to app,js to get the data from server:

	
    'use strict';
    //to use express we need to require express
    var express = require('express');

    //create an instance of express server, this instance allow us to setup the server when we need
    var app = express();

    //app listern to port 3000
    app.listen(3000, function(){
        console.log("server is running");
    })

    //to handle multi routes
    var router= express.Router();


    //get todos
    router.get('/todos', function(req, res){
        res.json({todos:[]}});
    })


    //autoroute adding api prefix
    app.use('/api',router)



## Refactor api calls


src/app.js
    'use strict';
    //to use express we need to require express
    var express = require('express');
    var router =  require('./api');

    //create an instance of express server, this instance allow us to setup the server when we need
    var app = express();

    //app listern to port 3000
    app.listen(3000, function(){
        console.log("server is running");
    })


    //autoroute adding api prefix
    app.use('/api',router)


create src/api/index.js file:

    'use strict';
    var express = require('express');

    //to handle multi routes
    var router= express.Router();


    //get todos
    router.get('/todos', function(req, res){
        res.json({todos:[]}});
    });

    //POST
    //PUT
    //DELETE

