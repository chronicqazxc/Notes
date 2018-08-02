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
10. [assign a port mapping to an existing Docker container?](https://stackoverflow.com/a/26622041)
11. [restore-a-docker-volume-to-your-mac](https://medium.com/@jimkang/restore-a-docker-volume-to-your-mac-f79628617dee)
12. [getting-path-and-accessing-persistent-volumes-in-docker-for-mac](https://timonweb.com/posts/getting-path-and-accessing-persistent-volumes-in-docker-for-mac/)
13. [Docker for Mac Commands for Getting Into The Local Docker VM](https://www.bretfisher.com/docker-for-mac-commands-for-getting-into-local-docker-vm/)
14. [How do I kill all screens](https://unix.stackexchange.com/a/94528)

## [Bind Mount](https://docs.docker.com/storage/bind-mounts/)
```shell
docker run --name your_container_name -p 80:8080 -p 50000:50000 -v /Users/your_username/Documents/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
## [Create Volume](https://docs.docker.com/engine/reference/commandline/volume_create/)
```shell
docker run --name your_container_name -p 80:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
