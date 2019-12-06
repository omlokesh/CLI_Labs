Module 01 - The Bash Shell



# Exercise 1: Using the BASH Shell


Running Commands and Using Keyboard Shortcuts.


## IMPORTANT COMMANDS



```console
tty
man
pinfo
alias
date
echo
```



## Instructions



### Step 1. 

Log in to the CentOS7 VM on a terminal as user `student` then run `sudo -i` to become user `root`.

### Step 2.

Every user’s shell session is connected to its own special device file (controlling terminal device). Identify the device file for your terminal.


```console
tty
```

*Sample output*

* Local sessions:

```console
/dev/tty1
```

* SSH sessions:

```
 /dev/pts/0
```



### Step 3.

Run the command `man builtins` to find the purpose of each of the following BASH shell builtins: `echo`, `alias`, `umask`, `jobs`, `help`, `history`, `pwd`, `type`.

To display BUILTIN command syntax you can also use `help` command, for example:

```console
help pwd
```


### Step 4.

Run the command `pinfo bash` then navigate (UP, DOWN arrow keys) to **Bash Features::**. Next, select **Aliases::** to read more about how aliases work, how to add and remove them, and which characters cannot be part of a command `alias`. 

 
    
To close `pinfo` utility, type `q`.


    
### Step 5.

Switch to user `root` account (`su -`) and run `alias` command to view all the aliases currently set for the `root` user.


### Step 6.

Log in to another terminal as `student` (e.g. switch to /dev/tty2 by pressing `<CTRL>+<ALT>+<F2>` or open a new GUI terminal).


### Step 7.

Verify which terminal you are logged into by running  tty (e.g.  /dev/tty2 or /dev/pts/1 or similar)


### Step 8.

Run `alias` again as `student`.

***QUESTION:***  Does the student user have the same or different aliases than the root user?


***ANSWER:***  The `student` user has a custom alias called `trythisalias` which runs a BASH shell script located at `/home/student/.CustomizingAliases` that explains how custom per-user aliases are set.


### Step 9.

Options are the key to mastering commands on the CLI. Options change the output of a command, how it operates, or both. On the terminal logged in as student run the command `date --help` and determine which option formats the output of the `date` command to look like each of the following examples:

<br>

Display current date/time using RFC 2822 format

```console
date -R
```

Display current date/time in the form YYYY-MM-DD

```console
date +%F
```

Display current time in the form HH:MM:SS

```console
date +%T
```

The time and date +48 hours from now

```console
date -d "+48 hours"
```


### Step 10.

To practice quoting and escaping and to see how "expansion" is affected, run each of the following commands. Determine which examples expand the `$SHELL` variable or history events, which prints the literal string `$SHELL`, and which generate errors.

Use the BASH shell history feature and CLI navigation shortcuts to reduce the number of keystrokes required to complete each command.


Try these:

```console
<CTRL>+<a> 
<CTRL>+<e>
<CTRL>+<Left Arrow>
<CTRL>+<Right Arrow>
```

**Commands to run:**


*Shell variable expansion.*

```console
echo $SHELL is a variable!
```



*Escaping (`\`) special character `$`. Escaped characters lose their special meaning.*

```console
echo \$SHELL is a variable!
```



*Missing closing `"` or `'` quote causes entering secondary prompt (defined by `PS2` variable). Type `"` and hit ENTER or `<CTRL-C>` to cancel command*

```console
echo "$SHELL is a variable!
```



*When using single quotes (`'`), all characters are treated as literals.*


```console
echo '$SHELL is a variable'
```



*Most things in Linux are case-sensitive, including variable names*


```console
echo "$shell and $SHELL are two different things!"
```



*`!!` in Bash shell is a special variable that stores most recently invoked command*


```console
date
echo Last issued command is: !!
```




### Step 11.

Repeat and/or modify any parts of this lab you feel you need to practice or ask your instructor for additional practice exercises.  Notify the instructor when you have completed this lab and are ready to proceed.


 
 