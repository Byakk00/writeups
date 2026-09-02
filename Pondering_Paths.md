
# Challenge 1: The Root

Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

## Solution:

Enter '/pwn' to get the flag.

```sh
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{oPwz2NIGNjHtBPv5i2eEfgS8765.QX4cTO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{oPwz2NIGNjHtBPv5i2eEfgS8765.QX4cTO0wiM1EjNwIzW}
```

### Notes:

Learnt about absolute paths.

***

# Challenge 2: Program and absolute paths

Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

## Solution:

Run run in challenge using '/challenge/run' in prompt and pressing Enter.

```sh
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{I1zr6VZiGi2tCKLdURlEEMMbKMh.QX1QTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{I1zr6VZiGi2tCKLdURlEEMMbKMh.QX1QTN0wiM1EjNwIzW}
```

### Notes:

Learnt to use absolute path of directories inside directories.

***

# Challenge 3: Position thy self

The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```sh
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

## Solution:

'/challenge/run' returns Incorrect in '~' and provides a directory, so we change directory to '/usr/share/doc' using cd and then run '/challenge/run' to capture the flag.

```sh
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/share/doc directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /usr/share/doc
hacker@paths~position-thy-self:/usr/share/doc$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{kt3l5JC010_1QcorR8uMcTnGBgP.QX2QTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{kt3l5JC010_1QcorR8uMcTnGBgP.QX2QTN0wiM1EjNwIzW}
```

### Notes:

Learnt how to change directories.


***

# Challenge 4: Position elsewhere

Same thing, but 5 times!

## Solution:

Repeatedly ran 'challenge/run' for 5 times to receive different directories and cd to them and repeat.

```sh
hacker@paths~position-elsewhere:~$ /challenge/run
Starting level 1.
Incorrect...
You are not currently in the /usr/bin directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /usr/bin
hacker@paths~position-elsewhere:/usr/bin$ /challenge/run
Starting level 1.
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 2
Please use the `cd` utility to change directory to /sys/kernel
hacker@paths~position-elsewhere:/usr/bin$ cd /sys/kernel
hacker@paths~position-elsewhere:/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 3
Please use the `cd` utility to change directory to /etc/apt/sources.list.d
hacker@paths~position-elsewhere:/sys/kernel$ cd /etc/apt/sources.list.d
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 4
Please use the `cd` utility to change directory to /home
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ cd /home
hacker@paths~position-elsewhere:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 5
Please use the `cd` utility to change directory to /usr/share/build-essential
hacker@paths~position-elsewhere:/home$ cd /usr/share/build-essential
hacker@paths~position-elsewhere:/usr/share/build-essential$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4jNCbQ41mr4o-lozIDZj5dpUd9e.QX3QTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{4jNCbQ41mr4o-lozIDZj5dpUd9e.QX3QTN0wiM1EjNwIzW}
```

### Notes:

Learnt how to change multiple directories.


***

# Challenge 5:

[Challenge Description copied from pwn.college]

## Solution:

[Solution]

```sh
$ [Put Code/Bash Commands Here]
```

## Flag: 

```
[Put Flag Here]
```

### Notes:

- [Any Notes You Want To Make Regarding The Challenges]
- [Any Thing You Learned From Solving The Challenge]

### Resources:

- [Any Resources You Used While Solving The Challenge]


***

# Challenge 2: [Challenge Name]

[Challenge Description copied from pwn.college]

## Solution:

[Solution]

```sh
$ [Put Code/Bash Commands Here]
```

## Flag: 

```
[Put Flag Here]
```

### Notes:

- [Any Notes You Want To Make Regarding The Challenges]
- [Any Thing You Learned From Solving The Challenge]

### Resources:

- [Any Resources You Used While Solving The Challenge]


***

# Challenge 1: [Challenge Name]

[Challenge Description copied from pwn.college]

## Solution:

[Solution]

```sh
$ [Put Code/Bash Commands Here]
```

## Flag: 

```
[Put Flag Here]
```

### Notes:

- [Any Notes You Want To Make Regarding The Challenges]
- [Any Thing You Learned From Solving The Challenge]

### Resources:

- [Any Resources You Used While Solving The Challenge]


***

# Challenge 2: [Challenge Name]

[Challenge Description copied from pwn.college]

## Solution:

[Solution]

```sh
$ [Put Code/Bash Commands Here]
```

## Flag: 

```
[Put Flag Here]
```

### Notes:

- [Any Notes You Want To Make Regarding The Challenges]
- [Any Thing You Learned From Solving The Challenge]

### Resources:

- [Any Resources You Used While Solving The Challenge]


***

...
