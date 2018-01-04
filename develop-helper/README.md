```
docker run --privileged --restart always --mount source=localuser-home,target=/home/localuser --publish 22:22 --name develop_helper --detach develop_helper:base
```