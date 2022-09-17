# Running a GUI in a docker container

This repo is a very simple example of running a GUI (in this case xeyes) in a docker container.

Steps required to make this work:

1. Allow X Server connections with `xhost +local:*`
2. Build the container with `docker build -t xeyes-gui-app:latest .`
3. Launch container with `docker run --rm --net=host -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix/:/tmp/.X11-unix/ --name xeyes-gui-app-test xeyes-gui-app:latest`

If this is successful, you should see a GUI with 2 eyes popup.  Those eyes will follow your cursor around.  When you close the GUI, the container also exits.

## Notes
Instead of allowing X Server connections on your host, you would need to install xauth in the container, and installed a valid auth token in the container, found on the host via `xauth list`, then install it in the container with `xauth add <token>`