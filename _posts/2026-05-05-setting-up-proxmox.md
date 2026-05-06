---
layout: post
title: "Setting Up Proxmox"
date: 2026-05-05 10:00:00 -0500
tags:
  - Post
  - Homelab
  - Proxmox
featured_image: none
excerpt: >-
  Notes from setting up Proxmox as the next step in my homelab.
---
I've been dabbling with running my own home server for a few years. After my gaming pc started collecting dust for child reasons I wiped it and started experimenting with different Linux distros.

Out of principle (and cheapness) I have a hard time paying Google and Apple for storage space when I have plenty of hard drives sitting around and way more than enough spare compute. I've also run pihole on a raspberry pi in the past. 

I think my first foray into self hosting was running Umbrel to try and host a Bitcoin node. That opened me up to some of the other popular self hosting applications such as Nextcloud and photosphere. I've never been a big docker person and the config required to get the different applications to be able to work together was frustrating enough at the time that I ended up abandoning the project. 

After that I went through a few other iterations. I ran Ubuntu server headless and set up docker containers to run immich, backups through zfs and a raidz. I never trusted my setup enough to start relying on it and again started to abandon it.

Then I tried truenas, but truenas could only run containers. Pihole worked fine, immich worked fine, but it couldn't really share the machine with openclaw in the way I wanted.

In the meantime AI tools started getting better, so I wiped the machine again and set up PopOS with various openclaw adjacent projects. Again they were good, but I think they need the whole computer to get the most use. I also didn't trust using it for anything important while an AI was regularly killing itself and the computer. 

I started a job where I was using vmware virtual machines but the company is switching off of that and over to proxmox for cost reasons so I started experimenting.

Turns out proxmox was the solution I needed. Not sure why I was afraid of VMs before, but the features of proxmox make it the perfect solution. 

Openclaw can be sandboxed but then you really want a vm. Proxmox can run LXC containers so something like pihole takes 5 minutes to setup, while still giving me full VMs for the things that need their own machine. 

A key feature is clones, templates and snapshots. Templates let you set up a machine to a desired state and then nearly instantly spin up as many copies of it as you want to. You can clone running machines but if you have any config that depends on IP address for example you'll end up with conflicts so creating a template is key. 

I put ssh keys in my template as well as some basic configs like the qemu-guest-agent for proxmox to talk nicely to them and some zsh configs.

When I was installing I had two issues i needed to fix. No /boot/ found was flashing on the screen before going to the GRUB(?) menu. Second and more importantly there was some sort of display driver issue that would prevent the installer screen from showing. I had to edit the command that would run on a menu option to include `nomodeset`. 

Once proxmox was installed it was showing me a warning `“No support for hardware accelerated KVM virtualization detected”`. I needed to reboot back into BIOS and enable Intel VT-x.

Another thing was after installing qemu-guest-agent i was running `sudo reboot now` but proxmox still wasn't picking it up. Needed to be cold booted, full shutdown and then full boot and then it picked up ip address and run stats.

Now that I'm set up with a template some of the next things I want to do are:
1. Setup nice domain names in pihole so I can stop memorizing IPs (prox.home, pics.home)
2. New VM for my AI agent
3. Setup immich in a separate VM and see if I can hook it up to the old zfs pools.

I'll try to keep writing as I go, but I have a tendency to skip a few months. 
