Module 14 - Introduction to Security Enhanced Linux


# Exercise 1: View and Changing SELinux Operating Modes




## IMPORTANT COMMANDS



```console
getenforce
setenforce
sestatus
semanage
/etc/selinux/config
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Find the current operating mode of SELinux.



```console
getenforce
```



### Step 3

Find the SELinux mode from config file and loaded policy name.




```console
sestatus
```



### Step 4

Persistently change the SELinux mode to `permissive`.


Edit `/etc/selinux/config`. Ensure `SELINUX` parameter is set to `permissive`.


```ini
SELINUX=permissive
```



### Step 5

Verify the current mode of SELinux is `permissive`.



```console
getenforce
```



### Step 6

Temporarily change the SELinux mode back to `enforcing`.



```console
setenforce 1
getenforce
```

*QUESTION*:  Would changing the mode using `setenforce` persist after a reboot?

*ANSWER*:  No. Changes made with `setenforce` are temporary runtime changes. Persistent changes must be made in `/etc/selinux/config`.




### Step 7

Change the SELinux mode back to `enforcing` in the `/etc/selinux/config` file.




### Step 8

Verify SELinux persistent and runtime status is `enforcing`.



```console
sestatus
```



### Step 9

Notify the instructor when you have completed this lab and are ready to proceed.








# Exercise 2: Changing SELinux File Contexts


This exercise is optional.




## IMPORTANT COMMANDS



```console
semanage
restorecon
```



## Instructions



### Step 1

Log in to the **CentOS7 VM** as `root`.




### Step 2


Run this script.



```console
/usr/local/bin/lab-setup-selinux1
```



### Step 3

Correct any errors as instructed by the script and run the script again until it looks like the example.



***SCENARIO***

There is a web server running on your CentOS7 VM. You can reach this web service through CLI.


```console
curl http://localhost/index.html
```


You received permissions errors. You will need to investigate log files to determine what is causing the error messages. You should see some `sealert` events in `/var/log/messages` indicating SELinux access violations.

Web content is stored in `/web` rather than the default location of `/var/www/html`.



### Step 4

Troubleshoot and fix the issue.


Investigate Apache logs.



```console
grep '/index.html' /var/log/httpd/error_log
```


Verify that Apache service (running as user `apache`) has appropriate UNIX file permissions on `/web/` and its content.



```console
ps -o user,group $(pgrep httpd)
ls -ld /web /web/index.html
```


Verify SELinux security context on `/web/` and `/web/index.html`. As you will see, the SELinux label isn't correct.



```console
ls -lZd /web /web/index.html
```


Verify if there have been any "file context" customizations done to SELinux policy.


```console
semanage fcontext -l -C
```


Create "file context" rule for `/web/` directory and everything inside it.



```console
semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
```


Apply SELinux labels on `/web` using updated SELinux policy.



```console
restorecon -RFv /web
```


Verify if web server responds with the valid web page.


```console
elinks -dump http://localhost/index.html
```






### Step 5

Notify the instructor when you have completed this lab and are ready to proceed.









