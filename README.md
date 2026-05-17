# dockerDocs
docker build PATH : a command that we run in the terminal, it is used to build an image based on the docker file

once we build the image, we need to run a container based on this image.

to run the container, we use :
docker run -p LOCAL_POST:THE_EXPOSED_PORT_FROM_DOSCKERFILE ID_IMAGE : -p is for publish. if we dont use the -p tag, the container won't expose it's port locally even thought it is precised in the dockerfile

 EXPOSE 80 in the Dockerfile in the end is optional. It documents that a process in the container will expose this port. But you still need to then actually expose the port with -p when running docker run. So technically, -p is the only required part when it comes to listening on a port. Still, it is a best practice to also add EXPOSE in the Dockerfile to document this behavior.

As an additional quick side-note: For all docker commands where an ID can be used, you don't always have to copy / write out the full id.

You can also just use the first (few) character(s) - just enough to have a unique identifier.

So instead of

docker run abcdefg
you could also run

docker run abc
or, if there's no other image ID starting with "a", you could even run just:

docker run a
This applies to ALL Docker commands where IDs are needed.

# cache image layers: 
when we rerun a build command without any modifications, the build pass very quickly, it's because every result of a command (layers) is cached, and we use this result to build the image.
when a modification is acted, and we run the build, we can see that some parts of the image construction are quick, it uses the cache, and when there is no cache, it reexecute the command.
