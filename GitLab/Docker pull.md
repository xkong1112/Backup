# Docker pull

## Testing

```bash
E: Failed to fetch https://vorboss.dl.sourceforge.net/project/corefonts/the fonts/final/comic32.exe  Could not wait for server fd - select (11: Resource temporarily unavailable) [IP: 5.10.152.194 443]
E: Download Failed
```

```bash
debconf: delaying package configuration, since apt-utils is not installed
```

Not important! Succeed anyway.

## Build the docker on the GitLab

After passing the test, go to ``` Packages``` and click ```Container Registry```, then copy the URL of the project, for example```git.ita.chalmers.se:4443/xkong/cfsd-opendlv-device-camera-zed```. 

## Docker pull form the big computer

First, docker login needed in this case.

```bash
docker login git.ita.chalmers.se:4443/xkong/cfsd-opendlv-device-camera-zed
```

Then type the user name and password

```
$Username
$Password
```

Password is got from the Personal Access Token (in User Settings/ Access Tokens) with an expired date. (Scopes: read_registry)

Then pull the docker file!! (Specify the version)

```bash
docker pull git.ita.chalmers.se:4443/xkong/cfsd-opendlv-device-camera-zed:v0.0.1
```

However, I use docker login to the URL for the camera repo. What if I want to download another repo? 
I think it is login the xkong,so you only need to login it once. And name the repos/images name. Then you could download it.

## Run the camera docker

From the GitLab:

```bash
nvidia-docker run -ti --rm --privileged --init --ipc=host --net=host -e DISPLAY=$DISPLAY -v /tmp:/tmp image_name:version opendlv-device-camera-zed --profile=1280x720@60 --verbose
```

Then, adjust the  ```image_name:version```  with ```git.ita.chalmers.se:4443/xkong/cfsd-opendlv-device-camera-zed:v0.0.1``` 

If it doesn't work, then use 

```
dmesg
```

to check if the usb connection for the camera is okay for all input devices.

Before the run, let camera have the ability to access the screen: 

```
xhost +
```

Then run

```
nvidia-docker run -ti --rm --privileged --init --ipc=host --net=host -e DISPLAY=$DISPLAY -v /tmp:/tmp git.ita.chalmers.se:4443/xkong/cfsd-opendlv-device-camera-zed:v0.0.1 opendlv-device-camera-zed --profile=1280x720@60 --verbose
```

Make sure the Internet is connected and reboot the PC if needed. 

