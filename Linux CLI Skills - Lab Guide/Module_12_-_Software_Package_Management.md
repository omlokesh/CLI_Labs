Module 12 - Software Package Management


# Exercise 1: Querying Packages



## IMPORTANT COMMANDS


```console
rpm
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Use the `rpm` command to perform the following tasks:


List of all installed packages.



```console
rpm -qa
```



Confirm whether or not the packages `ethtool` and `telnet` are installed.


```console
rpm -q ethtool telnet
```



List the documentation files installed with `grep` package.


```console
rpm -qd grep
```




List configuration files installed with `grep` package.


```console
rpm -qc grep
```




List additional information about the package `grep`.



```console
rpm -qi grep
```


*QUESTION: What license does the installed version of `grep` use?*
*QUESTION: What is the name of the host upon which the package `grep` was built?*




### Step 3

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.







# Exercise 2: Installing and Updating Packages




## IMPORTANT COMMANDS


```console
yum
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Run the command `/usr/local/bin/lab-setup-yum1`.



### Step 3

Use the `yum` command to perform the following tasks:



List all of the packages available to be installed.



```console
yum list available
```



List all of the packages currently installed.



```console
yum list installed
```



Search for keyword `elinks` in package *name* or *summary*.



```console
yum search elinks
```


List informational details regarding the package `elinks`.



```console
yum info elinks
```


Using one command to install the packages and dependencies for both `elinks` and `lftp`.



```console
yum -y install elinks lftp
```


Find the package that provides the file `/etc/passwd` file.



```console
yum provides /etc/passwd
```



Check for available package updates.



```console
yum check-update
```



List available `yum` package groups.



```console
yum groups list
```



Install the package group "Basic Web Server".



```console
yum -y group install "Basic Web Server"
```



### Step 4

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.








# Exercise 3: Configuring a Repository


This exercise is optional.




## IMPORTANT COMMANDS



```console
rpm
```




## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Run this command.


```console
/usr/local/bin/lab-setup-yum2
```



### Step 3

***SCENARIO***

The inexperienced admin strikes again! You get another frantic call from the developer with new `sudo` privileges. This time he accidentally ran `rm -rf ./*` in `/etc/yum.repos.d/` when he meant to be in a different directory.



Identify RPM package that owns files located in `/etc/yum.repos.d/` directory.



```console
rpm -qf /etc/yum.repos.d/Cent*
```


Run verification check on `centos-release` RPM.



```console
rpm -V centos-release
```


Some files are reported as missing. To fix this, reinstall `centos-release` RPM using `rpm` utility.


```console
rpm -ivh --force http://mirror.centos.org/centos-7/7/os/x86_64/Packages/centos-release-7-7.1908.0.el7.centos.x86_64.rpm
```




### Step 4

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.




