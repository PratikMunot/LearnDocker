### Playing with Busybox
Pull busybox image and run the container
```
$ docker pull busybox
```
Check if image has been pulled in our system
```
$ docker images
```
Run the container
```
$ docker run busybox
```
When you call run, the Docker client finds the image (busybox in this case), loads up the container and then runs a command in that container. When we run docker run busybox, we didn't provide a command, so the container booted up, ran an empty command and then exited.

We try to pass a command to execute to the container
```
$ docker run busybox echo "hello from busybox"
hello from busybox
```
Now we run the container and enter inside interactive shell ie attach a shell to our container 
```
$ docker run -it busybox sh
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # uptime
 05:45:21 up  5:58,  0 users,  load average: 0.00, 0.01, 0.04
```
Remove the container 
```
$ docker rm 25e2ca123d10
```
Remove all container which are in exited state and not the running ones
```
$ docker rm $(docker ps -a -q -f status=exited)

-q flag only returns the numeric IDs
-f flag filters output based on conditions 
```
The docker prune command can be used for same case where you want to remove all the containers which are in exited state
```
$ docker container prune
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
4a7f7eebae0f63178aff7eb0aa39f0627a203ab2df258c1a00b456cf20063
f98f9c2aa1eaf727e4ec9c0283bcaa4762fbdba7f26191f26c97f64090360

Total reclaimed space: 212 B
```



