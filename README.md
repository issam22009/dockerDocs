[Cheat-Sheet-Images-Containers.pdf](https://github.com/user-attachments/files/28690615/Cheat-Sheet-Images-Containers.pdf)
[slides-images-containers.pdf](https://github.com/user-attachments/files/28690614/slides-images-containers.pdf)
# dockerDocs
```docker build PATH``` : a command that we run in the terminal, it is used to build an image based on the docker file

once we build the image, we need to run a container based on this image.

to run the container, we use :
```docker run -p LOCAL_POST:THE_EXPOSED_PORT_FROM_DOSCKERFILE ID_IMAGE``` : -p is for publish. if we dont use the -p tag, the container won't expose it's port locally even thought it is precised in the dockerfile

 ```EXPOSE 80``` in the Dockerfile in the end is optional. It documents that a process in the container will expose this port. But you still need to then actually expose the port with -p when running docker run. So technically, -p is the only required part when it comes to listening on a port. Still, it is a best practice to also add EXPOSE in the Dockerfile to document this behavior.

As an additional quick side-note: For all docker commands where an ID can be used, you don't always have to copy / write out the full id.

You can also just use the first (few) character(s) - just enough to have a unique identifier.

So instead of

```docker run abcdefg```
you could also run

```docker run abc```
or, if there's no other image ID starting with "a", you could even run just: ```docker run a```

This applies to ALL Docker commands where IDs are needed.

# cache image layers: 
when we rerun a build command without any modifications, the build pass very quickly, it's because every result of a command (layers) is cached, and we use this result to build the image.
when a modification is acted, and we run the build, we can see that some parts of the image construction are quick, it uses the cache, and when there is no cache, it reexecute the command.

# Detele images and containers
```docker rm <Name1> <Name2>```: connot remove a running container, so we need to stop it before, docker stop <Name>

```docker images``` : list all images
```docker rmi <ID-image>```: delete image and all the layers of the image, this command deletes image that are no longer used, no containers based on this image, even the the stopped ones, you should remove all containers based on this image, then the rmi can be used.

```docker image prune``` : removes all unused images

```docker run -p 3000:80 -d --rm <id-image>``` : is used to start a new container based on a specified image, and it has several components that influence its behavior:

docker run: This is the command used to create and start a new container from a Docker image.

-p 3000:80: This option maps port 3000 on your host machine to port 80 on the container. This means that when you access localhost:3000 on your host, it will forward the traffic to port 80 of the running container. This is particularly useful for web applications or services running inside the container that listen on port 80.

-d: This flag stands for "detach." It tells Docker to run the container in the background (detached mode), allowing you to continue using the terminal for other commands without keeping the container's output visible.

--rm: This flag automatically removes the container once it stops running. This helps prevent clutter by ensuring that stopped containers do not occupy space and resources.

<id-image>: This placeholder should be replaced with the actual image ID or image name (with a tag) that you want to use for running the container.

# docker cp : 
1 - Copying a Local Folder to a Container: To copy a folder named dummy (which contains files) from your local machine to a running container, the command would look like this:
```docker cp dummy <container_name>:/path/inside/container/test```
2 - Copying from a Container to Local Machine: To copy a folder or file from the container back to your local machine, you would use:
```docker cp <container_name>:/path/inside/container/test /local/path/destination```

# Naming and tagging Containers and images :
Naming a Container
When creating a container, you can specify its name using the --name flag:
```docker run --name <container_name> <image_name>```

To tag an already existing image, you would use the following command:
```docker tag <source_image> <new_image_name>:<tag>```
to tag an image when you're building it : 
```docker build -t <image-name>:<tag-name> .```

# Sharing Images : 
let's say i want to push my image to dockerhub, i must follow these steps : 
STEP 1 : i must have an account into dockerhub plateform, and then, i must create a repository, in my case i called it ```test-node-hello```.
PS : this repository name should be the same as the name of my image in local.
STEP 2 : i must log in to docker in my terminal using ```docker login -u <username>``` 
STEP 3 : Push the image using : ```docker push username/image:tag```

To pull the image : if the repo is public, everyone can pull it using : ```docker pull username/repository:tag```

 
