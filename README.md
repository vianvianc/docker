# Docker Intro
This code repository is a simple proof-of-concept Docker container example

## How to use this repository
- Create a server and install docker on it
  - We use Digital Ocean droplets for this process, but it can be done on any host or even locally
- Clone this git repo to the server
- Navigate inside the directory you just created and run the commands from the "How to create an image and container" section below
- You now have a running Docker container

## How to create an image and container
Build the image with your username: 
`docker image build -t <YOUR_USERNAME>/pwp .`
* `build` a docker command that builds a docker image based on a dockerfile
* `-t` allows us to give the image our own name
* `.` refers to where you want to create the image from
  * Reminder: `.` is Linux shorthand for "the directory that we are currently in"

Check for the image: 
`docker image ls`

Create a new container from the image:
`docker container run --rm --name pwp -p 80:80 -d <YOUR_USERNAME>/pwp`
* `--rm` means to delete the container when it stops running (default is to be manually removed)
* `--name` is optional but highly reccommended. Naming a container lets you reference it in commands by name instead of container id.
* `-p 80:80` means to publish Docker's port 80 to your local machine's port 80 (port 80 is the default port for http)
* `-d` means to run in detach mode, or in other words in the background of your terminal
  * if you don't do this, you will 

Check for the running container
`docker container ls` or `docker ps`
* We prefer `docker container ls` because it is more consistent with the other commands
* If this works, you have correctly built an image and created a container based on it


#### Useful Docker commands
Run a single command on a running container  
`docker container exec command`
- `exec` stands for execute 
- `command` can be any valid unix command as long as the right arguments are used.  

Gain shell access to the container
`docker container exec -it pwp /bin/bash`
* `exec` executes a shell command on the droplet
* `-it` flags stand for interactive tty whichs allows for the container to take over the terminal
* `pwp` is the name of the container you want to run a command on
* `/bin/bash` is the command on the container you want to run. In this case the command starts a bash session
  * Occasionally, bash will not be installed on your container, in which case you can use `/bin/sh` instead

Rename a docker image
`docker rename my_container my_new_container`

Stop the running container
`docker container stop my_container`
* `stop` is a docker command that stops a running container

Delete a container 
`docker container rm -f my_container`
- You can use a name or an ID for my_container

View the docker logs
`docker container logs -f my_container`
- Very useful for debugging backend problems, such as when Insomnia can't connect to your Express container
