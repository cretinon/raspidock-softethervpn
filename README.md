# Docker image for SoftEther VPN

This will deploy a fully functional [SoftEther VPN](https://www.softether.org) server as a docker image.

Available on [Docker Hub](https://hub.docker.com/r/cretinon/raspidock-softethervpn/)

With the help of [resin.io](https://resin.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/) to build on dockerhub and [frosquin](https://hub.docker.com/r/frosquin/softether/)

## Download

    docker pull cretinon/raspidock-softethervpn
	
## Run

Simplest version:

    docker run -d --privileged --net host --cap-add NET_ADMIN --name softether cretinon/raspidock-softethervpn

With external config file:

    touch /etc/vpnserver/vpn_server.config
    docker run -d --privileged -v /etc/vpnserver/vpn_server.config:/usr/local/vpnserver/vpn_server.config --net host --cap-add NET_ADMIN --name softether cretinon/raspidock-softethervpn

If you want to keep the logs in a data container:

    docker volume create --name softether-logs
    docker run -d --privileged --net host --cap-add NET_ADMIN --name softether -v softether-logs:/var/log/vpnserver cretinon/raspidock-softethervpn

All together now:

    touch /etc/vpnserver/vpn_server.config
    docker volume create --name softether-logs
    docker run -d --privileged -v /etc/vpnserver/vpn_server.config:/usr/local/vpnserver/vpn_server.config  -v softether-logs:/var/log/vpnserver --net host --cap-add NET_ADMIN --name softether cretinon/raspidock-softethervpn

