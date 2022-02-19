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
## 2. Test
```bash
$ wget https://download.openmmlab.com/mmrotate/v0.1.0/rotated_faster_rcnn/rotated_faster_rcnn_r50_fpn_1x_dota_le90/rotated_faster_rcnn_r50_fpn_1x_dota_le90-0393aa5c.pth
$ wget https://download.openmmlab.com/mmrotate/v0.1.0/oriented_rcnn/oriented_rcnn_r50_fpn_1x_dota_le90/oriented_rcnn_r50_fpn_1x_dota_le90-6d2b2ce0.pth

$ python demo/image_demo.py \
demo/demo.jpg \
configs/oriented_rcnn/oriented_rcnn_r50_fpn_1x_dota_le90.py  \
oriented_rcnn_r50_fpn_1x_dota_le90-6d2b2ce0.pth \
demo/vis.jpg
```
