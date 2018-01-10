[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://couchpota.to/
[hub]: https://hub.docker.com/r/lsioarmhf/couchpotato/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/couchpotato
[![](https://images.microbadger.com/badges/version/lsioarmhf/couchpotato.svg)](https://microbadger.com/images/lsioarmhf/couchpotato "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/couchpotato.svg)](https://microbadger.com/images/lsioarmhf/couchpotato "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/couchpotato.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/couchpotato.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-couchpotato)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-couchpotato/)

[CouchPotato](https://couchpota.to) is an automatic NZB and torrent downloader. You can keep a "movies I want" list and it will search for NZBs/torrents of these movies every X hours. Once a movie is found, it will send it to SABnzbd or download the torrent to a specified directory.

[![couchpotato](https://couchpota.to/media/images/full.png)][appurl]

## Usage

```
docker create \
	--name=couchpotato \
	-v <path to data>:/config \
	-v <path to data>:/downloads \
	-v <path to data>:/movies \
	-e PGID=<gid> -e PUID=<uid>  \
	-e TZ=<timezone> \
	-e UMASK_SET=<022> \
	-p 5050:5050 \
	lsioarmhf/couchpotato
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 5050` - the port(s)
* `-v /config` - Couchpotato Application Data
* `-v /downloads` - Downloads Folder
* `-v /movies` - Movie Share
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
* `-e UMASK_SET` for umask setting of couchpotato, *optional* , default if left unset is 022.
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine-linux with S6 overlay, for shell access whilst the container is running do `docker exec -it couchpotato /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Info
`IMPORTANT... THIS IS THE ARMHF VERSION`

* To monitor the logs of the container in realtime `docker logs -f couchpotato`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' couchpotato`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/couchpotato`

## Versions

+ **10.01.18:** Rebase to alpine 3.7.
+ **20.07.17:** Internal git pull instead of at runtime, add UMASK_SET variable.
+ **29.05.17:** Rebase to alpine 3.6.
+ **07.02.17:** Rebase to alpine 3.5.
+ **11.11.16:** Stop cp logging to docker log (they are accessible in the webui and the config folder)
+ **14.10.16:** Add version layer information.
+ **30.09.16:** Fix umask.
+ **11.09.16:** Add layer badges to README.
+ **06.09.16:** Add badges to README.
+ **01.09.16:** Initial Release.
