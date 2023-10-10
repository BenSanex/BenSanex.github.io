---
layout: post
title:  "Home Server - ZFS Setup"
date:   2023-08-31
categories: blog post
tags: [Post, Homelab]
---
So I was wrong about a good chunk of what I wrote yesterday.

I did successfully install ubuntu server, what I didn't realize was that I was not booting to it. There were 3 drives with bootable operating systems installed and the one I wanted to boot into apparently did not support UEFI secure boot.
Why that one didn't like secure boot but the older install of ubuntu server did is a mystery. That's what happens when you just click your way through the install process.

Once I was using the correct OS I had to remove all of the LVM setup and partitions in order to setup my zfs pools.

<!--more-->

##LVM Discovery and Removal
```bash
sudo lvdisplay
```

The reference `ubuntu--vg-ubuntu--lv` indicates that the drive was previously set up with Logical Volume Management (LVM). LVM is a method of allocating space on mass-storage devices that is more flexible than conventional partitioning methods.

In LVM terminology:

- **VG (Volume Group)**: This is a pool of disk space that can be used to create logical volumes. In your case, the volume group is named `ubuntu-vg`.

- **LV (Logical Volume)**: This is a portion of a volume group that has been allocated for a specific purpose. It's analogous to a partition in a traditional disk management setup. In your case, the logical volume is named `ubuntu-lv`.

The double dashes (`--`) in the name are used to escape the single dash (`-`) that is part of the original name. This is a convention in LVM naming.

Here's what you can do to remove the LVM setup:

1. **Display the Logical Volume**:

   ```bash
   sudo lvdisplay
   ```

   This will show details about the logical volume, including its size and the volume group it belongs to.

2. **Deactivate the Logical Volume**:

   ```bash
   sudo lvchange -an /dev/ubuntu-vg/ubuntu-lv
   ```

3. **Remove the Logical Volume**:

   ```bash
   sudo lvremove /dev/ubuntu-vg/ubuntu-lv
   ```

   Confirm the removal when prompted.

4. **Display the Volume Group**:

   ```bash
   sudo vgdisplay
   ```

   This will show details about the volume group.

5. **Remove the Volume Group**:

   ```bash
   sudo vgremove ubuntu-vg
   ```

6. **Display Physical Volumes**:

   ```bash
   sudo pvdisplay
   ```

   This will show the physical volumes that were part of the LVM setup.

7. **Remove the Physical Volume**:

   ```bash
   sudo pvremove /dev/sda
   ```

   Replace `/dev/sda` with the appropriate device name if different.

After these steps, the LVM setup on `/dev/sda` should be completely removed, and you should be able to use `wipefs` without any issues.

**Caution**: These commands will delete the LVM setup and any data stored within the logical volume. Ensure you have backups of any important data before proceeding.

Now when I got to step 7 there was an error message that because the drive was partitioned I could not remove the physical volume with pvremove. I had to run
```bash
sudo fdisk /dev/sda
```
and then press d to delete a partition and then delete 1-3.

##ZFS

Once this was done I was able to setup ZFS. This part was actually extremely simple. There are 2 SSDs and 1 HDD installed in this setup. The SSDs are in a RAIDz pool and then snapshots will be sent to the HDD at some interval to be determined later.

Here's a step-by-step guide:

### 1. Install ZFS:

If you haven't already installed ZFS, do so with:

```bash
sudo apt update
sudo apt install zfsutils-linux
```

### 2. Identify Drives:

Before creating any ZFS pools, identify the drives you want to use:

```bash
sudo fdisk -l
```

Take note of the device names for your SSDs (e.g., `/dev/sda`, `/dev/sdb`).

### 3. Create the ZFS Pool:

Create a RAIDZ pool with your SSDs:

```bash
sudo zpool create mypool raidz /dev/sda /dev/sdb
```

__Note:__ Replace `/dev/sda` and `/dev/sdb` with the appropriate device names for your SSDs.

### 4. Check the Pool Status:

```bash
sudo zpool status mypool
```

### 5. Create a ZFS Filesystem:

You can create a filesystem in your pool:

```bash
sudo zfs create mypool/mydata
```

### 6. Send Snapshots to the Hybrid Drive:

First, identify the device name for your backup drive (e.g., `/dev/sdc`).

Create a separate pool for the drive:

```bash
sudo zpool create backuppool /dev/sdc
```

Now, you can periodically send snapshots from `mypool` to `backuppool`:

```bash
# Create a snapshot
sudo zfs snapshot mypool/mydata@snapshot1

# Send the snapshot to the backup pool
sudo zfs send mypool/mydata@snapshot1 | sudo zfs receive backuppool/mybackup
```

### 7. Automate Snapshots:

You might want to automate the snapshot process. There are tools like `zfs-auto-snapshot` that can help with this.

### Important Notes:

- **Backup Important Data**: Before making any changes, ensure you have backups of any important data. Setting up ZFS pools will erase the data on the drives.
  
- **Monitor Drive Health**: Regularly check the health of your drives using `zpool status`.

- **Performance**: SSDs are great for ZFS due to their speed, especially when it comes to the ZFS Intent Log (ZIL) and the Adaptive Replacement Cache (ARC). However, given that you're using RAIDZ, the performance will be similar to a single SSD.


There isn't anything going into the setup yet, but it should be ready to start receiving backups.