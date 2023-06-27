### Step 1
Lets create index.js file which contains the nodejs code for our static app
```
 // content of index.js
const http = require('http');
const port = 3030;
const requestHandler = (request, response) => {
  console.log(request.url);
  response.end('Hello Node.js Server!');
};
const server = http.createServer(requestHandler);
server.listen(port, (err) => {
  if (err) { return console.log('something bad happened', err); }
  console.log(`server is listening on ${port}`);
});
```

### Step 2 
Install node.js on your server 
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install npm
```

### Step 3
Now we test locally if our node app is working correctly. First we get package.json file by running npm init command. Then we get express server and finally we start 
our node app. The node express server will be running on localhost:3030 so we take another session of vm and curl localjost:3030

```
npm init
npm install express
node index.js
```

### Step 4
Lets setup the Dockerfile
```
FROM node:14.17.0-alpine
WORKDIR /app
ADD package*.json ./
RUN npm install
ADD index.js ./
CMD [ "node", "index.js"]
```

### Step 5
Lets build image of our application and then tag it as per docker hub standard so we can push it to docker hub repo
```
docker build -t docker-node-express-app:1.1 .
docker tag docker-node-express-app:1.1 pmunot11/docker-node-express-app:1.1
docker push pmunot11/docker-node-express-app:1.1
```

### Step 6
Finally lets test the image we built by actually running a container 
```
docker -d -p 3030:3030 run pmunot11/docker-node-express-app:1.1
curl localhost:3030
```











