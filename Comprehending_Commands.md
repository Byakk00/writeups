
# Challenge 1: cat: Not the pet, but the command!

One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

```sh
hacker@dojo:~$ cat /path/to/file
Hello Hackers!
```

cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:

```sh
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```

Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!

## Solution:

Used 'cat flag' to get the flag.

```sh
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{4ZENVrEnRNZnOF90K6qd3baP2mj.QXxcTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{4ZENVrEnRNZnOF90K6qd3baP2mj.QXxcTN0wiM1EjNwIzW}
```

### Notes:

Learnt about the cat command.

***

# Challenge 2: Catting absolute paths

In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

```sh
hacker@dojo:~$ cat /path/to/file
Hello Hackers!
```

In this challenge, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## Solution:

Used 'cat /flag' to capture flag from /flag.

```sh
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{8-mXWjfRxe-IZ20fCMODneLjJ3V.QX5ETO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8-mXWjfRxe-IZ20fCMODneLjJ3V.QX5ETO0wiM1EjNwIzW}
```

### Notes:

Learnt to use absolute paths with cat command.

***

# Challenge 3: More catting practice

You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

## Solution:

Used 'cat PATH' where the given PATH was usr/games/flag.

```sh
hacker@commands~more-catting-practice:~$ cat /usr/games/flag
pwn.college{g_uDCdMhjuP7Tw1IYLx6P99_2vZ.QXwITO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{g_uDCdMhjuP7Tw1IYLx6P99_2vZ.QXwITO0wiM1EjNwIzW}
```

### Notes:

Learned how absolute paths allow files to be accessed from anywhere in the filesystem without needing to change the current working directory. Reinforced the difference between absolute and relative paths, and understood that commands like cat can directly access files using their full location.

***

# Challenge 4: Grepping for a needle in a haystack

Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

```sh
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

## Solution:

Since the file has hundred thousand lines of text, we need just the flag so used 'grep pwn.college /challenge/data.txt'.

```sh
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{Qv3Vo5suEPoa4nTegD_LtqW6yvj.QX3EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{Qv3Vo5suEPoa4nTegD_LtqW6yvj.QX3EDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to use the grep command.

***

# Challenge 5: Comparing files

When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:

```sh
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```

The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

```sh
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

- /challenge/decoys_only.txt contains 100 fake flags
- /challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
Use diff to find what's different between these files and get your flag!

## Solution:

Used the diff command with the two given paths to find the added flag in the second file path.

```sh
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
75a76
> pwn.college{03jZYMslQpUQVrkJux4RifMJygo.01MwMDOxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{03jZYMslQpUQVrkJux4RifMJygo.01MwMDOxwiM1EjNwIzW}
```

### Notes:

Learnt how to use the diff command.

***

# Challenge 6: Listing files

So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

```sh
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it. Then invoke the discovered absolute path to get the flag.

## Solution:

Used 'ls' in '/challenge' to find the content inside it, then ran /challenge/file (where file is renamed file name) to get the flag.

```sh
hacker@commands~listing-files:~$ ls /challenge
28628-renamed-run-17229  Dockerfile
hacker@commands~listing-files:~$ /challenge/28628-renamed-run-17229
Yahaha, you found me! Here is your flag:
pwn.college{sMN7LUXHhUaqBGP7vukPeyC5rXr.QX4IDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{sMN7LUXHhUaqBGP7vukPeyC5rXr.QX4IDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to use the list (ls) command.

***

# Challenge 7: Touching files

Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

## Solution:

Used 'touch' to create 'pwn' and 'college' in '/tmp' and then run '/challenge/run' to get the flag.

```sh
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{8la-IvoDoUGwTjL89hBlAmTFW89.QXwMDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8la-IvoDoUGwTjL89hBlAmTFW89.QXwMDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to use the touch command.

***

# Challenge 8: Removing files

Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:

```sh
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

## Solution:

Used the 'ls' command to list the home directory and check if delete_me file exists there, then used the 'rm' command to delete that file and ran '/challenge/check' to get the flag.

```sh
hacker@commands~removing-files:~$ ls
a  delete_me
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{s6IqOygpoPFq3rm9tqOA-5Fe-Tf.QX2kDM1wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{s6IqOygpoPFq3rm9tqOA-5Fe-Tf.QX2kDM1wiM1EjNwIzW}
```

### Notes:

Learnt how to use to rm command.

***

# Challenge 9: Moving files

You can also move files around with the mv command. The usage is simple:

```sh
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! Note, you must use the mv command rather than other methods (such as renaming the file in VSCode). When you're done, run /challenge/check, which will check things out and give the flag to you.

## Solution:

Used the 'mv' command to move the '/flag' file into '/tmp/hack-the-planet' file, then ran '/challenge/check' to get the flag.

```sh
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{4ktLu0Kd9EnI7VfNIoBnRJNAacD.0VOxEzNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{4ktLu0Kd9EnI7VfNIoBnRJNAacD.0VOxEzNxwiM1EjNwIzW}
```

### Notes:

Learnt how to use the mv command, and that it can also rename files.

***

# Challenge 10: Copying files

But what if you want to keep the original file? You can do so with the cp command. The usage is the same as with mv, but it will keep the source file. The command is cp SOURCE DESTINATION: the first argument is the existing file, and the second is where the copy should be created.

This challenge wants you to copy the /flag file to /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

NOTE: When a cp destination is a directory, cp places the copy inside it using the source file's name. For this challenge, /tmp/hack-the-planet should name the copied file itself, rather than an existing directory.

## Solution:

Used the 'cp' command to copy the '/flag' file into '/tmp/hack-the-planet' file, then ran '/challenge/check' to get the flag.

```sh
hacker@commands~copying-files:~$ cp /flag /tmp/hack-the-planet
Correct! Performing 'cp /flag /tmp/hack-the-planet'.
hacker@commands~copying-files:~$ /challenge/check
Congrats! You successfully copied the flag to /tmp/hack-the-planet! Here it is:
pwn.college{sXYbUwwTwjKDrN-_p_RfZGjQfGd.0lNxQTMywiM1EjNwIzW}
```

## Flag: 

```
pwn.college{sXYbUwwTwjKDrN-_p_RfZGjQfGd.0lNxQTMywiM1EjNwIzW}
```

### Notes:

Learnt how to use the cp command.

***
# Challenge 11: Hidden files

Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:

```sh
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.

## Solution:

Firstly 'cd' to '/' as per the task given. Then ran 'ls' with '-a' argument to see all files, finally using 'cat' on '.flag-32198303106611' to get the flag.

```sh
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    media  nix  proc  run   srv  tmp  var
..  .flag-32198303106611  boot  dev        home  lib64  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat .flag-32198303106611
pwn.college{ozytXxM5OAXXqRngJqB4dKhZZRK.QXwUDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{ozytXxM5OAXXqRngJqB4dKhZZRK.QXwUDO0wiM1EjNwIzW}
```

### Notes:

Learned that Linux treats files beginning with a dot (.) as hidden files, causing them to be excluded from normal ls output and the use of the -a flag with ls to display all files, including hidden ones.

***

# Challenge 12: An Epic Filesystem Quest

With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:

hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

0. Your first clue is in /. Head on over there.
1. Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
2. cat that file to read the clue!
3. Depending on what the clue says, head on over to the next directory (or don't!).
4. Follow the clues to the flag!

Good luck!

## Solution:

Used 'cd /' to start the quest. Then followed clues using previously learnt commands to get new clues and finally getting the flag.

```sh
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
SECRET  boot       dev  flag  lib    media  nix  proc  run   srv  tmp  var
bin     challenge  etc  home  lib64  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat SECRET
Great sleuthing!
The next clue is in: /usr/share/locale/ta

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/locale/ta
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ta$ ls
EVIDENCE  LC_TIME
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ta$ cat EVIDENCE
Yahaha, you found me!
The next clue is in: /usr/lib/x86_64-linux-gnu/perl/5.38.2/auto/B

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ta$ ls /usr/lib/x86_64-linux-gnu/perl/5.38.2/auto/B
B.so  HINT-TRAPPED
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ta$ cat /usr/lib/x86_64-linux-gnu/perl/5.38.2/auto/B/HINT-TRAPPED
Yahaha, you found me!
The next clue is in: /usr/share/doc/patch

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ta$ cd /usr/share/doc/patch
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/patch$ ls
AUTHORS  NEWS.gz  README  TEASER  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/patch$ cat TEASER
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/patch$ cd /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls$ ls
LEAD                        getgroups32.asm             olduname.asm                      setreuid32.asm
__doc__                     getitimer.asm               open.asm                          setrlimit.asm
_llseek.asm                 getpeername.asm             open_by_handle_at.asm             setsid.asm
_newselect.asm              getpgid.asm                 open_tree.asm                     setsockopt.asm
_sysctl.asm                 getpgrp.asm                 openat.asm                        settimeofday.asm
accept.asm                  getpid.asm                  openat2.asm                       setuid.asm
accept4.asm                 getpmsg.asm                 pause.asm                         setuid32.asm
access.asm                  getppid.asm                 pciconfig_iobase.asm              setxattr.asm
acct.asm                    getpriority.asm             pciconfig_read.asm                sgetmask.asm
add_key.asm                 getrandom.asm               pciconfig_write.asm               shmat.asm
adjtimex.asm                getresgid.asm               perf_event_open.asm               shmctl.asm
afs_syscall.asm             getresgid32.asm             personality.asm                   shmdt.asm
alarm.asm                   getresuid.asm               pidfd_getfd.asm                   shmget.asm
arch_prctl.asm              getresuid32.asm             pidfd_open.asm                    shutdown.asm
arch_specific_syscall.asm   getrlimit.asm               pidfd_send_signal.asm             sigaction.asm
arm_fadvise64_64.asm        getrusage.asm               pipe.asm                          sigaltstack.asm
arm_sync_file_range.asm     getsid.asm                  pipe2.asm                         signal.asm
bdflush.asm                 getsockname.asm             pivot_root.asm                    signalfd.asm
bind.asm                    getsockopt.asm              pkey_alloc.asm                    signalfd4.asm
bpf.asm                     gettid.asm                  pkey_free.asm                     sigpending.asm
break_.asm                  gettimeofday.asm            pkey_mprotect.asm                 sigprocmask.asm
brk.asm                     getuid.asm                  poll.asm                          sigqueueinfo.asm
cachectl.asm                getuid32.asm                ppoll.asm                         sigreturn.asm
cacheflush.asm              getxattr.asm                ppoll_time64.asm                  sigsuspend.asm
capget.asm                  gtty.asm                    prctl.asm                         sigtimedwait.asm
capset.asm                  ia32_arch_prctl.asm         pread.asm                         sigtimedwait_time64.asm
chdir.asm                   ia32_io_pgetevents.asm      pread64.asm                       socket.asm
chmod.asm                   ia32_rseq.asm               preadv.asm                        socketcall.asm
chown.asm                   ia32_statx.asm              preadv2.asm                       socketcall_accept.asm
chown32.asm                 idle.asm                    prlimit64.asm                     socketcall_bind.asm
chroot.asm                  init_module.asm             process_vm_readv.asm              socketcall_connect.asm
clock_adjtime.asm           inotify_add_watch.asm       process_vm_writev.asm             socketcall_getpeername.asm
clock_adjtime64.asm         inotify_init.asm            prof.asm                          socketcall_getsockname.asm
clock_getres.asm            inotify_init1.asm           profil.asm                        socketcall_getsockopt.asm
clock_getres_time64.asm     inotify_rm_watch.asm        pselect6.asm                      socketcall_listen.asm
clock_gettime.asm           io_cancel.asm               pselect6_time64.asm               socketcall_recv.asm
clock_gettime64.asm         io_destroy.asm              ptrace.asm                        socketcall_recvfrom.asm
clock_nanosleep.asm         io_getevents.asm            putpmsg.asm                       socketcall_recvmsg.asm
clock_nanosleep_time64.asm  io_pgetevents.asm           pwrite.asm                        socketcall_send.asm
clock_settime.asm           io_pgetevents_time64.asm    pwrite64.asm                      socketcall_sendmsg.asm
clock_settime64.asm         io_setup.asm                pwritev.asm                       socketcall_sendto.asm
clone.asm                   io_submit.asm               pwritev2.asm                      socketcall_setsockopt.asm
clone3.asm                  io_uring_enter.asm          query_module.asm                  socketcall_shutdown.asm
close.asm                   io_uring_register.asm       quotactl.asm                      socketcall_socket.asm
connect.asm                 io_uring_setup.asm          read.asm                          socketcall_socketpair.asm
copy_file_range.asm         ioctl.asm                   readahead.asm                     socketpair.asm
creat.asm                   ioperm.asm                  readdir.asm                       splice.asm
create_module.asm           iopl.asm                    readlink.asm                      ssetmask.asm
delete_module.asm           ioprio_get.asm              readlinkat.asm                    stat.asm
dup.asm                     ioprio_set.asm              readv.asm                         stat64.asm
dup2.asm                    ipc.asm                     reboot.asm                        statfs.asm
dup3.asm                    kcmp.asm                    recv.asm                          statfs64.asm
epoll_create.asm            kexec_file_load.asm         recvfrom.asm                      statx.asm
epoll_create1.asm           kexec_load.asm              recvmmsg.asm                      stime.asm
epoll_ctl.asm               keyctl.asm                  recvmmsg_time64.asm               stty.asm
epoll_ctl_old.asm           kill.asm                    recvmsg.asm                       swapoff.asm
epoll_pwait.asm             lchown.asm                  remap_file_pages.asm              swapon.asm
epoll_wait.asm              lchown32.asm                removexattr.asm                   symlink.asm
epoll_wait_old.asm          lgetxattr.asm               rename.asm                        symlinkat.asm
eventfd.asm                 link.asm                    renameat.asm                      sync.asm
eventfd2.asm                linkat.asm                  renameat2.asm                     sync_file_range.asm
execve.asm                  listen.asm                  request_key.asm                   sync_file_range2.asm
execveat.asm                listxattr.asm               reserved221.asm                   syncfs.asm
exit.asm                    llistxattr.asm              reserved82.asm                    sys_kexec_load.asm
exit_group.asm              lock.asm                    restart_syscall.asm               syscall.asm
faccessat.asm               lookup_dcookie.asm          rmdir.asm                         sysfs.asm
fadvise64.asm               lremovexattr.asm            rseq.asm                          sysinfo.asm
fadvise64_64.asm            lseek.asm                   sched_get_priority_max.asm        syslog.asm
fallocate.asm               lsetxattr.asm               sched_get_priority_min.asm        sysmips.asm
fanotify_init.asm           lstat.asm                   sched_getaffinity.asm             tee.asm
fanotify_mark.asm           lstat64.asm                 sched_getattr.asm                 tgkill.asm
fchdir.asm                  madvise.asm                 sched_getparam.asm                tgsigqueueinfo.asm
fchmod.asm                  madvise1.asm                sched_getscheduler.asm            time.asm
fchmodat.asm                mbind.asm                   sched_rr_get_interval.asm         timer_create.asm
fchown.asm                  membarrier.asm              sched_rr_get_interval_time64.asm  timer_delete.asm
fchown32.asm                memfd_create.asm            sched_setaffinity.asm             timer_getoverrun.asm
fchownat.asm                migrate_pages.asm           sched_setattr.asm                 timer_gettime.asm
fcntl.asm                   mincore.asm                 sched_setparam.asm                timer_gettime64.asm
fcntl64.asm                 mkdir.asm                   sched_setscheduler.asm            timer_settime.asm
fdatasync.asm               mkdirat.asm                 sched_yield.asm                   timer_settime64.asm
fgetxattr.asm               mknod.asm                   seccomp.asm                       timerfd.asm
finit_module.asm            mknodat.asm                 security.asm                      timerfd_create.asm
flistxattr.asm              mlock.asm                   select.asm                        timerfd_gettime.asm
flock.asm                   mlock2.asm                  semctl.asm                        timerfd_gettime64.asm
fork.asm                    mlockall.asm                semget.asm                        timerfd_settime.asm
fremovexattr.asm            mmap.asm                    semop.asm                         timerfd_settime64.asm
fsconfig.asm                mmap2.asm                   semtimedop.asm                    times.asm
fsetxattr.asm               modify_ldt.asm              semtimedop_time64.asm             tkill.asm
fsmount.asm                 mount.asm                   send.asm                          truncate.asm
fsopen.asm                  move_mount.asm              sendfile.asm                      truncate64.asm
fspick.asm                  move_pages.asm              sendfile64.asm                    tuxcall.asm
fstat.asm                   mprotect.asm                sendmmsg.asm                      ugetrlimit.asm
fstat64.asm                 mpx.asm                     sendmsg.asm                       ulimit.asm
fstatat.asm                 mq_getsetattr.asm           sendto.asm                        umask.asm
fstatat64.asm               mq_notify.asm               set_mempolicy.asm                 umount.asm
fstatfs.asm                 mq_open.asm                 set_robust_list.asm               umount2.asm
fstatfs64.asm               mq_timedreceive.asm         set_thread_area.asm               uname.asm
fsync.asm                   mq_timedreceive_time64.asm  set_tid_address.asm               unlink.asm
ftime.asm                   mq_timedsend.asm            setdomainname.asm                 unlinkat.asm
ftruncate.asm               mq_timedsend_time64.asm     setfsgid.asm                      unshare.asm
ftruncate64.asm             mq_unlink.asm               setfsgid32.asm                    uselib.asm
futex.asm                   mremap.asm                  setfsuid.asm                      userfaultfd.asm
futex_time64.asm            msgctl.asm                  setfsuid32.asm                    ustat.asm
futimesat.asm               msgget.asm                  setgid.asm                        utime.asm
get_kernel_syms.asm         msgrcv.asm                  setgid32.asm                      utimensat.asm
get_mempolicy.asm           msgsnd.asm                  setgroups.asm                     utimensat_time64.asm
get_robust_list.asm         msync.asm                   setgroups32.asm                   utimes.asm
get_thread_area.asm         munlock.asm                 sethostname.asm                   vfork.asm
getcpu.asm                  munlockall.asm              setitimer.asm                     vhangup.asm
getcwd.asm                  munmap.asm                  setns.asm                         vm86.asm
getdents.asm                name_to_handle_at.asm       setpgid.asm                       vm86old.asm
getdents64.asm              nanosleep.asm               setpriority.asm                   vmsplice.asm
getegid.asm                 newfstatat.asm              setregid.asm                      vserver.asm
getegid32.asm               nfsservctl.asm              setregid32.asm                    wait4.asm
geteuid.asm                 nice.asm                    setresgid.asm                     waitid.asm
geteuid32.asm               oldfstat.asm                setresgid32.asm                   waitpid.asm
getgid.asm                  oldlstat.asm                setresuid.asm                     write.asm
getgid32.asm                oldolduname.asm             setresuid32.asm                   writev.asm
getgroups.asm               oldstat.asm                 setreuid.asm
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls$ cat LEAD
Congratulations, you found the clue!
The next clue is in: /usr/share/locale/ast/LC_MESSAGES

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls$ ls -a /usr/share/locale/ast/LC_MESSAGES
.  ..  .TIP  apt.mo  dpkg.mo  libapt-pkg6.0.mo
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/aarch64/linux/syscalls$ cd /usr/share/locale/ast/LC_MESSAGES
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ast/LC_MESSAGES$ cat .TIP
Congratulations, you found the clue!
The next clue is in: /usr/include/misc
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/ast/LC_MESSAGES$ cd /usr/include/misc
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ ls
SNIPPET  cxl.h  fastrpc.h  ocxl.h  pvpanic.h  uacce  xilinx_sdfec.h
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ cat SNIPPET
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/thumb/freebsd

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ ls /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/thumb/freebsd
TRACE-TRAPPED  __doc__  syscall.asm
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ cat /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/thumb/freebsd/TRACE-TRAPPED
Lucky listing!
The next clue is in: /usr/share/base-passwd

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ ls /usr/share/base-passwd
NOTE-TRAPPED  group.master  passwd.master
hacker@commands~an-epic-filesystem-quest:/usr/include/misc$ cat /usr/share/base-passwd/NOTE-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{MH5XFKOczZw_QajlF6ND1IncncZ.QX5IDO0wiM1EjNwIzW}
```

## Flag: 

```
It is: pwn.college{MH5XFKOczZw_QajlF6ND1IncncZ.QX5IDO0wiM1EjNwIzW}
```

### Notes:

Reinforced the use of cd, ls, ls -a, and cat for discovering files, reading clues, and traversing directories. Also gained experience handling special challenge conditions such as hidden files, delayed clues that require entering a directory, and trapped clues that must be accessed through absolute paths without changing directories.

***

# Challenge 13: Making directories

We can create files. How about directories? You make directories using the mkdir command. Then you can stick files in there!

Watch:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```

Now, go forth and create a /tmp/pwn directory and make a college file in it! Then run /challenge/run, which will check your solution and give you the flag!

## Solution:

Used 'mkdir /tmp/pwn' to create the directory and then used 'touch /tmp/pwn/college' to create the file. Finally ran '/challenge/run' to get the flag.

```sh
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ touch /tmp/pwn/college
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{AexQZST3XAoSD8ys-E4d-AI1OHr.QXxMDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{AexQZST3XAoSD8ys-E4d-AI1OHr.QXxMDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to use the mkdir command.

***

# Challenge 14: Finding files

So now we know how to list, read, and create files. But how do we find them? We use the find command!

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). For example:

```sh
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```

And when specifying the search location:

```sh
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```

And, of course, we can specify the criteria! For example, here, we filter by name:

```sh
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```

You can search the whole filesystem if you want!

```sh
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```

Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called flag. Go find it!

Several notes. First, there are other files named flag on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause find to generate errors, but you can ignore those; we won't hide the flag there! Finally, find can take a while; be patient!

## Solution:

Used 'find / -name flag' to find flag and then 'cat /' to get the flag.

```sh
hacker@commands~finding-files:~$ find / -name flag
find: ‘/etc/ssl/private’: Permission denied
/usr/lib/python3/dist-packages/pwnlib/flag
/usr/share/man/uk/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/root’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/nix/store/ka6xbd6z6wj5d6frl7ym4nzfc6p2wkdx-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/f31j0igg7ms3yrj5gm3cm76bjcmdl8w5-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/n6vb30rd7kkwjj595pgm0dmsmfaqi6i5-rizin-0.7.3/share/rizin/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/8qvj9mzdq2qxgjigw4ysqgbkcx1zi80y-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/dz2qxywk6d8hc1gkarpwbhyxb50sh2ak-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/c07wba3nrck81kdh0yg5h8rx22di35xi-radare2-6.0.4/share/radare2/6.0.4/flag
/nix/store/gfyhjlxav9nczmnanb3jxr73kb22yp42-rizin-0.8.1/share/rizin/flag
/nix/store/61dd247b72i7xnm0mw9qaxgfx3gs2lyy-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/sh1s72wwgvcq50kp830nlhm5cjpxmyh7-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/1wn496frzskd2drjwyyskk3g50rd1nbd-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/rszkfmr2mp5r4dyvhwqcj3521nyqfyzc-rizin-0.8.2/share/rizin/flag
/nix/store/kdlmh9h9hmq225jarh6rk927lb7jsxsv-radare2-6.1.8/share/radare2/6.1.8/flag
/nix/store/p9vjrnqyl7hy1k0ik9dw0lb9ib3c4582-python3.13-pwntools-4.15.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/f42x3k5mrk3qq79ixwy991p6g6a5l9f6-python3.13-pwntools-4.15.0/lib/python3.13/site-packages/pwnlib/flag
/nix/store/hss94rqc4ha0y229f8fwcy304wnzdsq7-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ cat /usr/lib/python3/dist-packages/pwnlib/flag
cat: /usr/lib/python3/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/share/man/uk/flag
pwn.college{g4sd6ED6mWPynxnGz8LuhbKpYkI.QXyMDO0wiM1EjNwIzW}
hacker@commands~finding-files:~$
```

## Flag: 

```
pwn.college{g4sd6ED6mWPynxnGz8LuhbKpYkI.QXyMDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to use the 'find' command to search for files across the filesystem based on specific criteria. Reinforced that 'find' can start searching from any directory and that the -name option filters results by filename. Also gained experience dealing with permission-denied errors, understanding that inaccessible directories do not prevent find from continuing its search elsewhere.

***
# Challenge 15: Linking files

If you use Linux (or computers) for any reasonable length of time to do any real work, you will eventually run into some variant of the following situation: you want two programs to access the same data, but the programs expect that data to be in two different locations. Luckily, Linux provides a solution to this quandary: links.

Links come in two flavors: hard and soft (also known as symbolic) links. We'll differentiate the two with an analogy:

- A hard link is when you address your apartment using multiple addresses that all lead directly to the same place (e.g., Apt 2 vs Unit 2).
- A soft link is when you move apartments and have the postal service automatically forward your mail from your old place to your new place.

In a filesystem, a file is, conceptually, an address at which the contents of that file live. A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data. A soft/symbolic link, instead, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file. In most cases, both situations result in accessing the original data, but the mechanisms are different.

Hard links sound simpler to most people (case in point, I explained it in one sentence above, versus two for soft links), but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.

In this challenge, we will learn about symbolic links (also known as symlinks). Symbolic links are created with the ln command using the syntax ln -s TARGET LINK_NAME. TARGET is the path that the link will point to, and LINK_NAME is the new path you are creating. For example:

```sh
hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
```

You can see that accessing the symlink results in getting the original file contents! In this example, /tmp/myfile is the target and /home/hacker/ourfile is the link name.

A symlink can be identified as such with a few methods. For example, the file command, which takes a filename and tells you what type of file it is, will recognize symlinks:

```sh
hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
```

Okay, now you try it! In this level the flag is, as always, in /flag, but /challenge/catflag will instead read out /home/hacker/not-the-flag. The path /home/hacker/not-the-flag is the link name in this challenge. Choose the target that will fool /challenge/catflag into giving you the flag!

WARNING: If a previous experiment left something at /home/hacker/not-the-flag, remove it first so ln can create the symbolic link there.

## Solution:

Used 'ln -s /flag ~/not-the-flag' to link files and then run '/challenge/catflag' to get the flag.

```sh
hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{o3shLazV0TuS7VGsCb56I4PKCi3.QX5ETN1wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{o3shLazV0TuS7VGsCb56I4PKCi3.QX5ETN1wiM1EjNwIzW}
```

### Notes:

Learnt about soft and hard links and how to use them.

***
