
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

Ran '/challenge/run > /tmp/data.txt', then got the flag by 'grep "pwn.college" /tmp/data.txt'.

```sh
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep "pwn.college" /tmp/data.txt 
pwn.college{UtDfc-zL1ATAI3XFP1XyK679HYO.QX4EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{UtDfc-zL1ATAI3XFP1XyK679HYO.QX4EDO0wiM1EjNwIzW}
```

### Notes:

Learned how output redirection and text searching can be combined to process large amounts of command output efficiently.

***

# Challenge 7: Grepping live output

It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level. You can do this by using the | (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. For example:

```sh
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```

Now try it for yourself! /challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag!

## Solution:

Ran ' /challenge/run | grep "pwn.college" ' to get the flag.

```sh
hacker@piping~grepping-live-output:~$ /challenge/run | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/sacz532zgiacvg7mva9v6gbfmyw427i3-gnugrep-3.12/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{sEGdtEn-103FSREoQWlfpEfwjph.QX5EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{sEGdtEn-103FSREoQWlfpEfwjph.QX5EDO0wiM1EjNwIzW}
```

### Notes:

Learned how the pipe operator (|) connects commands by streaming stdout from one process into stdin of another, eliminating the need for intermediate files.

***

# Challenge 8: Grepping errors

You know how to redirect errors to a file, and you know how to pipe output to another program, such as grep. But what if you wanted to grep through errors directly?

The > operator redirects a given file descriptor to a file, and you've used 2> to redirect fd 2, which is standard error. The | operator redirects only standard output to another program, and there is no 2| form of the operator! It can only redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!

Try it now! Like the last level, this level will overwhelm you with output, but this time on standard error. grep through it to find the flag!

## Solution:

Ran ' /challenge/run 2>& 1 | grep "pwn.college" ' to get the flag.

```sh
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/sacz532zgiacvg7mva9v6gbfmyw427i3-gnugrep-3.12/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{0qoN90yuirYUlnxddQbzpBQv6Z9.QX1ATO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{0qoN90yuirYUlnxddQbzpBQv6Z9.QX1ATO0wiM1EjNwIzW}
```

### Notes:

Learned how the file descriptor redirection operator (2>&1) can be used to merge stderr into stdout, enabling tools like grep to process error output through pipes.

***

# Challenge 9: Filtering with grep -v

The grep command has a very useful option: -v (invert match). While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern:

```sh
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```

Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag!

## Solution:

Ran '/challenge/run | grep -v DECOY' to get the right flag.

```sh
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{kMyDUe-wiKg-hhmp_SmxXFM2UWM.0FOxEzNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{kMyDUe-wiKg-hhmp_SmxXFM2UWM.0FOxEzNxwiM1EjNwIzW}
```

### Notes:

Learned how grep -v inverts pattern matching, allowing lines that do not match a given pattern to be selected.

***

# Challenge 10: Filtering with sed 

grep is not the only way to match patterns. Sometimes the real data and the garbage data are mixed in the same line, and we want to filter out the garbage. For that, we have sed. sed provides an easy way to substitute patterns in text with a different word. The syntax for matching and replacing is simple:

```sh
sed "s/oldword/newword/g"
```

s/ - substitute
oldword - the word to replace
newword - the replacement for oldword
/g - global (search for all occurrences of the pattern)

In this challenge, /challenge/run will print out the flag, but between each character there will be the string "FAKEFLAG". Your job is to filter out the garbage data from the flag. Good luck!

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
