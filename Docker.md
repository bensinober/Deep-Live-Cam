# Docker.md

docker build -t deep-live-cam -f Dockerfile.cpu .

xhost +local:docker

docker run --rm --name deep-live-cam -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/Bilder:/app/pics --device=/dev/video0:/dev/video0 --user 0 --privileged deep-live-cam
