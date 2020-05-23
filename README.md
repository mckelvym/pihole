# Pi-Hole

## Create Volumes

```
docker volume create pihole
docker volume create dnsmasq
```

## Docker Run

```
docker run \
--name=pihole \
-e TZ=America/New_York \
-e WEBPASSWORD=YOURPASS \
-e SERVERIP=YOUR.SERVER.IP \
-v pihole:/etc/pihole \
-v dnsmasq:/etc/dnsmasq.d \
-p 80:80 \
-p 53:53/tcp \
-p 53:53/udp \
--restart=unless-stopped \
pihole/pihole
```

or

```
docker run --name=pihole -e TZ=America/New_York -e WEBPASSWORD=YOURPASS -e SERVERIP=YOUR.SERVER.IP -v pihole:/etc/pihole -v dnsmasq:/etc/dnsmasq.d -p 80:80 -p 53:53/tcp -p 53:53/udp --restart=unless-stopped pihole/pihole
```

e.g.:

```
docker run --name=pihole -e TZ=America/New_York -e WEBPASSWORD=pihole1 -e SERVERIP=192.168.1.10 -v pihole:/etc/pihole -v dnsmasq:/etc/dnsmasq.d -p 80:80 -p 53:53/tcp -p 53:53/udp --restart=unless-stopped pihole/pihole
```

## Setup

Configure at:

```
http://YOURSERVERIP/admin
```

## Reference

[https://codeopolis.com/posts/running-pi-hole-in-docker-is-remarkably-easy]

## Systemd

```
sudo systemctl disable systemd-resolved
sudo systemctl stop systemd-resolved
```

Then put the following line in the [main] section of your `/etc/NetworkManager/NetworkManager.conf`:

```
dns=default
```

Delete the symlink `/etc/resolv.conf`, which normally points to `/run/systemd/resolve/stub-resolv.conf`:

```
rm /etc/resolv.conf
```

Restart NetworkManager:

```
sudo systemctl restart NetworkManager
```

### Reference

[https://askubuntu.com/a/907249]

