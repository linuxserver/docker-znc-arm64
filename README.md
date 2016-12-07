[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/znc-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/znc-aarch64.svg)](https://microbadger.com/images/lsioarmhf/znc-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/znc-aarch64.svg)](http://microbadger.com/images/lsioarmhf/znc-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/znc-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/znc-aarch64.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-arm64/lsioarm64-znc)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-arm64/job/lsioarm64-znc/)
[hub]: https://hub.docker.com/r/lsioarmhf/znc-aarch64/

[ZNC](http://wiki.znc.in/ZNC)  is an IRC network bouncer or BNC. It can detach the client from the actual IRC server, and also from selected channels. Multiple clients from different locations can connect to a single ZNC account simultaneously and therefore appear under the same nickname on IRC.

[![znc](http://wiki.znc.in/resources/assets/wiki.png)][zncurl]
[zncurl]: http://wiki.znc.in/ZNC

## Usage

```
docker create \
  --name=znc \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \
  -p 6501:6501 \
  lsioarmhf/znc-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 6501` - the port(s)
* `-v /config` -
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone EG. Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it znc /bin/bash`.


### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARM64 VERSION`

To log in to the application, browse to https://<hostip>:6501.

* Default User: admin
* Default Password: admin
`change password ASAP.`

## Info

* Shell access whilst the container is running: `docker exec -it znc /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f znc`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' znc`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/znc-aarch64`


## Versions

+ **07.12.16:** Initial Release.
