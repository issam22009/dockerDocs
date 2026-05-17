# dockerDocs
docker build PATH : a command that we run in the terminal, it is used to build an image based on the docker file

once we build the image, we need to run a container based on this image.

to run the container, we use :
docker run -p LOCAL_POST:THE_EXPOSED_PORT_FROM_DOSCKERFILE ID_IMAGE : -p is for publish. if we dont use the -p tag, the container won't expose it's port locally even thought it is precised in the dockerfile