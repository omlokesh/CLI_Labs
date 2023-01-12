Module 08 - Managing Services


# Exercise 1: Using the **SystemD** Init System to Manage Services



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

Enable `iscsid` to start at boot.


```console
systemctl enable iscsid
```



### Step 7

Reboot the VM and log in to a terminal and use either `sudo -i` or `su -l` to become `root` again.




### Step 8

Check the status of the `iscsid` service, then stop and disable it.


```console
systemctl status iscsid
systemctl stop iscsid 
systemctl disable iscsid
```

### Step 9

Notify the instructor when you have completed this lab and are ready to proceed.



