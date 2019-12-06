Module 05 - Users and Groups


# Exercise 1:  Elevating Privileges and Running Commands as Other Users



## IMPORTANT COMMANDS

```console
man
su
sudo
```


## Instructions


### Step 1

Log in to the **CentOS7 VM** on the first virtual terminal ( `/dev/tty1` )  as `student`.


### Step 2

Run the command `man su` and locate the option that allows you run commands as another user without starting a separate login shell.


*QUESTION*:  When running this command, whose password must you enter when prompted?

```console
su -c "<COMMAND> -opts arg1 arg2" <USER>
```

*ANSWER*:  The password for the `<USER>` account.


### Step 3

Use the `man sudo`. Determine how the behavior of `sudo` is modified by each of the following options.


| Option | Description |
| :--- | :--- |
| `-i` | Simulates an initial login that will process login scripts like `~/.bash_profile` and `~/.bashrc` |
| `-b` | Starts a command in the background (When starting a process “in the background” the password prompt for sudo will not be displayed without the `-b` option) |


### Step 4

Run the command `man -k sudo` to find some of the other manual pages relevant to `sudo`.



### Step 5

Run the command `sudo -i` to become the `root` user.



### Step 6

Run the command `visudo` to edit the file `/etc/sudoers`. `visudo` performs syntax check before allowing to save edited file.



### Step 7

Find the commented line in `/etc/sudoers` which, if uncommented, would allow members of `wheel` group to run any command via `sudo` without password prompt. Copy the commented line, remove the `#` to uncomment it, and change it from the group `wheel` to the user `student`.


Line to find:

```sudo
# %wheel ALL=(ALL) NOPASSWD: ALL
```

Line to add:

```sudo
student ALL=(ALL) NOPASSWD: ALL
```


### Step 8


User can examine his/her SUDO priviliges using option `-l`. In another terminal session, as user `student` run the following command:


```console
sudo -l
```

### Step 9

As user `student` and try to run `sudo -i`. Is user `student` prompted for the password?

```console
sudo -i
```

No. `sudo` configuration files are processed every time user invokes command via `sudo`. It is not necessary for the user to log out in order to take advantage from new SUDO priviliges.






# Exercise 2:  Managing Users and Groups


## IMPORTANT COMMANDS

```console
groupadd
gpasswd
useradd
passwd
usermod
vim
```


### Step 1

Log in to the **CentOS7 VM** as `root`.

***NOTE:  It is important to complete this lab correctly! The `DevOps` group and `tux` user are needed for future lab exercises***

### Step 2


Create a new group called `DevOps` with a `GID` number of 5500.

```console
groupadd --help
groupadd --gid 5500 DevOps
```


### Step 3

Create a new user account with your first name and set the password to a password of your choice. Replace `<myname>` with your actual name.


```console
useradd --help
useradd <myname>
passwd <myname>
```

### Step 4

Create another new user account with the user name of `tux` and set the password to `P@ssw0rd`.


```console
useradd tux
echo "P@ssw0rd" | passwd --stdin tux
```


### Step 5

Add your user account and the `tux` user account to the groups `wheel` and `DevOps`.


This operation could be performed using `usermod`, but better tool for adding and removing users from/to UNIX groups is `gpasswd`. Replace `<myname>` with your actual name.


```console
gpasswd -a <myname> wheel
gpasswd -a <myname> DevOps
gpasswd -a tux wheel
gpasswd -a tux DevOps
```


### Step 6


Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.




# Exercise 3:  Managing Password Aging Policies



## IMPORTANT COMMANDS


```console
groupadd
useradd
passwd
usermod
vim
chage
```


## Instructions


### Step 1

Log in to the **CentOS7 VM** as `root`.



### Step 2

Run the command `chage -l <USERNAME>` to view current password age settings for `student`, `tux`, and `<myname>`. Replace `<myname>` with your actual name.

Example:

```console
chage -l tux
```

If you would like to run `chage -l` command for multiple user accounts that are stored in a file (one username per line), you could write simple BASH loop.


The code below requires `myusers.txt` file in current directory with user account names defined one per line.


```bash
for user in $(cat myusers.txt)
do
    chage -l $user
done
```


### Step 3


Define the following password aging policy for user `student`:

* Maximum Password Age: 90 days 
* Password Expiration Warning: 10 days
* Account Expiration Date: 1 month from today

All the below options could be combined and issued within single invocation for `chage` utility. However, for clarity reasons, each password aging property is modified separately.


```console
chage -M 90 student
chage -W 10 student
chage -E $(date -d "now + 1 month" +%y-%m-%d)
```


### Step 4

Use chage to set the tux user's account to expire January 1 of next year


```console
chage -E $(date -d "next year" +%Y)-01-01 tux
```



### Confirm user `student` and `tux` have correct password aging policy set.


```console
chage -l student
chage -l tux
```



### Step 5

Using VIM or nano editor modify `/etc/login.defs` file. Change `PASS_MAX_DAYS` and `PASS_WARN_AGE` values to reflect the code below.


```console
PASS_MAX_DAYS  60
PASS_WARN_AGE   5
```


### Step 6

Create a new user `harry` with a `GECOS comment` of "H. J. Potter" and `DevOps` and `users` as secondary group memberships. Set the password to `P@ssw0rd`.


```console
useradd --comment "H. J. Potter" --groups DevOps,users harry
echo P@ssw0rd | passwd --stdin harry
```


### Step 7

Run below commands and compare the differences between your account and Harry’s. Replace `<myname>` with your actual name.


```console
chage -l harry
chage -l <myname>
```



### Step 8

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.



