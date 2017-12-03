# Compiler Explorer image
Run Matt Godbolt's compiler explorer locally. https://godbolt.org

## Content
This imgae is based on official docker image of Ubuntu:latest. It contains the following compilers:
* gcc 4.4.7
* gcc 4.6.4
* gcc 5.4.1
* gcc 6.3.0
* gcc 7.2.0

## Usage
Run container with following command:
```Bash
docker run --restart always --publish 10240:10240 --name compiler-explorer --detach aoleksy/compiler-explorer
```

Description of the used switches:
* ``--restart always`` - container will be run always, even after host restart
* ``--publish 10240:10240`` - Compiler Explorer is available on port 10240
* ``--name compiler-explorer`` - name assigned to container
* ``--detach`` - run container in the background
