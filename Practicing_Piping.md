
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

Ran ' /challenge/run | sed "s/FAKEFLAG//g" ' to filter the output to get the flag.

```sh
hacker@piping~filtering-with-sed:~$ /challenge/run | sed "s/FAKEFLAG//g"
pwn.college{gWx9Z0x6XJ8V3fr1YCWxDtio6t5.01NxQTMywiM1EjNwIzW} 
```

## Flag: 

```
pwn.college{gWx9Z0x6XJ8V3fr1YCWxDtio6t5.01NxQTMywiM1EjNwIzW}
```

### Notes:

Learned how sed performs in-place pattern substitution on streamed text, making it ideal for cleaning or transforming data when useful and unwanted content are mixed within the same line.

***

# Challenge 11: Duplicating piped data with tee

When you pipe data from one command to another, you of course no longer see it on your screen. This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

Luckily, there is a solution! The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line. For example:

```sh
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```

As you can see, by providing two files to tee, we ended up with three copies of the piped-in data: one to stdout, one to the pwn file, and one to the college file. You can imagine how you might use this to debug things going haywire:

```sh
hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
```

Now, you try it! This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you! Use tee to duplicate your first attempt into a file, inspect the saved output, and then retry the pipeline with what you learned.

## Solution:

Ran '/challenge/pwn | tee pwn | /challenge/college' to get piped data in file named pwn then read it using 'cat pwn'. Finally analysing the secret and passing correct argument (/challenge/pwn --secret ARJYcruH | /challenge/college), got the flag.

```sh
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee pwn | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to save the first 
attempt to a file, inspect the saved output, and then retry the pipeline with 
what you learned.
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "ARJYcruH"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret ARJYcruH | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{ARJYcruHLA2fGmstUTWVEe2Towq.QXxITO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{ARJYcruHLA2fGmstUTWVEe2Towq.QXxITO0wiM1EjNwIzW}
```

### Notes:

Learned how tee duplicates piped data, allowing simultaneous inspection and forwarding of a stream.

***

# Challenge 12: Process substitution for input

Sometimes you need to compare the output of two commands rather than two files. You might think to save each output to a file first:

```sh
hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
```

But there's a more elegant way! Linux follows the philosophy that "everything is a file". That is, the system strives to provide file-like access to most resources, including the input and output of running programs! The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line and hook it up to the output of programs, as you learned in the previous few levels.

Interestingly, we can go further, and hook input and output of programs to arguments of commands. This is done using Process Substitution. For reading from a command (input process substitution), use <(command). When you write <(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:

```sh
hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
```

Where did /dev/fd/63 come from? bash replaced <(echo hi) with the path of the named pipe file that's hooked up to the command's output! While the command is running, reading from this file will read data from the standard output of the command. Typically, this is done using commands that take input files as arguments:

```sh
hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
```

Of course, you can specify this multiple times:

```sh
hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
```

Now for your challenge! Recall what you learned in the diff challenge from Comprehending Commands. In that challenge, you diffed two files. Now, you'll diff two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag.

Use process substitution with diff to compare the outputs of these two programs and find your flag!

## Solution:

Ran 'diff <(/challe
nge/print_decoys) <(/challenge/print_decoys_and_flag)' so it creates two temp files which have output of those two commands from which we get the different line using 'diff'. Using this I got the flag.

```sh
hacker@piping~process-substitution-for-input:~$ diff <(/challe
nge/print_decoys) <(/challenge/print_decoys_and_flag)
64a65
> pwn.college{k85Fel1duSo8anFkkpvy-cmaApM.0lNwMDOxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{k85Fel1duSo8anFkkpvy-cmaApM.0lNwMDOxwiM1EjNwIzW}
```

### Notes:

Learned how process substitution (<(command)) allows the output of a command to be treated as a temporary file.

***

# Challenge 13: Writing to multiple programs

Now you've learned that process substitution can make command output appear as files for reading with <(command). But you can also use process substitution for writing to commands!

You can duplicate data to two files with tee:

```sh
hacker@dojo:~$ echo HACK | tee THE > PLANET
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$ cat PLANET
HACK
hacker@dojo:~$
```

And you've used tee to duplicate data to a file and a command:

```sh
hacker@dojo:~$ echo HACK | tee THE | cat
HACK
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$
```

But what about duplicating to two commands? As tee says in its manpage, it's designed to write to files and to standard output:

```sh
TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and files
```

But wait! You just learned that bash can make commands look like files using process substitution! For writing to a command (output process substitution), use >(command). If you write an argument of >(rev), bash will run the rev command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary named pipe file. When commands write to this file, the data goes to the standard input of the command:

```sh
hacker@dojo:~$ echo HACK | rev
KCAH
hacker@dojo:~$ echo HACK | tee >(rev)
HACK
KCAH
```

Above, the following sequence of events took place:

1. bash started up the rev command, hooking a named pipe (presumably /dev/fd/63) to rev's standard input
2. bash started up the tee command, hooking a pipe to its standard input, and replacing the first argument to tee with /dev/fd/63. tee never even saw the argument >(rev); the shell substituted it before launching tee
3. bash used the echo builtin to print HACK into tee's standard input
4. tee read HACK, wrote it to standard output, and then wrote it to /dev/fd/63 (which is connected to rev's stdin)
5. rev read HACK from its standard input, reversed it, and wrote KCAH to standard output
Now it's your turn! In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands! Remember that tee can take multiple output targets, and >(command) is one kind of target. Scroll back through the previous challenges "Duplicating piped data with tee" and "Process substitution for input" if you need a refresher on this method.

Trivia!

The observant learner will realize that the following are equivalent:

```sh
hacker@dojo:~$ echo hi | rev
ih
hacker@dojo:~$ echo hi > >(rev)
ih
hacker@dojo:~$
```

More than one way to pipe data! Of course, the second route is way harder to read and also harder to expand. For example:

```sh
hacker@dojo:~$ echo hi | rev | rev
hi
hacker@dojo:~$ echo hi > >(rev | rev)
hi
hacker@dojo:~$
```

That's just silly! The lesson here is that, while Process Substitution is a powerful tool in your toolbox, it's a very specialized tool; don't use it for everything!

## Solution:

Ran '/challenge/hack | tee >(/challenge/the) | /challenge/planet' so output is simultaneously transferred to both of the other commands.

```sh
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
19648255782348314131
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{8pgHlN6fsmBQQK1sa76w_RX-LiV.QXwgDN1wiM1EjNwIzW}
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{8pgHlN6fsmBQQK1sa76w_RX-LiV.QXwgDN1wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8pgHlN6fsmBQQK1sa76w_RX-LiV.QXwgDN1wiM1EjNwIzW}
```

### Notes:

- Process substitution created a file-like destination connected to '/challenge/the', while the original output stream continued through the pipe to '/challenge/planet'.
- Learned how output process substitution (>(command)) allows a program's input to be exposed as a writable file-like target. 

***

# Challenge 14: Split-piping stderr and stdout

Now, let's put your knowledge together. You must master the ultimate piping task: redirect stdout to one program and stderr to another.

The challenge here, of course, is that the | operator links the stdout of the left command with the stdin of the right command. Of course, you've used 2>&1 to redirect stderr into stdout and, thus, pipe stderr over, but this then mixes stderr and stdout. How to keep it unmixed?

You will need to combine your knowledge of >(), 2>, and |. How to do it is a task I'll leave to you.

In this challenge, you have:

- /challenge/hack: this produces data on stdout and stderr
- /challenge/the: you must redirect hack's stderr to this program
- /challenge/planet: you must redirect hack's stdout to this program
  
Go get the flag!

BONUS: For some added difficulty, find a solution that doesn't use |.

## Solution:

Ran '/challenge/hack 2> >(/challenge/the) > >(/challenge/planet)' to capture the flag, which basically is routing stderr and stdout using 2> and > and sending it to their respective function files using process substitution.

```sh
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{kuYJTUfW8b3h0Y14CCRjnMt1LAf.QXxQDM2wiM1EjNwIzW}
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) > >(/challenge/planet)
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{kuYJTUfW8b3h0Y14CCRjnMt1LAf.QXxQDM2wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{kuYJTUfW8b3h0Y14CCRjnMt1LAf.QXxQDM2wiM1EjNwIzW}
```

### Notes:

Learned how stdout and stderr can be redirected independently to different destinations instead of being merged together.

***

# Challenge 15: Named pipes

You've learned about pipes using |, and you've seen that process substitution creates temporary named pipes (like /dev/fd/63). You can also create your own persistent named pipes that stick around on the filesystem! These are called FIFOs, which stands for First (byte) In, First (byte) Out.

You create a FIFO using the mkfifo command:

```sh
hacker@dojo:~$ mkfifo my_pipe
hacker@dojo:~$ ls -l my_pipe
prw-r--r-- 1 hacker hacker 0 Jan 1 12:00 my_pipe
hacker@dojo:~$ ls -l some_file
-rw-r--r-- 1 hacker hacker 0 Jan 1 12:00 some_file
hacker@dojo:~$
```

Notice the p at the beginning of the permissions - that indicates it's a pipe! That's markedly different than the - that's at the beginning of normal files, such as some_file in the above example.

Unlike the automatic named pipes from process substitution:

- You control where FIFOs are created
- They persist until you delete them
- Any process can write to them by path (e.g., echo hi > my_pipe)
- You can see them with ls and examine them like files

One problem with FIFOs is that they'll "block" any operations on them until both the read side of the pipe and the write side of the pipe are ready. For example, consider this:

```sh
hacker@dojo:~$ mkfifo myfifo
hacker@dojo:~$ echo pwn > myfifo
```

To service echo pwn > myfifo, bash will open the myfifo file in write mode. However, this operation will hang until something also opens the file in read mode (thus completing the pipe). That can be in a different console:

```sh
hacker@dojo:~$ cat myfifo
pwn
hacker@dojo:~$
```

What happened here? When we ran cat myfifo, the pipe had both sides of the connection all set, and unblocked, allowing echo pwn > myfifo to run, which sent pwn into the pipe, where it was read by cat.

Of course, this can somewhat be done by normal files: you've learned how to echo stuff into them and cat them out. Why use a FIFO instead? Here are key differences:

1. No disk storage: FIFOs pass data directly between processes in memory - nothing is saved to disk
2. Ephemeral data: Once data is read from a FIFO, it's gone (unlike files where data persists)
3. Automatic synchronization: Writers block until the readers are ready, and vice-versa. This is actually useful! It provides automatic synchronization. Consider the example above: with a FIFO, it doesn't matter if cat myfifo or echo pwn > myfifo is executed first; each would just wait for the other. With files, you need to make sure to execute the writer before the reader.
4. Complex data flows: FIFOs are useful for facilitating complex data flows, merging and splitting data in flexible ways, and so on. For example, FIFOs support multiple readers and writers.

This challenge will be a simple introduction to FIFOs. You'll need to create a /tmp/flag_fifo file and redirect the stdout of /challenge/run to it. If you're successful, /challenge/run will write the flag into the FIFO! Go do it!

HINT: The blocking behavior of FIFOs makes it hard to solve this challenge in a single terminal. You may want to use the Desktop or VSCode mode for this challenge so that you can launch two terminals.

## Solution:

Ran 'mkfifo /tmp/flag_fifo' to make a fifo at /tmp named flag_fifo then ran '/challenge/run > /tmp/flag_fifo' so stdout is stored in flag_fifo. Then opened another shell where ran 'cat /tmp/flag_fifo' to get the flag stored.

```sh
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo 
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!

hacker@piping~named-pipes:~$ cat /tmp/flag_fifo
You've correctly redirected /challenge/run's stdout to a FIFO at
/tmp/flag_fifo! Here is your flag:
pwn.college{kLCBt1SwJavphE2AzcNsLoS1_yI.01MzMDOxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{kLCBt1SwJavphE2AzcNsLoS1_yI.01MzMDOxwiM1EjNwIzW}
```

### Notes:

Learned how to create named pipes (FIFOs) using the mkfifo command and use them for communication between processes.

***
