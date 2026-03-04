---
icon: simple/docker
---
# :simple-docker: Docker

## Interactive shell in container

### Bash

```
docker exec -it <container> /bin/bash
docker run -it --rm <image> /bin/bash
```

### POSIX shell

```
docker exec -it <container> /bin/sh
docker run -it --rm <image> /bin/sh
```

## Container IP

Prints a container's IP, along with the name of the network.

```
docker inspect -f '{{range $name, $net := .NetworkSettings.Networks}}{{printf "%-15s %s\n" $name $net.IPAddress}}{{end}}' <container>
```

Output:
```
cloudflared     172.21.0.23
postgres        172.18.0.5
```