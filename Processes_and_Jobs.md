
# Challenge 1: Listing Processes

First, we will learn to list running processes using the ps command. Depending on whom you ask, ps either stands for "process snapshot" or "process status", and it lists processes. By default, ps just lists the processes running in your terminal, which honestly isn't very useful:

```sh
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```

In the above example, we have the shell (bash) and the ps process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).

In the majority of cases, this is all that you'll see with a default ps. To make it useful, we need to pass a few arguments.

As ps is a very old utility, its usage is a bit of a mess. There are two ways to specify arguments.

"Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.

"BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.

These two methods, ps -ef and ps aux, result in slightly different, but cross-recognizable output.

Let's try it in the dojo:

```sh
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```

You can see here that there are processes running for the initialization of the challenge environment (docker-init), a timeout before the challenge is automatically terminated to preserve computing resources (sleep 6h to timeout after 6 hours), the VSCode environment (several code-server helper processes), the shell (bash), and my ps -ef command. It's basically the same thing with ps aux:

```sh
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```

There are many commonalities between ps -ef and ps aux: both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND). ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question, while ps aux outputs the percentage of total system CPU and Memory that the process is utilizing. Plus, there's a bunch of other stuff we won't get into right now.

Anyways! Let's practice. In this level, I have once again renamed /challenge/run to a random filename, and this time made it so that you cannot ls the /challenge directory! But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag! Good luck!

NOTE: Both ps -ef and ps aux truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen. If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)! Alternatively, you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation.

## Solution:

Ran 'ps aux' and analyzed all processed to find the right name for '/challenge/run'. Then ran '/challenge/20381-run-1626' to get the flag.

```sh
hacker@processes~listing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.4  0.0   1056   752 ?        Ss   19:21   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/do
root           7  0.2  0.0   7136  2692 ?        S    19:21   0:00 /run/dojo/bin/sleep 6h
root         110  0.0  0.0 232596  3992 ?        S    19:21   0:00 /challenge/20381-run-1626
root         113  0.0  0.0 235016  3416 ?        S    19:21   0:00 sleep 6h
hacker       115  0.3  0.0   4716  3600 pts/0    Ss   19:21   0:00 /nix/store/pkf547jp8a92k4wmxikkyby58w10pysr-bash-interactive-5.3p9/bin/bash /ru
hacker       121  0.0  0.0 232860  4920 pts/0    S+   19:21   0:00 /run/dojo/bin/bash --login
hacker       134  0.2  0.0  37980 22812 ?        Sl   19:21   0:00 /nix/store/nzhm2kbnlpp13kwvk192825y8pykhiag-ttyd-1.7.7/bin/ttyd --port 7681 --i
hacker       136  0.0  0.0 232860  4972 pts/1    Ss   19:21   0:00 /run/dojo/bin/bash --login
hacker       141  0.0  0.0 235228  4400 pts/1    R+   19:21   0:00 ps aux
hacker@processes~listing-processes:~$ /challenge/20381-run-1626
Yahaha, you found me! Here is your flag:
pwn.college{83ZyBN8KAifiMibPP1J3PujW42Y.QX4MDO0wiM1EjNwIzW}
Now I will sleep for a while (so that you could find me with 'ps').
```

## Flag: 

```
pwn.college{83ZyBN8KAifiMibPP1J3PujW42Y.QX4MDO0wiM1EjNwIzW}
```

### Notes:

Learned how ps -ef and ps aux provide different but overlapping views of system processes, and how the ww option prevents command path truncation.

***

# Challenge 2: Killing processes

You've launched processes, you've viewed processes, now you will learn to terminate processes! In Linux, this is done using the aggressively-named kill command. With default options (which is all we'll cover in this level), kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.

Let's say you had a pesky sleep process (sleep is a program that simply hangs out for the number of seconds specified on the commandline, in this case, 1337 seconds) that you launched in another terminal, like so:

```sh
hacker@dojo:~$ sleep 1337
```

How do we get rid of it? You use kill to terminate it by passing the process identifier (the PID from ps) as an argument, like so:

```sh
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```

Now, it's time to terminate your first process! In this challenge, /challenge/run will refuse to run while /challenge/dont_run is running! You must find the dont_run process and kill it. If you fail, pwn.college will disavow all knowledge of your mission. Good luck.

## Solution:

Ran 'ps aux | grep dont_run' to get PID for dont_run, then kill it using 'kill 110'. Finally ran '/challenge/run' to get the flag.

```sh
hacker@processes~killing-processes:~$ ps aux | grep dont_run
hacker       110  0.0  0.0 232596  4032 ?        Ss   19:27   0:00 /challenge/dont_run
hacker       149  0.0  0.0 231628  2716 pts/1    S+   19:28   0:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ kill 110
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{cyHfPtZvUN5ECg_gZF3hL9WT1Bk.QXyQDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{cyHfPtZvUN5ECg_gZF3hL9WT1Bk.QXyQDO0wiM1EjNwIzW}
```

### Notes:

Learned how the kill command terminates a process by targeting its PID and how default signals allow a program to shut down cleanly.

***

# Challenge 3: Interrupting processes

You've learned how to kill other processes with the kill command, but sometimes you just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

Try it here! /challenge/run will refuse to give you the flag until you interrupt it. Good luck!

## Solution:

Ran '/challenge/run' and then Ctrl+C to get the flag by interrupting the process.

```sh
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{A1JqweC6BtfKW5M8l9tZXjiDeYv.QXzQDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{A1JqweC6BtfKW5M8l9tZXjiDeYv.QXzQDO0wiM1EjNwIzW}
```

### Notes:

Learned that Ctrl-C cleanly terminates a process without using the kill command. 

***

# Challenge 4: Killing misbehaving processes

Sometimes, misbehaving processes can interfere with your work. These processes might need to be killed...

In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at /tmp/flag_fifo into which (like in the Practicing Piping FIFO challenge) /challenge/run wants to write your flag. You need to kill this process.

Your general workflow should be:

Check what processes are running.
Find /challenge/decoy in the list and figure out its process ID.
kill it.
Run /challenge/run to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).
Good luck!

NOTE: You might see a few decoy flags show up even after killing the decoy process. This happens because Linux pipes are buffered: conceptually, they have a sort of length through which data flows, and you might kill the decoy process while data is in the pipe. That data, having already entered the pipe, will proceed to the other end (your cat). If you wait a second, you'll see the decoys stop, and then you can /challenge/run and win!

## Solution:

Ran 'ps aux | grep decoy' to get the PID for decoy process and kill it using 'kill 114'. Ran '/challenge/run' in one tab and 'cat /tmp/flag_fifo' in another to get the flag (got multiple decoy flags due to buffered data being delivered, eventually getting the right flag).

```sh
hacker@processes~killing-misbehaving-processes:~$ ps aux | grep decoy
root         113  0.0  0.0   4332  2932 ?        S    19:45   0:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
hacker       114  0.2  0.0  16440 12132 ?        Ss   19:45   0:00 /usr/bin/python3 /challenge/decoy
hacker       143  0.0  0.0 231456  2564 pts/1    R+   19:45   0:00 grep --color=auto decoy
hacker@processes~killing-misbehaving-processes:~$ kill 114
hacker@processes~killing-misbehaving-processes:~$ /challenge/run
Sending the flag to /tmp/flag_fifo!
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
pwn.college{Y3yjOdMujSwxzMxpqK7f8n1nA.g.cTIkwLBD55DKdyCoQbR}
pwn.college{DFcyiqi2VuFdWDBslWLL1fcMps6XwYbVy93L72mKyBH5HNp}
pwn.college{NxQJDVe0yHn2Mr5xRpnGyc-yTRYnv5uE1bSelUmQvTI4guy}
pwn.college{GyX6hDgAtK4ufwOHXgi5I9H2VBh3ymYAXOmuHZfhnMS.2B0}
pwn.college{TjKsXdghxLXcKCl3xviyjes0joDjxXp51GNKHOJ-Ht-5VCo}
pwn.college{MbbZBli1ibHqg3oO9L7JXf.1A5miYx7D-K4COIhNtSOSm05}
pwn.college{dI3yspBPHKcA8oFl0gE.uoxoKpwT6eGmNbA76I4VC-4Qd7P}
pwn.college{TTWykG3XaXPe-.WLYIm1uawEXKd3ftOhdkdAR8psSNS-xtd}
pwn.college{I0cySgMAcHv7A-XmfM8NEPzqzi0.tpzMDnxf1wDpApncu9V}
pwn.college{nqxawxG2fvzejuXwb4mCm5WV18dZ6B8vz3KVlXnMvy5-Xj5}
pwn.college{-z6wWuTosa4zCpyhdLX2DWC0U2HaI-jFKvh.a.-GaFFRM3G}
pwn.college{mOQI6h.bGaZFfrWh-C29fcFwvi0g1RRsAmIET.rqW3Uv.jM}
pwn.college{H0btdy8FaWq2O-mpDdHe6GlS1YCR3Zeejj2hqeeCH0hgZZq}
pwn.college{WmFz8U5B5ZFvV1ayfkuVeGa2k7vEe7Z-zWTKZuRsW4eow9X}
pwn.college{mSsGrWU6bD4ZRgF58bE2VCqFbwuu0SWH2erfMv9VFOMDr66}
pwn.college{I5WxttOXC6Zji-P.rHJ5OGZ1EoVZjLa6jZt9PaqtTCYAHxv}
pwn.college{1a7LbWzZIJoS.GJ.pPV4j-2gaLx7PncE7eQKfF-l0L1Vt0Z}
pwn.college{H0TvKXVl4y3zjY6VHnc-KqrnCUqW80KXSFhV5QjngC80J1U}
pwn.college{sWmruhWG9xshJW5dYifi6Qlt9AdkbPTsuPq4ckDfp0KG83O}
pwn.college{e6cJrREmZFGj.3otukUMeMJWmSZaIYopUAyBDqgt.b-A.Nf}
pwn.college{xkgEnNM5OpoXDtGlkWyCUj04ULDok4.Q-wYnTmyMBEZRao.}
pwn.college{8LqQet71tNsG72nA2xBGPdPaHkyJ.ETR5zYl3kzatPUZdLl}
pwn.college{SvE.QrlfTc9z.dL6m6rH34utlQfoKlBYqkCweCdmnbkX0LX}
pwn.college{UPiV1mYEjqA6NrVK3kZzI6Tp0tRg7YZ6X7ZCjruF3eC7FiJ}
pwn.college{9H-pSTBB5dIC7w.BqxDdxfgK1GJS9mYJ0S20Q7mnvicuhcW}
pwn.college{SqflQXD7qfjBAxvXXXF4us5ofWYvZEqC-8xd-v0foJAWL8j}
pwn.college{NBVnAvHzLcHRFxj7OtODqLgrShL5ieE0I9phvVGDxHzJiSN}
pwn.college{pi-sncjmyOQa8vEXwuNkQbTYyEDDPdBlOlAsq8W1k-EesCn}
pwn.college{YuqgI69DrygTunBNc1VjL3-h460oOWz-uu5.wo5yC8hjwRr}
pwn.college{HrnKswTh2Vh-diWucrkTxXROlVKy3gfwQiLlm5o04Z.IpLu}
pwn.college{ZpC-FbWj-UgOd66tEVIlASGrIPbsSNQX-Ry4YFAXA7CSbqE}
pwn.college{czHrx6QPM5ALS1aQizsseDAC7IM6fxbMz9TE3EIvEild1je}
pwn.college{Kw3YMRqH4a.qfKqAsXmwcEEDX9lKf5SFp3bnKKNc8yqirbI}
pwn.college{Bn7UNef5XXrBE.zJBLGomYLOSzhyt8cTSnUOTE9Sc5ORiET}
pwn.college{Jh9alZ7rpVG-NmrH7GE-.MpMlfAq3VBeUASXSwmkpAaAvHP}
pwn.college{gCb2VoJF1Js76qX--3rGzxAffYWvnYEqGUzAodZOYUscaTg}
pwn.college{Hr5WZ6DYXRX1DxU7RxHnFGllBF5-9FpsZV8aWm9qrky2d0y}
pwn.college{fQsSsq-JujDfT9N9aPRlCMYGCH-b74bE2yYZo2V4APSZo3m}
pwn.college{f8i.nJggCDdzbSvaCXTyHDkkKUUhVg5a77RtO3gFhG5i922}
pwn.college{4SA51nHOstqmSxjSBXKnTAfSUMv8zHBPs76ZoIoSYve.g20}
pwn.college{ny4rLmWS0Y8nqDl5pbLHaloLdVZH94YhwwfKxE-mHjLtZYQ}
pwn.college{HhRv03ruJ3Yi0FCCt6yofAgGfhKHgHZCJMvrf5B0HaSeoMB}
pwn.college{egKk1b9G3yJ5ShTvqfdiqOncEz8bzYkGaSWf-JG757nxeRw}
pwn.college{OUKVe9eJTPBFRV8OixOgGv8Q01aaU-JZrmnwhFZLSnHdBYG}
pwn.college{ys2v99ajKwBCfFoW5b2Az3-Vf-CX0JV3zBi27UvwVmvrXAX}
pwn.college{bINfGdIAWPxNXxogI-zEfUMp0vNLJCdpMzX8nu35hh65OTH}
pwn.college{MbjLUvbLecPzaeE4fUVKa79ammLfZpzBh1g2Z7GI7Y92Zgh}
pwn.college{cJcwuRWTzyTunft4fg.B.BrNXbyFhmOxMkINBC8KsSktB4c}
pwn.college{BIrKuVdKgLOvw7yzprBp4fr35veDSVhRN6iJmRxIxnHJJGG}
pwn.college{Rq.ZPiXHKqlGsaQ4Wm0gms4JaqL.74sezrJJZYzjEeP9LFT}
pwn.college{20Hp1vBD0FHh.lvx594PrWuA9ptyWfpWuw46k34ckuwcpar}
pwn.college{qM-ULuJD29K7CD97R2O3R3rHOV-.M6xcSs0rk3uFskp2hbv}
pwn.college{922HlZsoQZSIpExXbpxGV0IqKAhnk2MVoXNQrddD9WEDZBX}
pwn.college{to3I9LOkFPLwa9VRFkr8RsGrtojEfHG1n4F3AdqHFqKDRl7}
pwn.college{oNGJGUgFlqolaA6.jFAvn6IfIM9lxRiBvfs-699GN21WY8f}
pwn.college{HKydue9Te4FgcydvUix-87SG-tRPTTsi9RUipzIECH-YZqU}
pwn.college{NXUID2bHfet3Ur9UdhKwE-Wf9rgnQX3RFRkZUEAOqgF7h5p}
pwn.college{NL2XkG5g-f6KQIB5cAGin.tVzGcfL2ZOUvvfp3AhzwFzXFi}
pwn.college{LTVj1cuFymz9QzL9sTaEE9D7mPgUI9k6i8qtYXSQENeEQRH}
pwn.college{SkES-wspgbeiYIjq5VCKL1S9Zrw9Y5DEP-AiJx4SE7KAoPp}
pwn.college{qUiduqVh7S0h4UpbUpIefysC2sY8NB7zeHMyvmJ0aFrVGU3}
pwn.college{MHtPBdtWb0uW6L2Jg7N8ruABC6prbMQ4zAx.W78i2XZIJb0}
pwn.college{L1zRqT40Kty.fl3E7c5hWd3iDody5K4KSpOCok-cGSFr59n}
pwn.college{q627oVqODxVSt8tvNhduAVjkk2GGnDNGH.FzHsm7EVWElzv}
pwn.college{HcUR96Sh1HBAbDjzMvCmxc0.EVNeE8zquESEcNpCC7tzhqi}
pwn.college{Z0KmndFrgc4SBHhSaSO6oNjNRP8rvftVAwouy390-M0ad7N}
pwn.college{ncyuDmBoMy.rMWiijMVeFhuly.NpIyLlVPDGJVKjuoKYm1-}
pwn.college{cidwVB-jDSzpOTAfSbZew24dKmLTA4Xf03M3AK2zuQOGXPM}
pwn.college{LTu-CqSRreEvMJdwkQjT6wJisPUZoqPxwz9JD.TEM3f9.I5}
pwn.college{lQ0DtVwXA.W6.54XiytsZ301VY5hIdux7XWsJ6NTG.7RxNU}
pwn.college{NIb.-YsqxoSoWIZW-MRFnTTnjNema7shSpINMa3SvJo93gr}
pwn.college{r9Z0geIM3Dc3W11lFQdYheOqJ6srmSIFzpyV4JaA2FJYk80}
pwn.college{etj04TakrEGodnlg4byZAPAk9dl96ejNCxVNBtndSR-b5XB}
pwn.college{cBbmhzYmxVCPVuSe0xNiwf3ou0VKR-JbCyOGi2AN1G8pHJe}
pwn.college{SOFevMLFtLreuLvm0zAnF9LAkUzT1wcGu1zXSFh-o2rZNzd}
pwn.college{slTDz9dYjyf9.D-UoLDA63w6rJhXSFFUwVL.yrUQDHOUTRl}
pwn.college{nX4jCq-QFotaeo1.HhZ0MhdHJYKqRElRRG3E-lkXlDJMcXR}
pwn.college{ST48-bIzlFkrrJZ1DoCACoXV-qCJ.buNw3CcT2dm-qBdvUg}
pwn.college{p9msCuz7STSf9u-wL66J8h8Uav4elQnOlV0N4hHWkTZSSsX}
pwn.college{zofP4ZMjTLSTpmUzKBmk6amYND6v.EvlzIKf.BNyTW69vIx}
pwn.college{6T4FfJuo84OamBFwHGODb.g0h95ATNY-PMMjhjVJgeKW.dd}
pwn.college{xi0YFrgzW8d9UWB32uoxgRcMEuyPpOzr0svYzxAgwvqu5xX}
pwn.college{HBEacL.YO48RZw.MA0nAJhlMAVUu6-SaedAYmU7yi3xdd0M}
pwn.college{bzlhOM3JEvCxapoRpKX8PBwWYe0lbET-4OwPIfADqL7KDQN}
pwn.college{EJ1523seFNBjdlyvU9MRmXE3cqkEFxW17FwAsGGhf14W76y}
pwn.college{TLTUgrpp79gkxt-dRLcgeD5gheMr.hxkxczNHoLQaXyA3L7}
pwn.college{wK7qKHODqrTDLim7h9lgyLgIwmTH5hWbXhPNBfW-yc0nj13}
pwn.college{FH9Et-USj4rhW.l4Ymm1XzpBjrkOXk6.alpHKPCS6dMX1Yz}
pwn.college{j2LpCXUDfGObSXO3XKvyJIaRvcmW-a9xabyemXTCv-9gy.C}
pwn.college{dec6QbtyRqOqdyquMCmYj66h8NuBhgjNH24SCqauzyv4y7Z}
pwn.college{4P5zA-VPT.Uq3sbGOuHWhGr1dZ.LyWMWWV8QVibHDQrTAwd}
pwn.college{CFTMAY3rYdipbqOLn68CocQVffrFU8YfB21ASsWvb9IJSyO}
pwn.college{zKkWpBrVnjV9g11gF69i-FtL-lQNxoMHCEav6PRKmrHT24v}
pwn.college{NRpSu8TePs9QK2.rSRTDv5eqyO1oDU1T24dspQb8C-i3NbD}
pwn.college{l1Pr5spwAA8lc9XgPNe9oyf3dFZLai.i8xuNDHiR7iiCU3i}
pwn.college{NcMMdkh3dduyxDBuHxqLHx0J0PW3.cprVyJmq5nUFs533vs}
pwn.college{cuz4WMqPPxmyJtqljJJN1s1BTIslyogKd91WLRa5nzFzfbe}
pwn.college{Vl9oyKj0NW-6w4QolsfU7fwzR6iMt9lfbYKlu0b-GqAoJ.S}
pwn.college{ak4hwq.VvN9t2ocKLhkWoRBKYMJ7f4ehyjnL5nKl3guhqwK}
pwn.college{4YUMW9N-8UoH0U7x858BeFj7ty7MBcU8MS3fVr6X6Q-9hHn}
pwn.college{9qf8zptKN1d36e5rFWpUA.ZrOCbKOCSnWVvehLwQjn.GKrr}
pwn.college{wWadwe4iLXXYKtojrowC57rhqbghLetUg54PiIsFIKYnG57}
pwn.college{bNhpdMnAXTn5pMqtZoml3TSf5q5ETFAbmsNleMrKzkkBh99}
pwn.college{D-0dLv47bMdNw1VUutMf01TqDaPQXTgQpbQSHW2p1RnR5o9}
pwn.college{bjsCTow9p1O2xmGqZjS5nARQSH65rAuTi24lXvm3mBGRULn}
pwn.college{Pw0uAxkl8hgqB.lSpUh27q-.s82sythiQYNhWclOxA..aSD}
pwn.college{Fm18Auq6Nl70E5fWuJmp.wwXqPT8UI5yof2rjAKeKcakCyp}
pwn.college{JghO7IaFCt1HVDQEBjzhzpy7usUgxpL4doednaUp08Frdyh}
pwn.college{SsbEU8HHCeBZRNDgdjrtxI2ZOz8Wsk3hW7815C9vEOhw1B4}
pwn.college{XWUOoEme19pgES5H4a7EGNlOSo3ut8O5BAJLRhsni7GDe5L}
pwn.college{5xfb-W9Bet8C7O9knvNUTM6GQytzIWZK6mqdwuzt3fGY8am}
pwn.college{6QiDn.0spJnqPckdnBCLnVBM7rsm3O.MAI4oXc2nqknKT2S}
pwn.college{WBWf8RtQ-PBpxtwqonpdlKpTcqnYCixF6wTZFllYsZTa0XM}
pwn.college{MiPbCBF8GhyXYEcs-VDftMMvIQbqeGYLCLdjBDut9Alt1Ez}
pwn.college{2EOsZhRD6TDIZlSoibgvISQ0nr8crkROy39pgR0NcRiUL91}
pwn.college{zsZVq7b4ZCspFJYBZ11zIgmLeFQSYw3I.AbI01OlJwGF91-}
pwn.college{jzJ5HQsWB3XR2z2LZzCglNKQRyu1HrUBVnmhzhPH1GpiUOS}
pwn.college{cqilSr5irm0di3udzJJfcQUhD1w2l.QGvaM5YURBDj3fGuW}
pwn.college{TIvqjwcgl2vPwrMaPAckGoUdXQoKEXvMN3C2iww3diQfDbY}
pwn.college{3iuq5I7S42aYN-UJYBQdsJC5nPmKpooum8aaVPGlwFauDia}
pwn.college{-UxZDw.cIj.uwboIeU87RgqitYlUC.VvcewHaRkK0dTcm8I}
pwn.college{GwBbKRbBxn1kAdQPOwAoUe.fgWSbq2umyfn6lNS6M7J7YOs}
pwn.college{ium6jlXV6.-OeMDGZbecOtc17Sf09tXIZMbcfNbZ6Olf3fv}
pwn.college{WeShKKPSO0wyOAe6yHmVEGUqERgMx4N-scWBjU7eEBANp3c}
pwn.college{MXY..SYLSKpovi4.Cs4nEzsqVDv83KxSnX43btXvW5qgoHW}
pwn.college{xugUj9PwwBHrThhfKtpaJVC4aDyPMWV-eFqeiOKp7yhA-SA}
pwn.college{wo9VMySEBpeRnxAvRM3MnWq-Pgswa43V.LINaLqXEsAK8T4}
pwn.college{nhcq72IcvA53abBq73c8a0g033jjFxyjddrQjPBGVyRbeQG}
pwn.college{.-3AajMOqWzQSHZxqMQnfpO6CBf84djq5XqGd6Gut8Ocqg5}
pwn.college{mNEFMnWTbF336sgjTtwjOzU9yNQMGQuzCRWC-hCQe7.FS9O}
pwn.college{FNCoZk0Avx-tsHVzYYADppydGK7lb9DmcVR2PDh6Y5NdBDd}
pwn.college{I43r8LUva2VTDjwMFFje8kmvxw2CN4lsdB4.jQ1zcrsmUOI}
pwn.college{6s5C7itc4su8rcmZJl3zjzoq7b5rE7W3DICFyF9bvz0aYJB}
pwn.college{ftCowuz3zAmGP7WcG1Zc5zsqexqxTuaVVWo3Xe6Uv53W7Hx}
pwn.college{8oypAuX54N25SMJFfSPuQNkhMbC.0FNzMDOxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8oypAuX54N25SMJFfSPuQNkhMbC.0FNzMDOxwiM1EjNwIzW}
```

### Notes:

Learned how to identify and terminate specific running processes using their Process ID (PID), and about how Linux pipe buffering works even after a process has been terminated.

***

# Challenge 5: Suspending processes

You have learned to interrupt processes with Ctrl-C, but there are less drastic measures you can use to get your terminal back! You can suspend processes to the background with Ctrl-Z. In this level, we'll explore how this works and, in the next level, we'll figure out how to resume those suspended processes!

This level's run wants to see another copy of itself running and using the same terminal. How? Use the terminal to launch it, then suspend it, then launch another copy while the first is suspended!

## Solution:

Ran '/challenge/run' and suspending it using Ctrl+Z and then again ran '/challenge/run' to get the flag.

```sh
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         122     115  0 19:52 pts/0    00:00:00 /bin/bash 
root         124     122  0 19:52 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         122     115  0 19:52 pts/0    00:00:00 /bin/bash 
root         129     115  0 19:52 pts/0    00:00:00 /bin/bash 
root         131     129  0 19:52 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{MPy5Be9C42v8JShMgL3lUTVk_7I.QX1QDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{MPy5Be9C42v8JShMgL3lUTVk_7I.QX1QDO0wiM1EjNwIzW}
```

### Notes:

Learned that Ctrl-Z sends the SIGTSTP signal, which suspends (stops) a foreground process instead of terminating it.

***

# Challenge 2: Resuming processes

Usually, when you suspend processes, you'll want to resume them at some point. Otherwise, why not just terminate them? To resume processes, your shell provides the fg command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

Go try it out! This challenge's run needs you to suspend it, then resume it. Good luck!

## Solution:

Ran '/challenge/run' to run the process then suspend using Ctrl+Z. Then ran 'fg' to bring '/challenge/run' to foreground.

```sh
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{sePc0YovfEYbSBfSFO4V0m4Ji9_.QX2QDO0wiM1EjNwIzW}
Don't forget to press Enter to quit me!

Goodbye!
```

## Flag: 

```
pwn.college{sePc0YovfEYbSBfSFO4V0m4Ji9_.QX2QDO0wiM1EjNwIzW}
```

### Notes:

Learned how the fg command resumes a suspended job and returns it to the foreground of the terminal.

***

# Challenge 7: Backgrounding processes

You've resumed processes in the foreground with the fg command. You can also resume processes in the background with the bg command! This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

This level's run wants to see another copy of itself running, not suspended, and using the same terminal. How? Use the terminal to launch it, then suspend it, then background it with bg and launch another copy while the first is running in the background!

ARCANUM: If you're interested in some deeper details, check out how to view the differences between suspended and backgrounded properties! Allow me to demonstrate. First, let's suspend a sleep:

```sh
hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
```

The sleep process is now suspended in the background. We can see this with ps by enabling the stat column output with the -o option:

```sh
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```

See that T? That means that the process is suspended due to our Ctrl-Z. The S in bash's STAT column means that bash is sleeping while waiting for input. The R in ps's column means that it's actively running, and the + means that it's in the foreground!

Watch what happens when we resume sleep in the background:

```sh
hacker@dojo:~$ bg
[1]+ sleep 1337 &
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 S    sleep 1337
hacker      1224 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```

Boom! The sleep now has an S. It's sleeping while, well, sleeping, but it's not suspended! It's also in the background and thus doesn't have the +.

## Solution:

Ran '/challenge/run' to run the process then suspend using Ctrl+Z. Then ran 'bg' to bring '/challenge/run' to background. Then again ran '/challenge/run' to get the flag.

```sh
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         120 S+   /bin/bash -p /challenge/run
root         122 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.

hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         120 S    /bin/bash -p /challenge/run
root         130 S    sleep 6h
root         131 S+   /bin/bash -p /challenge/run
root         133 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{s9xOz3lDIPuGOYaYJcBRPw0GbN1.QX3QDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{s9xOz3lDIPuGOYaYJcBRPw0GbN1.QX3QDO0wiM1EjNwIzW}
```

### Notes:

Learned how bg resumes a suspended process and allows it to continue executing in the background without taking over the terminal.

***

# Challenge 8: Foregrounding processes

Imagine that you have a backgrounded process, and you want to mess with it some more. What do you do? Well, you can foreground a backgrounded process with fg just like you foreground a suspended process! This level will walk you through that!

## Solution:

Ran '/challenge/run' to run the process then suspend using Ctrl+Z. Then ran 'bg' to bring '/challenge/run' to background. Then ran 'fg' to bring it to foreground and get the flag.

```sh
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.

hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{Aa7hnaKGY8vVFYa91qSrQE89_3K.QX4QDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{Aa7hnaKGY8vVFYa91qSrQE89_3K.QX4QDO0wiM1EjNwIzW}
```

### Notes:

Learned how fg can foreground not only suspended jobs but also actively running background jobs.

***

# Challenge 9: Starting backgrounded processes

Of course, you don't have to suspend processes to background them: you can start them backgrounded right off the bat! It's easy; all you have to do is append a & to the command, like so:

```sh
hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```

Here, sleep is actively running in the background, not suspended. Now it's your turn to practice! Launch /challenge/run backgrounded for the flag!

## Solution:

Ran '/challenge/run &' to get the flag.

```sh
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 122
hacker@processes~starting-backgrounded-processes:~$ 


Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{wP3LEbwlKWK_Tf7pOb2IRPI-fBT.QX5QDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{wP3LEbwlKWK_Tf7pOb2IRPI-fBT.QX5QDO0wiM1EjNwIzW}
```

### Notes:

Learned that adding & to a command starts it as a background job from the beginning, avoiding the need for Ctrl-Z and bg.

***

# Challenge 10: Process exit codes

Every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates. This can be used by the shell, or the user of the shell (that's you!) to check if the process succeeded in its functionality (this determination, of course, depends on what the process is supposed to do in the first place).

You can access the exit code of the most recently-terminated command using the special ? variable (don't forget to prepend it with $ to read its value!):

```sh
hacker@dojo:~$ touch test-file
hacker@dojo:~$ echo $?
0
hacker@dojo:~$ touch /test-file
touch: cannot touch '/test-file': Permission denied
hacker@dojo:~$ echo $?
1
hacker@dojo:~$
```

As you can see, commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.

In this challenge, you must retrieve the exit code returned by /challenge/get-code and then run /challenge/submit-code with that error code as an argument. Good luck!

## Solution:

Ran '/challenge/get-code' and then 'echo $?' to get the error code. Then ran '/challenge/submit-code 170' to get the flag.

```sh
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
170
hacker@processes~process-exit-codes:~$ /challenge/submit-code 170
CORRECT! Here is your flag:
pwn.college{wCF8t2rH15z4PPZOtNOEFxm0nCu.QX5YDO1wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{wCF8t2rH15z4PPZOtNOEFxm0nCu.QX5YDO1wiM1EjNwIzW}
```

### Notes:

Learned that every command in Linux terminates with an exit code, where 0 typically indicates success and non-zero values indicate failure or special conditions.

***
