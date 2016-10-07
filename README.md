[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/couchpotato


[![](https://images.microbadger.com/badges/image/lsioarmhf/couchpotato.svg)](http://microbadger.com/images/lsioarmhf/couchpotato "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/couchpotato.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/couchpotato.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-couchpotato)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-couchpotato/)
[hub]: https://hub.docker.com/r/lsioarmhf/couchpotato/

[CouchPotato](https://couchpota.to) is an automatic NZB and torrent downloader. You can keep a "movies I want" list and it will search for NZBs/torrents of these movies every X hours. Once a movie is found, it will send it to SABnzbd or download the torrent to a specified directory.

[![couchpotato](https://couchpota.to/media/images/full.png)][couchurl]
[couchurl]: https://couchpota.to/

## Usage

```
docker create \
	--name=couchpotato \
	-v <path to data>:/config \
	-v <path to data>:/downloads \
	-v <path to data>:/movies \
	-e PGID=<gid> -e PUID=<uid>  \
	-e TZ=<timezone> \
	-p 5050:5050 \
	lsioarmhf/couchpotato
```

**Parameters**

* `-p 5050` - the port(s)
* `-v /config` - Couchpotato Application Data
* `-v /downloads` - Downloads Folder
* `-v /movies` - Movie Share
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
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

## Version Log

+ **30.09.16:** Fix umask.
+ **11.09.16:** Add layer badges to README.
+ **06.09.16:** Add badges to README.
+ **01.09.16:** Initial Release
