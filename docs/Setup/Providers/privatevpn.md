# PrivateVPN

## TLDR

💁 To use with Wireguard, see [the custom provider Wireguard section](custom.md#wireguard).

For OpenVPN:

```sh
docker run -it --rm --cap-add=NET_ADMIN --device /dev/net/tun \
-e VPN_SERVICE_PROVIDER=privatevpn \
-e OPENVPN_USER=abc -e OPENVPN_PASSWORD=abc \
-e SERVER_COUNTRIES=Netherlands qmcgaw/gluetun
```

```yaml
version: "3"
services:
  gluetun:
    image: qmcgaw/gluetun
    cap_add:
      - NET_ADMIN
    devices:
      - /dev/net/tun:/dev/net/tun
    environment:
      - VPN_SERVICE_PROVIDER=privatevpn
      - OPENVPN_USER=abc
      - OPENVPN_PASSWORD=abc
      - SERVER_COUNTRIES=Netherlands
```

## Required environment variables

- `VPN_SERVICE_PROVIDER=privatevpn`
- `OPENVPN_USER`
- `OPENVPN_PASSWORD`

## Optional environment variables

- `SERVER_COUNTRIES`: Comma separated list of countries
- `SERVER_CITIES`: Comma separated list of cities
- `SERVER_HOSTNAMES`: Comma separated list of server hostnames
- `OPENVPN_ENDPOINT_PORT`: Custom OpenVPN server endpoint port to use

## VPN server port forwarding

Set `VPN_PORT_FORWARDING=on` and the port forwarded will be logged out as well as available via the http control server.

## Servers

To see a list of servers available, [list the VPN servers with Gluetun](../servers.md#list-of-vpn-servers).
