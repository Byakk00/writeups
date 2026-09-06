
# Challenge 1: Redirecting output

First, let's look at redirecting stdout to files. You can accomplish this with the > character, as so:

```sh
hacker@dojo:~$ echo hi > asdf
```

This will redirect the output of echo hi (which will be hi) to the file asdf. You can then use a program such as cat to output this file:

```sh
hacker@dojo:~$ cat asdf
hi
```

In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

## Solution:

Ran 'echo PWN > COLLEGE' to get the flag.

```sh
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{U1nbDj224DskRlOJILV8iIbu2kF.QX0YTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{U1nbDj224DskRlOJILV8iIbu2kF.QX0YTN0wiM1EjNwIzW}
```

### Notes:

Learned how output redirection (>) sends a command’s stdout to a file instead of the terminal. 

***

# Challenge 2: Redirecting more output

Aside from redirecting the output of echo, you can, of course, redirect the output of any command. In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will, of course, end up in the myflag file!

You'll notice that /challenge/run will still happily print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

WARNING: If a previous experiment left a file, directory, or symlink named myflag in your current directory, remove it first so the shell can create a normal writable file there.

## Solution:

Ran '/challenge/run > myflag' to get the stdout in myflag, then ran 'cat myflag' to get the flag.

```sh
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{8JbFoCL-ny2n7hs9Zi2k6rq-jb1.QX1YTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8JbFoCL-ny2n7hs9Zi2k6rq-jb1.QX1YTN0wiM1EjNwIzW}
```

### Notes:

Learned the distinction between standard output (stdout) and standard error (stderr), and how redirecting stdout does not affect messages sent to stderr.

***

# Challenge 3: Appending output

A common use-case of output redirection is to save off some command results for later analysis. Often times, you want to do this in aggregate: run a bunch of commands, save their output, and grep through it later. In this case, you might want all that output to keep appending to the same file, but > will create a new output file every time, deleting the old contents.

You can redirect input in append mode using >> instead of >, as so:

```sh
hacker@dojo:~$ echo pwn > outfile
hacker@dojo:~$ echo college >> outfile
hacker@dojo:~$ cat outfile
pwn
college
hacker@dojo:$
```

To practice, run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag. The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag!

Go for it now!

## Solution:

Ran '/challenge/run >> /home/hacker/the-flag' and then 'cat /home/hacker/the-flag' to get the flag.

```sh
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{czAJp7DlbJAEqg0T5x0CJW22dAL.QX3ATO0wiM1EjNwIzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```

## Flag: 

```
pwn.college{czAJp7DlbJAEqg0T5x0CJW22dAL.QX3ATO0wiM1EjNwIzW}
```

### Notes:

Learned how append mode redirection (>>) differs from truncation-mode redirection (>), and why it is essential when preserving existing file contents.

***

# Challenge 4: Redirecting errors

Just like standard output, you can also redirect the error channel of commands. Here, we'll learn about File Descriptor numbers. A File Descriptor (FD) is a number that describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:

```sh
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```

Redirecting errors is pretty easy from this point. If you have a command that might produce data via standard error (such as /challenge/run), you can do:

```sh
hacker@dojo:~$ /challenge/run 2> errors.log
```

That will redirect standard error (FD 2) to the errors.log file. Furthermore, you can redirect multiple file descriptors at the same time! For example:

```sh
hacker@dojo:~$ some_command > output.log 2> errors.log
```

That command will redirect output to output.log and errors to errors.log.

Let's put this into practice! In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off!

WARNING: If a previous experiment left a file, directory, or symlink named myflag or instructions in your current directory, remove it first so the shell can create normal writable files there.

## Solution:

Ran '/challenge/run > myflag 2> instructions' and then 'cat myflag' to get the flag.

```sh
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{YCRL7BkH9uc37sUYwkZoAn4TpBc.QX3YTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{YCRL7BkH9uc37sUYwkZoAn4TpBc.QX3YTN0wiM1EjNwIzW}
```

### Notes:

Learned how file descriptor numbers control different output streams and how they can be redirected independently.

***

# Challenge 5: Redirecting inputs

Just like you can redirect output from programs, you can redirect input to programs! This is done using <, as so:

```sh
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```

You can do interesting things with a lot of different programs using input redirection! In this level, we will practice using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE! To write that value to the PWN file, recall the prior challenge on output redirection from echo!

## Solution:

Ran 'echo COLLEGE > PWN' and then '/challenge/run < PWN' to capture the flag.

```sh
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{wpsrLBYKMu6XsXbbYI5RDaoWn2S.QXwcTN0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{wpsrLBYKMu6XsXbbYI5RDaoWn2S.QXwcTN0wiM1EjNwIzW}
```

### Notes:

Learned how input redirection (<) feeds file contents into a program’s standard input.

***

# Challenge 6: Grepping stored results

You know how to run commands, how to redirect their output (e.g., >), and how to search through the resulting file (e.g., grep). Let's put this together!

In preparation for more complex levels, we want you to:

1. Redirect the output of /challenge/run to /tmp/data.txt.
2. This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
3. grep that for the flag!

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
