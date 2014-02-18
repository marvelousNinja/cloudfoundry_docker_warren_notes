Docker
================

# Some basic terminology

## LXC (LinuX Containers)** 
Operating system-level virtualization method for running multiple isolated Linux systems (containers) on a single control host.

## Image
An image is a read only layer used to build a container. They do not change.

## Container
Is basically a self contained runtime environment that is built using one or more images. You can commit your changes to a container and create an image.

## Index / Registry
These are public or private servers where people can upload their repositories so they can easily share what they made.

## Repository
A repository is a group of images located in the docker registry. There are two types of repositories, Top level and user repositories. Top level repositories don't have a '/' in the name and they are usually reserved for base images. These Top level repositories is what most people build their repositories on top of. They are controlled by the maintainers of Docker. User repositories are repositories that anyone can upload into the registry and share with other people.

# Example and basic workflow
```
docker run base /bin/echo hello world   # Generate and run container based on 'base image' and execute 'echo hello world' command
docker ps -a                            # List all containers
docker images                           # List all available images
```

The following things happened during ```docker run``` command:

1. Generated a new LXC container
2. Created a new file system
3. Mounted a read/write layer
4. Allocated network interface
5. Setup IP
6. Setup NATing
7. Executed the process in the container
8. Captured it's output
9. Printed to screen
10. Stopped the container

More complicated example. Long-living container - it will print 'Hello world' every second.
```
CONTAINER_ID=$(docker run -d base /bin/sh -c "while true; do echo hello world; sleep 1; done") # Create a container and capture it's ID
docker logs $CONTAINER_ID                                                                      # Capture portion of container logs
docker attach $CONTAINER_ID                                                                    # Attach container output to current STDOUT   
docker stop $CONTAINER_ID                                                                      # Stop container
```

