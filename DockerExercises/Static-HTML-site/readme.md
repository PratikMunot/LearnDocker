### Step1
Create a static html page named as index.html as shown below
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker</title>
  <meta name="description" content="">
  <meta name="author" content="">
</head>
<body>
  <h2>Hello Pratik</h2> 
		<h4>-from Docker!</h4>
        <p>This is a static HTML page which is running on a <strong>docker</strong> container and Nginx server.</p>

</body>
</html>

```

### Step 2
Create a wrapper.sh file as shown below. This will be used to start the nginx server inside the container
```
#!/bin/bash

echo "Nginx is running..."

exec nginx -g "daemon off;"
```

### Step 3 
Create a Dockerfile as shown below. Dockerfile contains list of all instructions required to build the image.
```
FROM nginx

COPY wrapper.sh /

COPY html /usr/share/nginx/html

CMD ["./wrapper.sh"]
```

### Step 4
Now all the required files are ready. Lets build our image with following docker command
```
docker build -t dockerhtml:1.1 .
```
You can check if the image has been created successfully and whether it has proper tags by executing the command and checking the Tag column.
(Tags are must. Always create an image with correct tags which ill help you to push the image in repository)
```
docker images
```

### Step 5 
Once image is created, we run the container with that base image. 
```
docker run -d -p 8080:80 dockerhtml:1.1
```

### Step 6
Execute docker ps command to check if container is running. To check the output, open chrome browser and in url type - http://localhost:8080 
```
docker ps

# In linux use following comand to check the content of webpage
curl localhost:8080

```

### Step 7
Now we do tagging to our image again. This time we are doing because we need to follow naming convention of Docker hub.
```
docker tag dockerhtml:1.1 pmunot11/dockerhtml:1.1
docker images       # check if image tagged correctly
```

### Step 8
Now we login to docker hub and enter the credentials for authentication. And finally we push the image via cmd - docker push accountname/imagename:tag
```
docker login
docker push pmunot11/dockerhtml:1.1
```
Now we have successfully pushed our own application image to our public docker hub repo. If we want to run the container with our custom image we need to just run following command
```
docker run -d -p 8080:80 pmunot11/dockerhtml:1.1
```

-------------
### Some additional tips and info
If you want to run the container and delete it after you exit it - then use following command
```
docker run --rm -it pmunot11/dockerhtml:1.1
```
To name the container use following command
```
docker run -d -P --name docker-static-site pmunot11/dockerhtml:1.1
-d will detach our terminal,
-P will publish all exposed ports to random ports and finally
--name corresponds to a name we want to give.
Now we can see the ports by running the docker port [CONTAINER] command

docker port docker-static-site
```





















