Module 13 - Storage Devices and File Systems


# Exercise 1: Configuring, Formatting, and Mounting Partitions




## IMPORTANT COMMANDS



```console
lsblk
blkid
parted
fdisk
mount
mkswap
swapon
swapoff
man 5 fstab
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Discover all hard disks without partition table.



Show all block devices.

```console
lsblk
```

To determine if disk is used for something (e.g. filesystem) or/and has partition table, use the following utilities.


```console
blkid /dev/sdb
parted /dev/sdb print 2> /dev/null | grep -i 'partition table'
```



### Step 3

Create a 500M partition on the /dev/sdb device. Set the type to `Linux` (83).



```console
fdisk /dev/sdb
```

Within `fdisk` follow these instructions:

* type `p` to print partition table
* type `n` to create new partition
* type `p` to choose primary partition
* type `1` to specify partition number
* type `2048` to specify starting sector for your partition
* type `+500M` to specify ending sector for your partition (fdisk calculates appropriate sector number)
* type `p` to print partition table
* type `w` to save partition table to the disk




### Step 4

Display partition table on `/dev/sdb`.


```console
fdisk -l /dev/sdb
parted /dev/sdb unit s print
```


### Step 5

Format the partition with an XFS file system.



```console
mkfs.xfs /dev/sdb1
```



### Step 6

Confirm the system can recognize XFS (`TYPE=xfs`) filesystem on `/dev/sdb1` device.



```console
blkid /dev/sdb1
```



### Step 7

Mount the new filesystem in `/data` mount point (directory).



```console
mkdir /data
mount /dev/sdb1 /data
```



### Step 8

View all mounted filesystems.


```console
df -hT
```



### Step 9

Create a new 300M swap partition on the same hard disk (`/dev/sdb`), and format it with `mkswap` to create a swap filesystem.  Before and after activating the new swap space, check the current swap configuration with `swapon`.  Then configure the new swap to be activated at boot.


```console
fdisk /dev/sdb
```

Within `fdisk` follow these instructions:

* type `p` to print partition table
* type `n` to create new partition
* type `p` to choose primary partition
* type `2` to specify partition number
* hit ENTER to accept default starting sector
* type `+300M` to specify ending sector for your partition (fdisk calculates appropriate sector number)
* type `t` to change partition type
* type `2` to select 2nd partition
* type `82` to set partition type as "Linux Swap"
* type `p` to print partition table
* type `w` to save partition table to the disk


Because another partition (`/dev/sdb1`) is being used (mounted XFS filesystem) on `/dev/sdb` device, Linux kernel did not refresh its in-memory (`/proc/partitions`) information about available block devices. We need to run `partprobe` command to force kernel to refresh its in-memory block device cache.




```console
lsblk /dev/sdb
partprobe /dev/sdb
lsblk /dev/sdb
```



### Step 10

Format `/dev/sdb2` device as swap.



```console
mkswap /dev/sdb2
```

View information on current amount of swap space and individual swap devices.



```console
free -m
swapon -s
```


Update `/etc/fstab` by referencing additional swap device.


```bash
echo "UUID=$(blkid -o value -s UUID /dev/sdb2) swap swap defaults 0 0" >> /etc/fstab
```


Activate all swap devices defined in `/etc/fstab` file.



```console
swapon -a
```



### Step 11

Notify the instructor when you have completed this lab and are ready to proceed.





# Exercise 2: Working with LVM - Logical Volume Manager




## IMPORTANT COMMANDS



```console
pvs, pvdisplay, pvcreate
vgs, vgdisplay, vgcreate
lvs, lvdisplay, lvcreate
mkfs
mount
blkid
man 5 fstab
```




## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Create an LVM Logical Volume named `DATALV` with a size of 2GB in a new Volume Group named `DATAVG` using `/dev/sdc`, `/dev/sdd` and `/dev/sdd` as Physical Volumes.


When using block devices exclusively for LVM, there's no need to partition the disks.




### Step 3

Create 3 physical volumes.



```console
pvcreate /dev/sd[cde]
pvs
```



### Step 4

Create volume group `DATAVG` using previously formatted physical volumes.



```console
vgcreate DATAVG /dev/sd[cde]
vgs
vgs DATAVG
vgdisplay DATAVG
```



### Step 5

Create logical volume named `DATALV` in `DATAVG` volume group.



```console
lvcreate -n DATALV -L 2G DATAVG
lvs DATAVG
lvdisplay /dev/DATAVG/DATALV
```



### Step 6

Create XFS filesystem on top of `/dev/DATAVG/DATALV` block device that was created by LVM.



```console
mkfs -t xfs /dev/DATAVG/DATALV
blkid /dev/DATAVG/DATALV
```



### Step 7

Ensure that XFS filesystem located on `/dev/DATAVG/DATALV` device is mounted automatically (during system boot) in `/data2` mount point.


*NOTE*: when using LVM, do not use filesystem UUID in `/etc/fstab` file.



```console
echo "/dev/DATAVG/DATALV /data2 xfs defaults 0 0" >> /etc/fstab
mkdir /data2
mount -av
```



### Step 8

Notify the instructor when you have completed this lab and are ready to proceed.







# Exercise 3:  Working with Links and Finding Files




## IMPORTANT COMMANDS



```console
ln
df
find
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** on the first virtual terminal as `root`.



### Step 2

Create a soft link to `/boot/grub2/grub.cfg` called `my_grub`  in `/root/` directory.



```console
ln -s /boot/grub2/grub.cfg /root/my_grub
ls -l /root/my_grub
```



### Step 3

Create a hard link to `/boot/grub2/grub.cfg` called `my_grub2`  in `/root/` directory.



```console
ln /boot/grub2/grub.cfg /root/my_grub2
```


***QUESTION***:  Why did creating a hard link fail?

***ANSWER***:  *"Invalid cross-device link"* means the files are on different filesystems.


```console
df -hT /boot/grub2/grub.cfg
df -hT /root/my_grub2
```





### Step 4

Create a hard link to `/etc/sysconfig/network-scripts/ifcfg-lo`  at `/root/lo-config`. Display inode number of both files.



```console
ln /etc/sysconfig/network-scripts/ifcfg-lo /root/lo-config
ls -il /root/lo-config
```



### Step 5

Use the `find` command to locate all files with the same inode number as `/root/lo-config`.




```console
find / -samefile /root/lo-config
```




### Step 6

Notify the instructor when you have completed this lab and are ready to proceed.


