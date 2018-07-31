# Notes of Docker

1. [putting-jenkins-docker-container](https://engineering.riotgames.com/news/putting-jenkins-docker-container)
2. [container](https://docs.docker.com/engine/reference/commandline/container/)
3. [recap-and-cheat-sheet-optiona](https://docs.docker.com/get-started/part2/#recap-and-cheat-sheet-optional)
4. [image](https://docs.docker.com/engine/reference/commandline/image/)
5. [Copying files from host to Docker container](https://stackoverflow.com/a/31971697)
6. [logging](https://docs.docker.com/config/containers/logging/)
7. [Exploring Docker container's file system](https://stackoverflow.com/a/20816397)
8. [Programmatically removes files/folder resides in docker container](https://stackoverflow.com/a/38591846)
9. [understanding-volumes](https://container-solutions.com/understanding-volumes-docker/)
## [Bind Mount](https://docs.docker.com/storage/bind-mounts/)
```shell
docker run -p 8080:8080 -p 50000:50000 -v /Users/tron/Documents/jenkins_home:/var/jenkins_home jenkins/jenkins
```
## [Create Volume](https://docs.docker.com/engine/reference/commandline/volume_create/)
```shell
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```