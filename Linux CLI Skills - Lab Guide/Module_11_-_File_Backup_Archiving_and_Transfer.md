Module 11 - File Backup, Archiving, and Transfer


# Exercise 1: Using `tar`, `scp`, and `rsync`




## IMPORTANT COMMANDS


```console
tar
scp
rsync
```




## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Explore `tar` compression options.


```console
tar --help | grep -A 15 "Compression"
```




Create a `bzip2` compressed backup of `/etc` and `/var/log`  at `/root/backup.tar.bz2`.



```console
tar -cjf /root/backup.tar.bz2  /etc  /var/log
```



### Step 3

Extract `/root/backup.tar.bz2` into `/tmp/restore/`.


```console
mkdir /tmp/restore
tar -C /tmp/restore/ -xf /root/backup.tar.bz2
```



### Step 4

Use `scp` as the user `root` to send the file to `/root` directory on the RHEL6 host at 192.168.0.100.


```console
scp /root/backup.tar.bz2 root@192.168.0.100:/root/
```




### Step 5

Locate the `sosreport` file created in one of the previous exercise in `/var/tmp`  and extract it in that directory.


*NOTE*: If the file is missing or was never created, create it with `sosreport --batch`.



```console
cd /var/tmp/; tar -xf /var/tmp/sosreport*.tar.xz
```



### Step 6

Use `rsync` to synchronize the contents of the extracted sosreport to `/tmp/sosreport/` on the RHEL6 host at 192.168.0.100.


Refer to `rsync --help` and `man rsync` for help.


***Important***: Pay special attention to how trailing slashes in directory names affect the behavior of `rsync`.



```console
rsync -avz /var/tmp/sosreport-<hostname>-<date> root@192.168.0.100:/tmp/sosreport/
```




### Step 7

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.


