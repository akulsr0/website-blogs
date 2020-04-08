## Node.js data caching with Redis

In this blog, we will make a demo application which fetches number of instagram followers of a user. And, we will cache that data using redis.

Before moving further, lets understand

### What is data caching?

Data caching is a way to store frequently used data or information in memory for fast access. Once the data is cached, it will come from memory instead of the server until the cached data is expired.

Lets build the application

First of all we need to install Redis

- Windows users can download and install Redis from [here](https://redis.io/download).
- Mac users can install it using homebrew

Installing Redis using Homebrew

    > brew install redis

After installing Redis, initialize the server by entering following command

> redis-server

Now, we need to create the actual application.

    cd Desktop
    mkdir nodejs-redis-caching
    cd nodejs-redis-caching
    npm init -y
    npm i express axios redis
    code .

After opening the project in VSCode or any editor. Create index.js

_nodejs-redis-caching/index.js_

    const express = require('express');
    const axios = require('axios');
    const redis = require('redis');

    const app = express();
    const client = redis.createClient(6379);

    app.listen(9000, () => {
        console.log('Server is running at port 9000');
    });

Now let's make a _GET Request_ at localhost:9000/username

_nodejs-redis-caching/index.js_

    app.get('/:username', (req, res) => {
        let { username } = req.params;
        axios
            .get(`https://www.instagram.com/${username}/?__a=1`)
            .then((result) => {
                let fc = result.data.graphql.user.edge_followed_by.count;
                client.setex(username, 3000, fc);
                res.send(`<h3>${username} has ${fc} followers.</h3>`);
            })
            .catch((err) => {
                res.json({ error: 'Server Error' });
            });
    });

In the above code, we are making a GET Request a localhost:9000/username route and fetching user's follower count, also were caching that data into redis. But we are not retrieving the cached data from memory.
To do so, we need to make a middleware function.

    function getCache(req, res, next) {
        let { username } = req.params;
        client.get(username, (err, result) => {
            if (err) {
                res.send('Server Error');
            }
            if (result !== null) {
                res.send(`<h3>${username} has ${result} followers.</h3>`);
            } else {
                next();
            }
        });
    }

Now we need to add this middleware into our main GET Request.

    app.get('/:username', getCache, (req, res) => {
        ...
    }

So, that's it. We have successfully cached the data and able to retrieve it from memory.

Let's quick jump onto the results.

### Results

#### Before Caching

![before-caching](https://user-images.githubusercontent.com/43666833/78834604-7a672e00-7a0c-11ea-8b84-c4f6db61689d.png)

#### After Caching

![after-caching](https://user-images.githubusercontent.com/43666833/78834904-e9dd1d80-7a0c-11ea-84ea-75699d6e1657.png)

Here is the link to [github repo](https://github.com/akulsr0/nodejs-redis-caching)
