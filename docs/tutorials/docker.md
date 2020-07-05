# How to run BerryNet in docker

 This page describe how to run BerryNet inside the Docker. The host os is currently on Debian or Ubuntu.

## Create a berrynet-buster image.
```
docker build -t berrynet-buster ./docker
```

## Create a privileged Ubuntu docker instance.

 Because BerryNet contains several services which needs systemd to load and run. 
 Thus we start with /sbin/init. Also we need to allow to use USB camera inside.

```
docker run -d --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:ro -v /dev/bus/usb:/dev/bus/usb --device /dev/video0:/dev/video0 berrynet-buster /sbin/init
```

## Login into the docker

```
docker exec -i -t <instance ID> /bin/bash
```

## Use BerryNet inside the docker

 You need to figure out the IP address of the docker and then use it.

1. Change the IP address inside the config file from localhost to 172.x.x.x

2. Now we can use the browser to access the dashboard outside of the docker through 172.x.x.x IP address.

