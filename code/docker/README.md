# Build and run Docker image for AI development, deployment and data visuaization

## requirements
Postman-linux-x64-7.2.2.tar.gz

## build

docker-compose build

## run container

### setup alias to launch container

`~/.alias`
```
alias kaidev='docker run --rm -u $(id -u):$(id -g) --name kaidev --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" -p "8899:8899" --memory=16g  --shm-size=16g -p "6006:6006" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY kaidev_gpu bash'
```

`. ~/.alias`

`$ kaidev`

## Commands in docker container

### jupyter

`launch_jupyter_notebook.sh`

### tensorboard

```
alias tensorboard-docker='tensorboard --logdir output/Coronahack-Chest/logs --host 0.0.0.0 --port 6006'
```

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

## Environment 
export environment from Docker image
```
conda env export -n base -f environment.yml
```