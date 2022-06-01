---
layout: post
categories: linux
tags: [disk, format]
excerpt:
  Format a USB drive

---

Insert the disk and then, to identify the attached disks, type

```
sudo fdisk -l
```

The USB device will be listed as `/dev/sdx` or similar, whilst the partition on it will be identified as `/dev/sdx1` or similar.

**Ensure the correct partition is identified; the following action cannot be undone**

Having ensured the correct disk has been identified, the partition can be formatted as FAT16 using this command;

```
sudo mkfs -t fat /dev/sdx1
```
