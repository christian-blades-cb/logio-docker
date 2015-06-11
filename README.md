# Logio Docker Image

[![](https://badge.imagelayers.io/christianbladescb/logio-server:latest.svg)](https://imagelayers.io/?images=christianbladescb/logio-server:latest 'Get your own badge on imagelayers.io')

A docker image for [logio](http://logio.org/)

## How to run

### CoreOS

Modify the `logio-app.env.dist` file and put the contents into the etcd key `/environments/logio-app`
```shell
$ cp logio-app.env.conf logio-app.env
$ vi logio-app.env
$ etcdctl set /environments/logio-app < logio-app.env
```

Submit logio-app@.service and logio-discovery@.service (assuming you're running [vulcand](http://vulcanproxy.com/)) to fleet
```shell
$ fleetctl submit logio-{app,dicovery}@.service
```

Start it
```shell
$ fleetctl start logio-{app,discovery}@1
```

If you're running vulcand, you can now attach a frontend to the `logio` backend

### Other

```shell
$ docker run --name=logio -p 28777:28777 -p 28778:28778 -e AUTH_USER=user -e AUTH_PASS=pass christianbladescb/logio-server
```

Logio is now available on your docker machine.

port  | service
----- | -----------------
28777 | incoming loglines
28778 | web interface
