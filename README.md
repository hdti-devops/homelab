# HOMELAB

This repository contains my homelab documentation and infrastructure files. Here, you'll find notes, setups, and configurations for infrastructure, applications, networking, and more.

## Prerequisite


## Homelab's Software

* [Technitium DNS](https://technitium.com/dns/) as DNS server
* [Wireguard](https://www.wireguard.com/) as VPN
* [TrueNAS](https://www.truenas.com/truenas-community-edition/) as NAS OS for managing data


## Proxmox Setup 

* Download Proxmox VE ISO Installer image from [the official site](https://www.proxmox.com/en/downloads).
* Make a bootable USB drive with the image, here i used [Rufus](https://rufus.ie/en/).
* Plug the Bootable USB to your server and set USB as first boot option in the BIOS.
* Proceed with the GUI Install

| Field             | Value           | Explanation                                         |
|-------------------|------------------|-------------------------------------------------------------------------------|
| Hostname (FQDN)   | pve.homelab      | Fully-qualified domain name for the Proxmox server. Can go with wtv suits you.|
| IP Address (CIDR) | 192.168.1.50/24  | Static IP address with subnet mask in CIDR format. Must be static and free.   |
| Gateway           | 192.168.1.1      | Router or network gateway used for outbound traffic. Here your router's IP.   |
| DNS Server        | 1.1.1.1          | DNS resolver for domain name lookups. Put 8.8.8.8 or 1.1.1.1                  |

[ x ] Pin Interfaces - Checked, Prevents future breakage

You can then complete the install and afterwards, remove the Bottable USB drive and restart your server. It will then display the server's IP which you can then use with port 8006 to access the Proxmox's UI.

Proceeding to the first login, a notification from Proxmox will appear: 

> **No Valid Subscription**</br>
> ⚠️  You do not have a valid subscription for this server...

This pop-up appears because we're using the free Community version of Proxmox without an enterprise key, but it's just a nag screen, not a functional limitation; it encourages paying for support while letting us access all features via community repos. To remove the pop-up, we can edit a JavaScript file (proxmoxlib.js) or use a community script for Proxmox. 

## Promox Community Helper Scripts

Proxmox Community Helper Scripts are a collection of open-source automation tools for Proxmox VE, designed to simplify common tasks like installing applications (e.g., Plex, Jellyfin, Docker) in lightweight LXC containers. They can also help configuring repositories, removing subscription nags, cleaning up old kernels, offering interactive setups and secure defaults for homelabs.
This giant library of curated, safe, community-maintained installers contain scripts that can reduce up to 30–60 minutes of setup into 30 seconds.

