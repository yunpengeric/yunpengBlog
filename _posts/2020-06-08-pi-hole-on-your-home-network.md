---
layout: post
title: Pi-hole on Your Home Network
---

# Background

I have seen a lot of people post blogs regarding working from home, so I would like to share my experience of a small network change while working remotely. 

Recently, I have deployed Pi-hole (an ad blocking tool) in my home network to improve network security and performance. At the same time, Ad blocking  improves my productivity as well.  Pi-hole is capable of recording, blocking and visualising DNS queries from your home devices. The most important thing is to find the "unusual" traffic from your applications to protect your privacy. If you have children at home, this is also a great internet safety tool for kids.

# Prerequisites

Usually Pi-hole is deployed to these three places:

- Raspberry Pi > Highly recommended 🙌🏻
- NAS > Recommended 👍🏻
- Public Cloud (e.g. AWS EC2) > Not recommended unless you can make it secure.🔒

# Process

The following process is to spin up a Pi - hole Docker container on Ubuntu 20.04, other Linux distributions are similar. 

## Disable `systemd-resolved`

You need to disable `systemd-resolved` to prevent port conflicts if you are using Ubuntu (17.10+):

```bash
sudo systemctl stop systemd-resolved.service
sudo systemctl disable systemd-resolved.service
```

Then manually set the `nameserver` to Google Public DNS:

```bash
sudo vim /etc/resolv.conf
nameserver 8.8.8.8
```

Then add your hostname to `/etc/hosts`:

```bash
echo $(hostname -I | cut -d\  -f1) $(hostname) | sudo tee -a /etc/hosts
```

## Create the Script File

Create the `pihole_docker_run.sh` file by pasting the following scripts:

- You may want to change `TZ` environment variable to your [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

```bash
cat << EOF > pihole_docker_run.sh
#!/bin/bash

# https://github.com/pi-hole/docker-pi-hole/blob/master/README.md

docker run -d \
    --name pihole \
    -p 53:53/tcp -p 53:53/udp \
    -p 80:80 \
    -p 443:443 \
    -e TZ="Australia/Sydney" \
    -v "$(pwd)/etc-pihole/:/etc/pihole/" \
    -v "$(pwd)/etc-dnsmasq.d/:/etc/dnsmasq.d/" \
    --dns=127.0.0.1 --dns=1.1.1.1 \
    --restart=unless-stopped \
    --hostname pi.hole \
    --privileged \
    pihole/pihole:latest

printf 'Starting up pihole container '
for i in \$(seq 1 20); do
    if [ "\$(docker inspect -f "{{.State.Health.Status}}" pihole)" == "healthy" ] ; then
        printf ' OK'
        echo -e "\n$(docker logs pihole 2> /dev/null | grep 'password:') for your pi-hole: https://\$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')/admin/"
        exit 0
    else
        sleep 3
        printf '.'
    fi

    if [ \$i -eq 20 ] ; then
        echo -e "\nTimed out waiting for Pi-hole start, consult check your container logs for more info (\`docker logs pihole\`)"
        exit 1
    fi
done;
EOF
```

## Run the Pi-hole Container

Add executable permissions to `pihole_docker_run.sh` then run the script:

```bash
chmod u+x pihole_docker_run.sh &&
./pihole_docker_run.sh
```

You will get your web interface URL from the output. (e.g. [`https://172.31.13.205/admin/`](https://172.31.13.205/admin/))

## Web Interface Password

To get your web interface password:

```bash
docker logs pihole | grep random
```

You may also want to reset your password, then enter your password into the prompt:

```bash
docker exec -it pihole pihole -a -p
```

## Configure your Router

You need to configure your router to use Pi-hole as its DNS server.

If you are using an ASUS router, you can go to [`http://router.asus.com/Advanced_DHCP_Content.asp`](http://router.asus.com/Advanced_DHCP_Content.asp) and change  the `DNS server` to Pi-hole's IP address.

For other methods:

[How do I configure my devices to use Pi-hole as their DNS server?](https://discourse.pi-hole.net/t/how-do-i-configure-my-devices-to-use-pi-hole-as-their-dns-server/245)

## Allowlist Domains

You may also want to allowlist some Domains. (e.g. YouTube history sync problems)

[Commonly Whitelisted Domains](https://discourse.pi-hole.net/t/commonly-whitelisted-domains/212)