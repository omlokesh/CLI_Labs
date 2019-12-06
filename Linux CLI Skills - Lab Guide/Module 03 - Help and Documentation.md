Module 03 - Help and Documentation


# Exercise 1: Using documentation resources 


## IMPORTANT commands and resources

```console
sosreport
pinfo
man
/usr/share/doc
```


### Step 1

Log in to the **CentOS7 VM** on the first virtual terminal ( `/dev/tty1` )  as `root`.


### Step 2

Generate a SOSReport using the `--batch` option.

```console
sosreport --batch
```



### Step 3

Use `pinfo` utility to to open the Texinfo documentation index and locate for the `wget` network downloader.


*NOTICE: the exact view of Textinfo pages may differ depending on various factors (installed packages, Linux distribution, etc.)*



If `wget` is not installed, run this command:

```console
yum -y install wget
```

Open `wget` Texinfo

```console
pinfo wget
```



### Step 4


Keep the `pinfo` utility open. Navigate to **Invoking** section.



![a3f212b3ca726aafd2b6d289901212fe.png](../_resources/0a30f5fefd5b435b92ef2b26e61836ec.png)


Locate and and navigate to the **Recursive Retrieval Options** node.



![50ddb170f35ada6aa439142ce3de308b.png](../_resources/226a7fd2a5af483f89cfcd3a6f16ed3c.png)


Locate the option for creating a mirror of a site (Look for:  `-m`  or `--mirror`).




![b1af0e5227108cfb5e4d16295e175df6.png](../_resources/19bc6b9882ef483f93165fcc4c5763bc.png)





Use the `p` key to navigate through all the previous nodes, until you return to the **Invoking** section of `wget.info`.


Use the `u` key to navigate up to the top index of the Texinfo documentation.



![29555075c5e4ebb114186b45fbeecd51.png](../_resources/0558c396b3814137a60fa8c582dd30ea.png)



### Step 5

Using the menu items in `coreutils.info` for reference, which commands might you use to:

* output only part of a file’s contents
* view user information
* change file attributes


#### Look for: `Output of parts of files::`
Utilities: `head`, `tail`, `split`, `csplit`



#### Look for: `User information::`
Utilities: `id`, `logname`, `whoami`, `groups`, `users`, `who`



#### Look for: `Changing file attributes::`
Utilities: `chgrp`, `chmod`, `chown`, `touch`



### Step 6

Quit the `pinfo` view by pressing the `q` key.


### Step 7

Find all the manual pages that match the keywords `bash` and `shellgrub`.

```console
man -k grubash
man -k shell
```

### Step 8

Use the command `man man` and find the formatting conventions for the for the SYNOPSIS section of a page.


```console
man man
```

Once inside the man page, type `/SYNOPSIS` and hit `<ENTER>` to find occurence of word `SYNOPSIS` within the page. The search is case-insensitive. To go to the next occurence of matching string type `n`.


Remember the meaning of bold text (**command**), italics (*\<argument\>*), square braces (`[optional_arg]`), ellipses (`[arg]...`), and  pipes (`[-a|-A]`) when using the SYNOPSIS to learn how to effectively use commands.




![9c680ae613a352013048019f52779236.png](../_resources/27eb2e67f6e3498e8564961f0e11b8aa.png)





### Step 9

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.


