# Official CCA for Splunk Docker image

The open source project for CCA for Splunk that is [available on Docker Hub](https://hub.docker.com/r/innovationfleet/cca_for_splunk).

The project that used this image is [cca_for_splunk](https://github.com/innovationfleet/cca_for_splunk)

This instruction is written for Mac and Linux users.

# Pull image from docker

´docker pull innovationfleet/cca_for_splunk:latest´

# Bind Mount

Create a directory where cca_for_splunk can create companion repos for CCA infrastructure and onboarding configuration.

```
mkdir -p ${PWD}/config/data
```

When the directory is created go ahead and pull and launch the latest cca_for_splunk docker image from Docker Hub.


This will use a bind mount and data can easily be accessible from the host machine.

```
docker run -d --name cca_for_splunk -it -v ${PWD}/config/data:/opt/cca_manager/data cca_for_splunk
```

# Volume Mount

You will probably want to make that an explicit volume so you can manage it and attach to another container for upgrades :

```
docker run -d --name cca_for_splunk -it -v cca_home:/opt/cca_manager/data cca_for_splunk
```

This will automatically create a 'cca_home' [docker volume](https://docs.docker.com/storage/volumes/) on the host machine. Docker volumes retain their content even when the container is stopped, started, or deleted.

# Usage

Connect to the docker image that has cca_for_splunk preinstalled.
```
docker exec -it cca_for_splunk /bin/bash '-l'
```

NOTE: If this is the first connection for a given release, setup wizard will run automatically to create user specific configurations. This will store the workspace in `${PWD}/config/data`. All CCA for Splunk data lives in there - including apps and configuration.

[![cca_for_splunk Setup Wizard](https://asciinema.org/a/567633.svg)](https://asciinema.org/a/567633)
