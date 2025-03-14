---
title: Welcome
---
# 🎊 Welcome to the Gluetun Wiki! 🎊

<!-- ![Visitors count](https://visitor-badge.laobi.icu/badge?page_id=gluetun.wiki) -->

Gluetun is a VPN client in a thin Docker container for multiple VPN providers,
written in Go. Gluetun utilizes OpenVPN or Wireguard and DNS over TLS, with a
few proxy servers built-in.

🐛 Found a bug in the Wiki?! [Please create an issue](https://github.com/qdm12/gluetun-wiki/issues/new).

## Versioning

Please use the appropriate version of the wiki depending on what version of Gluetun you are using.

| Gluetun release tag | Corresponding wiki |
| --- | --- |
| `:latest` | [`main` branch](https://github.com/qdm12/gluetun-wiki) |
| `:v3.39.0` | [`v3.39.0` tag](https://github.com/qdm12/gluetun-wiki/tree/v3.39.0) |
| `:v3.38.0` | [`v3.38.0` tag](https://github.com/qdm12/gluetun-wiki/tree/v3.38.0) |
| `:v3.35.0` | [`v3.35.0` tag](https://github.com/qdm12/gluetun-wiki/tree/v3.35.0) |

The Wiki aims to mirror the release tags of Gluetun, except the Wiki bugfix version number (last number) is for Wiki fixes only.

## Features

- Based on Alpine 3.20 for a small Docker image of 35.6MB
- Supports: **AirVPN**, **Cyberghost**, **ExpressVPN**, **FastestVPN**, **Giganews**, **HideMyAss**, **IPVanish**, **IVPN**, **Mullvad**, **NordVPN**, **Perfect Privacy**, **Privado**, **Private Internet Access**, **PrivateVPN**, **ProtonVPN**, **PureVPN**,  **SlickVPN**, **Surfshark**, **TorGuard**, **VPNSecure.me**, **VPNUnlimited**, **Vyprvpn**, **WeVPN**, **Windscribe** servers
- Supports OpenVPN for all providers listed
- Supports Wireguard both kernelspace and userspace
    - For **AirVPN**, **FastestVPN**, **Ivpn**, **Mullvad**, **NordVPN**, **Perfect privacy**, **ProtonVPN**, **Surfshark** and **Windscribe**
    - For **Cyberghost**, **Private Internet Access**, **PrivateVPN**, **PureVPN**, **Torguard**, **VPN Unlimited**, **VyprVPN** and **WeVPN** using [the custom provider](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/custom.md)
    - For custom Wireguard configurations using [the custom provider](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/custom.md)
    - More in progress, see [#134](https://github.com/qdm12/gluetun/issues/134)
- DNS over TLS baked in with service provider(s) of your choice
- DNS fine blocking of malicious/ads/surveillance hostnames and IP addresses, with live update every 24 hours
- Choice of vpn network protocol, `udp` or `tcp`
- Built in firewall kill switch to allow traffic only with needed the VPN servers and LAN devices
- Built in Shadowsocks proxy server (protocol based on SOCKS5 with an encryption layer, tunnels TCP+UDP)
- Built in HTTP proxy (tunnels HTTP and HTTPS through TCP)
- Compatible with amd64, i686 (32 bit), **ARM** 64 bit, ARM 32 bit v6 and v7, and even ppc64le 🎆
- Custom VPN server side port forwarding for [Perfect Privacy](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/perfect-privacy.md#vpn-server-port-forwarding), [Private Internet Access](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/private-internet-access.md#vpn-server-port-forwarding), [PrivateVPN](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/privatevpn.md#vpn-server-port-forwarding) and [ProtonVPN](https://github.com/qdm12/gluetun-wiki/blob/main/setup/providers/protonvpn.md#vpn-server-port-forwarding)
- Possibility of split horizon DNS by selecting multiple DNS over TLS providers
- Can work as a Kubernetes sidecar container, thanks @rorph

## Quickstart

For experienced users just looking for a `docker-compose.yml` template, refer to the following:

``` yaml
---
services:
  gluetun:
    image: qmcgaw/gluetun
    # container_name: gluetun
    # line above must be uncommented to allow external containers to connect.
    # See https://github.com/qdm12/gluetun-wiki/blob/main/setup/connect-a-container-to-gluetun.md#external-container-to-gluetun
    cap_add:
      - NET_ADMIN
    devices:
      - /dev/net/tun:/dev/net/tun
    ports:
      - 8888:8888/tcp # HTTP proxy
      - 8388:8388/tcp # Shadowsocks
      - 8388:8388/udp # Shadowsocks
    volumes:
      - /yourpath:/gluetun
    environment:
      # See https://github.com/qdm12/gluetun-wiki/tree/main/setup#setup
      - VPN_SERVICE_PROVIDER=ivpn
      - VPN_TYPE=openvpn
      # OpenVPN:
      - OPENVPN_USER=
      - OPENVPN_PASSWORD=
      # Wireguard:
      # - WIREGUARD_PRIVATE_KEY=wOEI9rqqbDwnN8/Bpp22sVz48T71vJ4fYmFWujulwUU=
      # - WIREGUARD_ADDRESSES=10.64.222.21/32
      # Timezone for accurate log times
      - TZ=
      # Server list updater
      # See https://github.com/qdm12/gluetun-wiki/blob/main/setup/servers.md#update-the-vpn-servers-list
      - UPDATER_PERIOD=
```

