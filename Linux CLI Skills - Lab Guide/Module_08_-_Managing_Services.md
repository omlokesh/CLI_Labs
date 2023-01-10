Module 08 - Managing Services


# Exercise 1: Using the **SysV** Init System to Manage Services



## IMPORTANT COMMANDS


```console
chkconfig
service
```


## Instructions


### Step 1

Log in to the **CentOS6 VM** as `root`.



### Step 2

Check the status of the `ntpd` service.


```console
service ntpd status
```

*Reference*: `man 8 service` and `service --help`.



### Step 3

Check if the `ntpd` service is set to start at boot.

```console
chkconfig --list ntpd
```

*Rerefence*: `man 8 chkconfig` and `chkconfig --help`.



### Step 4

View ALL services and their settings for each SysV Init run level.


```console
chkconfig --list
```



### Step 5

Run the following command.


```console
ls -l /etc/rc.d/rc3.d/ | grep ntpd > /root/rc3.txt
```

This saves a list of the scripts in `/etc/rc.d/rc3.d/` that contain `ntpd`.



### Step 6

Enable `ntpd` to start at boot.


```console
chkconfig ntpd on
chkconfig --list ntpd
```


### Step 7

Run the following command.


```console
ls -l /etc/rc.d/rc3.d/ | grep ntpd > /root/NEWrc3.txt
```

This saves a new list of scripts in `/etc/rc.d/rc3.d/` that contain `ntpd`.



### Step 8

Compare `/root/rc3.txt` and `/root/NEWrc3.txt` for differences.


```console
diff /root/rc3.txt /root/NEWrc3.txt
```

If you are not familiar with how to read the output of the `diff` command it may be easier to manually compare the differences.

***QUESTION***:  What EXACTLY is different? What did `chkconfig` create in `/etc/rc.d/rc3.d/`?

*NOTE*: Symbolic links in `/etc/rc.d/*` that begin with `S` start a service and those that begin with `K` indicate to stop/kill a service.




### Step 9

Reboot the VM and log in as `root` again.


```console
reboot
```



### Step 10

Check the status of the `ntpd` service then stop and disable it.


```console
service ntpd status
chkconfig ntpd off
service ntpd stop
```

Verify the symbolic link to start the service has been removed from `/etc/rc.d/rc3.d/`.


```console
\ls -l /etc/rc.d/rc3.d/*ntpd
```



### Step 11

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.





# Exercise 2: Using the **SystemD** Init System to Manage Services



## IMPORTANT COMMANDS


```console
systemctl
service
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

View active or failed service units.


```console
systemctl list-units --type service
```

Reference: Use \<TAB\> completion with `systemctl` for options and arguments.



### Step 3

Check the status of the `iscsid` service.


```console
systemctl status iscsid
```




### Step 4

Check if the `iscsid` service is set to start at boot.


```console
systemctl is-enabled iscsid
```



### Step 5


Show service units needed to reach `multi-user.target`.


```console
systemctl list-dependencies multi-user.target --type service
```



### Step 6

Save all the file names in `/etc/systemd/system/multi-user.target.wants` directory to a file named `/root/target.txt`.


```console
ls -l /etc/systemd/system/multi-user.target.wants > /root/target.txt 
```



### Step 7

Enable `iscsid` to start at boot.


```console
systemctl enable iscsid
```



### Step 8

Locate the symbolic link that enables the `iscsid` service.


```console
ls -l /etc/systemd/system/multi-user.target.wants | grep iscsid  
```



### Step 9

Save all the file names in `/etc/systemd/system/multi-user.target.wants` directory to a file named `/root/NEWtarget.txt`.


```console
ls /etc/systemd/system/multi-user.target.wants > /root/NEWtarget.txt
```



### Step 10

Compare `/root/target.txt` and `/root/NEWtarget.txt` for differences.


```console
diff /root/target.txt /root/NEWtarget.txt
```


***QUESTION***:  What EXACTLY is different?  What did the `systemctl` command create in `/etc/systemd/system/multi-user.target.wants/` directory?




### Step 11

Reboot the VM and log in to a terminal and use either `sudo -i` or `su -l` to become `root` again.




### Step 12

Check the status of the `iscsid` service, then stop and disable it.


```console
systemctl status iscsid
systemctl stop iscsid 
systemctl disable iscsid
```



### Step 13

Verify the symbolic link to enable the `iscsid` service has been removed from  `/etc/systemd/system/multi-user.target.wants/`.


```console
ls -l /etc/systemd/system/multi-user.target.wants | grep iscsid
```



### Step 14


Run the `service` and `chkconfig` commands used on CentOS 6 to start, enable, status check, and disable `iscsid`.


```console
service iscsid start
service iscsid status
chkconfig iscsid on
chkconfig --list iscsid
chkconfig iscsid off
chkconfig --list iscsid
```



### Step 15

Verify the symbolic link to enable the `iscsid` service has been removed from  `/etc/systemd/system/multi-user.target.wants/`.


```console
ls -l /etc/systemd/system/multi-user.target.wants | grep iscsid
```



### Step 16

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.



