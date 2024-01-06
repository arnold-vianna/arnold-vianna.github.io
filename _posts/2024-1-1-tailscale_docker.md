---
title: Tailscale docker
date: 2024/1/1 12:00:00 -500
categories: [docker, Cheat Sheet]
tags: [docker, cheat sheet]    # tags should allways be lowercase
---

# Tailscale Docker Cheat Sheet

Setting up a Tailscale Docker container

* mkdir tailscale
* cd tailscale 
* mkdir root

# Here is the dockerfile


```bash
FROM alpine:3.15

RUN \
  apk add --no-cache \
    bind-tools \
    tailscale 

# add local files
COPY /root /

ENTRYPOINT [ "/entrypoint.sh" ]
```

------------------------------------------------------------------------------------

#   make entrypoint.sh file

* make a file in the root folder
* root/entrypoint.sh

```bash
#! /bin/sh

# create tun device
if [ ! -c /dev/net/tun ]; then
  mkdir -p /dev/net
  mknod /dev/net/tun c 10 200
fi

# Enable devices MASQUERADE mode
iptables -t nat -A POSTROUTING -o eth+ -j MASQUERADE
iptables -t nat -A POSTROUTING -o tailscale+ -j MASQUERADE

# start vpn client
tailscaled
```

------------------------------------------------------------------------------------

# Make sure the entrypoint is executable

* run this command


```bash
chmod +x root/entrypoint.sh
```

------------------------------------------------------------------------------------

# The directory structure should look like this:



```bash
tailscale/
├─ root/
│  ├─ entrypoint.sh
├─ Dockerfile
```

------------------------------------------------------------------------------------

# Now build the container


```bash
sudo docker build -t tailscaled .
```

------------------------------------------------------------------------------------
# On the Docker host running Kasm Workspaces (or Agent Server if using a Mult-Server Deploy) create a custom docker network 

* these commands will be on the machine with kasm
* open a terminal and past 

```bash
sudo docker network create \
  --driver=bridge \
  --opt icc=true \
  --subnet=172.20.0.0/16 \
  vpn-1
```

------------------------------------------------------------------------------------

# Now spinup a Tailscale Docker container: 

* same as the last steps
* copy and past in the terminal

```bash
sudo docker run -d \
  --cap-add NET_ADMIN \
  --name tailscaled \
  --net vpn-1 \
  --ip 172.20.0.2 \
  --restart unless-stopped \
  tailscaled
```

------------------------------------------------------------------------------------


# Now login using the auth key

* past youre auth key
* ready to use

```bash
sudo docker exec tailscaled tailscale up --authkey=<AUTH KEY FROM tailscale>
```

------------------------------------------------------------------------------------

# For the documentation see kasm

* this link explains how to use tailscale with docker
* this was made with thare information

```bash
https://kasmweb.com/docs/latest/how_to/vpn_sidecar/vpn_sidecar.html#option-3-tailscale
```

------------------------------------------------------------------------------------