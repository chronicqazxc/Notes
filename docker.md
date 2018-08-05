# Notes of Docker

1. [putting-jenkins-docker-container](https://engineering.riotgames.com/news/putting-jenkins-docker-container)
2. [container](https://docs.docker.com/engine/reference/commandline/container/)
3. [recap-and-cheat-sheet-optiona](https://docs.docker.com/get-started/part2/#recap-and-cheat-sheet-optional)
4. [image](https://docs.docker.com/engine/reference/commandline/image/)
5. [logging](https://docs.docker.com/config/containers/logging/)
6. [Exploring Docker container's file system](https://stackoverflow.com/a/20816397)
7. [Programmatically removes files/folder resides in docker container](https://stackoverflow.com/a/38591846)
8. [understanding-volumes](https://container-solutions.com/understanding-volumes-docker/)
9. [assign a port mapping to an existing Docker container?(Create a new image based on current container)](https://stackoverflow.com/a/26622041)
10. [restore-a-docker-volume-to-your-mac](https://medium.com/@jimkang/restore-a-docker-volume-to-your-mac-f79628617dee)
11. [getting-path-and-accessing-persistent-volumes-in-docker-for-mac](https://timonweb.com/posts/getting-path-and-accessing-persistent-volumes-in-docker-for-mac/)
12. [Docker for Mac Commands for Getting Into The Local Docker VM](https://www.bretfisher.com/docker-for-mac-commands-for-getting-into-local-docker-vm/)
13. [How do I kill all screens](https://unix.stackexchange.com/a/94528)
14. [SCP](http://www.hypexr.org/linux_scp_help.php) file from Docker VM to localhost: ```scp -r file_to_be_moved username@remote_host:/path/to/destination/dir```
15. [Copying files from host to Docker container](https://stackoverflow.com/a/31971697)
16. [Pushing and Pulling to and from Docker Hub (Backup Images)](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html)
17. [Backup Volumes](https://github.com/moby/moby/issues/32263#issuecomment-290753968)
18. [Login container as root](https://stackoverflow.com/a/35485346)

## [Bind Mount](https://docs.docker.com/storage/bind-mounts/)
```shell
docker run --name your_container_name -p 80:8080 -p 50000:50000 -v /Users/your_username/Documents/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
## [Create Volume](https://docs.docker.com/engine/reference/commandline/volume_create/)
```shell
docker run --name your_container_name -p 80:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
## Back Volume
```shell
docker run --rm --volumes-from jenkins_container_name --name tmp-backup -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /var/jenkins_home
```
