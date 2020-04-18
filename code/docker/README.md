# Build and run Docker image for AI development, deployment and data visuaization

## requirements
atom-amd64.deb
dbeaver-ce_6.1.2_amd64.deb
pycharm-community-2019.1.1.tar.gz
code_1.33.1-1554971066_amd64.deb
Postman-linux-x64-7.2.2.tar.gz

## build

docker-compose build

## run container

### setup alias to launch container

`~/.alias`
```
alias kaidev='docker run --rm -u $(id -u):$(id -g) --name kaidev --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" -p "8899:8899" --shm-size=6g -p "5006:5006" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY kaidev_gpu bash'
```

`. ~/.alias`

`$ kaidev`

## Commands in docker container

### jupyter

`launch_jupyter_notebook.sh`

### Code editors

#### Visual Studio code

`code &`

#### Pycharm

`pycharm.sh &`

#### atom

`atom &`

## Database

* mongo
* postgresql
* dbeaver

## Web
nginx
Postman 

