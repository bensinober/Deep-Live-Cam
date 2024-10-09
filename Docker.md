# Docker.md

## Fix

## fetch missing models from huggingspace

https://huggingface.co/hacksider/deep-live-cam/tree/main

    wget https://huggingface.co/hacksider/deep-live-cam/resolve/main/inswapper_128_fp16.onnx
    wget https://huggingface.co/hacksider/deep-live-cam/resolve/main/inswapper_128.onnx?download=true

## insightface model (buffalo)

https://github.com/deepinsight/insightface/releases/download/v0.7/buffalo_l.zip

### CPU

docker build -t deep-live-cam -f Dockerfile.cpu .

xhost +local:docker

docker run --rm --name deep-live-cam -e DISPLAY=$DISPLAY --device=/dev/video0:/dev/video0 -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/Bilder:/app/pics -v /dev/dri/card1:/dev/dri/card1 -v /dev/dri/renderD128:/dev/dri/renderD128 --user 0 --privileged deep-live-cam

DISPLAY=:0 python3 run.py --execution-provider cpu --live-mirror

### CUDA

docker build -t deep-live-cam -f Dockerfile.cpu .

xhost +local:docker

docker run --rm -it --name deep-live-cam -e DISPLAY=$DISPLAY --entrypoint /bin/bash -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/Bilder:/app/pics --device=/dev/video0:/dev/video0 --user 0 --privileged --gpus all deep-live-cam

DISPLAY=:0 python3 run.py --execution-provider cuda --live-mirror
