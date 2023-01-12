Module 02 - The Bash Shell



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

Log into the **`gnome-terminal`** as user *student*.
Then run **`sudo -i`** to become user *root*.

### Step 2.

Type **`tty`** to identify the device file for your terminal.


```console
[student@workstation ~]$ tty
/dev/pts/0
```

### Step 3.

Run the command **`man builtins`** to find the purpose of each of the following BASH shell builtin commands: 
1. `echo` 
2. `alias`
3. `umask`
4. `jobs`
5. `help`
6. `history`
7. `pwd`

### Step 4.
Display a list of all the *BUILTIN* commands with the command **`help`** or **`help | less`**.
Then view the help for the following BUILTINS:
1. `pwd`
2. `cd`
3. `jobs`

```console
help pwd
help cd
help jobs
```


### Step 5.

Run the command **`pinfo bash`** then use the UP and DOWN arrow keys to navigate to **Bash Features::**. 
Next, select **Aliases::** to read more about how aliases work, how to add and remove them, and which characters cannot be part of a command `alias`. 
    
To close `pinfo`, type ***`<q>`***.

    
### Step 6.

Switch to user *root* account by typing **`su -`**. 
Then run **`alias`** to view all the aliases currently set for the *root* user.


### Step 7.

Open another **`gnome-terminal`** window or tab as *student*.
Verify which terminal you are logged into by running  **`tty`** (e.g.  ***/dev/pts/1*** or similar)


### Step 8.

Run **`alias`** again as *student*.

     ***QUESTION:***  Does the *student* user have the same or different aliases than the *root* user?
     ***ANSWER:***  The *student* user has a custom alias called **`trythisalias`** which runs a BASH shell script located at *`/home/student/.CustomizingAliases`* that explains how custom per-user aliases are set.


### Step 9.

     Options are the key to mastering commands on the CLI. 
     Options change the output of a command, how it operates, or both.
     
On the terminal logged in as *student* run the command **`date --help`**. 
Determine which options will format the output of the `date` command to look like each of the following examples:

-----
1. Display current date/time using RFC 2822 format

```console
date -R
```

-----
2. Display current date/time in the form YYYY-MM-DD

```console
date +%F
```

-----
3. Display current time in the form HH:MM:SS

```console
date +%T
```

-----
4. The time and date +48 hours from now

```console
date -d "+48 hours"
```


### Step 10.

To practice quoting and escaping and to see how "expansion" is affected, run each of the following commands. 
Determine which examples expand the `$SHELL` variable or history events, which prints the literal string `$SHELL`, and which generate errors.

Use the BASH shell history feature and CLI navigation shortcuts to reduce the number of keystrokes required to complete each command.  Remember these:
```
<CTRL>+<a>  # Jump to the beginning of the line 
<CTRL>+<e>  # Jump to the end of the line
<CTRL>+<Left Arrow>   # Jump 1 word to the left
<CTRL>+<Right Arrow>  # Jump 1 word to the right
```

**Commands to run:**

1. Shell variable expansion with `$VARNAME`
     
```console
echo $SHELL is a variable!
```

-----
2. Escaping (`\`) special character `$`. Escaped characters lose their special meaning.
     
```console
echo \$SHELL is a variable!
```

-----
3. Missing closing `"` or `'` quote causes entering secondary prompt (defined by `PS2` variable). 
     
```console
echo "$SHELL is a variable!
```

Type `"` and hit **`<ENTER>`** to complete the command or **`<CTRL+c>`** to cancel command*

-----
4. When using single quotes (`'`), all characters are treated as literals.
     
```console
echo '$SHELL is a variable'
```

-----
5. Most things in Linux are case-sensitive, including variable names
     
```console
echo "$shell and $SHELL are two different things."
```

-----
6. BASH performs a "history expansion" of the most recently invoked command when you type `!!`
     
```console
date
echo Last issued command is: !!
```


### Step 11.

Notify the instructor when you have completed this lab and are ready to proceed.
