# mmrotate-exec-env

## 1. Usage
### 1-1. Docker Pull
```bash
$ docker pull pinto0309/mmrotate_exec_env:latest
```
### 1-2. Docker Build
```bash
$ docker build -t pinto0309/mmrotate_exec_env:latest .
```

### 1-3. Docker Run
```bash
$ docker run --gpus all --rm -it \
--shm-size=10g \
-v `pwd`:/mmrotate/data \
-v /tmp/.X11-unix/:/tmp/.X11-unix:rw \
--device /dev/video0:/dev/video0:mwr \
--net=host \
-e XDG_RUNTIME_DIR=$XDG_RUNTIME_DIR \
-e DISPLAY=$DISPLAY \
--privileged \
--name mmrotate_exec_env \
pinto0309/mmrotate_exec_env:latest
```

### 1-4. Local source code debugging
```bash
$ git clone https://github.com/open-mmlab/mmrotate.git \
&& cd mmrotate \
&& git checkout 6519a3654e17b707c15d4aa2c5db1257587ea4c0 \
&& mkdir -p data

$ docker run --gpus all --rm -it \
--shm-size=10g \
-v `pwd`:/mmrotate \
-v /tmp/.X11-unix/:/tmp/.X11-unix:rw \
--device /dev/video0:/dev/video0:mwr \
--net=host \
-e XDG_RUNTIME_DIR=$XDG_RUNTIME_DIR \
-e DISPLAY=$DISPLAY \
--privileged \
--name mmrotate_exec_env \
pinto0309/mmrotate_exec_env:latest
```