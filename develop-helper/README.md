```
docker run --privileged --restart always --mount type=bind,source=$env:USERPROFILE,target=/mnt --mount source=localuser-home,target=/home/localuser --mount source=docker_in_docker,target=/var/lib/docker --publish 22:22 --name develop_helper --detach develop_helper:base
```