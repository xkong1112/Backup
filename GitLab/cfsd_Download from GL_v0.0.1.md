# Download docker from GitLab

## Install curl

```
sudo apt-get install curl
```

## Install docker in Ubuntu or other Linux pulication using apt

```bash
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
```

## Docker login

```bash
docker login https://git.chalmers.se/cfs/driverless20/cfsd-opendlv-device-camera-zed.git
xkong
Z1DWiXbxUnLt_3KcGdJy
docker pull git.chalmers.se/cfs/driverless20/cfsd-opendlv-device-camera-zed:v0.0.2
```

## Runner...