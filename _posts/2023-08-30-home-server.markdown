---
layout: post
title:  "Home Server - OS Install and Internet Connection"
date:   2023-08-30 19:57:57 -0500
categories: blog post
---
**Building My Own Home Server: The Journey Begins**

For quite some time, I've harbored the ambition to construct my very own home server. The idea of shelling out for Google Drive and iCloud, especially when I have terabytes of hard drives and idle computers gathering dust in my office, feels almost sacrilegious. Why let Google train their AIs on my cherished photos when I can spend my boundless free hours not just "banging my head against the wall," but genuinely relishing the learning curve of Linux, Docker, networking, and more?

**The Motivation: Taking Control of My Photos**

At the heart of this endeavor is my desire for a robust photo storage solution. I aim to liberate all our family photos from the clutches of proprietary storage systems and place them securely in my control. This brings to mind the 3-2-1 backup rule:
- 3 copies of data
- 2 of which are local
- 1 stored offsite

Having two local copies safeguards against unexpected data corruption, while the offsite backup is a shield against calamities like fires.

**Exploring Solutions**

I've dabbled with a few solutions. [Umbrel](www.getumbrel.com) caught my eye due to its user-friendly setup. Initially designed to aid non-techies in establishing Bitcoin nodes, its principles seamlessly extend to other self-hosted applications.

GPT-4 has been an invaluable guide, laying out a plethora of options. Ubuntu Desktop and Windows emerged as frontrunners, courtesy of their user-friendliness and my familiarity with them. On the other hand, Ubuntu Server and openSUSE promised stability, albeit with a slightly steeper learning curve. With GPT-4 as my trusty sidekick, I felt emboldened to venture slightly off the beaten path and opted for Ubuntu Server. The last thing I wanted was Windows' unpredictable updates and restarts. While a GUI wasn't a necessity, I liked knowing I could install one should the need arise.

**The Hurdles: Setting Up Ubuntu Server**

The challenges cropped up almost instantly. After crafting a bootable USB, I installed Ubuntu Server. With four hard drives in the mix, ensuring data integrity was a tad nerve-wracking. The only hiccup so far? A drive with a prior Ubuntu desktop installation displayed some stray files in my home directory. I'm optimistic that this glitch will resolve itself once I delve into the zfs setup.

The real time-drain was the server's reluctance to connect to the internet. While it detected the Wi-Fi card, it likely lacked the requisite drivers. The motherboard's ethernet port was recognized, but plugging in a cable yielded no results. After some troubleshooting, I realized the issue: DHCP wasn't configured to fetch an IP address from the router. The solution? Crafting a `/etc/netplan/99_config.yaml` file with the following content:

```
network:
    version: 2
    renderer: networkd
    ethernets:
        eno2:
            dhcp4: true
```

Here, `eno2` refers to the network adapter linked to the ethernet port, a detail I gleaned after executing `ip addr`.

After saving the file, I ran `sudo netplan apply` followed by a system reboot. A quick `ip addr` confirmed that an IP address was now assigned, and a peek into the router settings corroborated this.

Perhaps, by default, the server version doesn't activate DHCP, assuming users would prefer setting a static address.

This post is already quite lengthy, so I'll delve into other applications in subsequent entries. Stay tuned!