```
docker run --privileged --restart always --mount source=localuser-home,target=/home/localuser --mount type=bind,source=$env:USERPROFILE/Workspace,target=/home/localuser/workspace --publish 22:22 --name develop_helper --detach develop_helper:base
```