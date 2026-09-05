
# Challenge 1: Matching with *

The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```

Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```

When zero files are matched, by default, the shell leaves the glob unchanged:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```

The * matches any part of the filename except for / or a leading . character. For example:

```sh
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

## Solution:

Ran 'cd /ch*' to get into directory using glob '*' and then ran '/challenge/run' to get the flag.

```sh
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{gyjDHT8HYLIG8tbaU9DevV2fh0M.QXxIDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{gyjDHT8HYLIG8tbaU9DevV2fh0M.QXxIDO0wiM1EjNwIzW}
```

### Notes:

Learned how the * glob acts as a wildcard during shell expansion, allowing abbreviated path patterns to match full directory names.

***

# Challenge 2: Matching with ?

Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

## Solution:

Ran 'cd /?ha??enge' to get into directory using glob '?' and then ran '/challenge/run' to get the flag.

```sh
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{49_tSrkqwPjifv9QUjifN8zqVPr.QXyIDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{49_tSrkqwPjifv9QUjifN8zqVPr.QXyIDO0wiM1EjNwIzW}
```

### Notes:

Learned how the ? glob matches exactly one character during shell expansion, enabling precise control over which parts of a filename or path are substituted.

***

# Challenge 3: Matching with []

Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

## Solution:

Changed directory to '/challenge/files' then ran '/challenge/run file_[bash]' (Used [] globbing to include bash for getting all files) to get the flag.

```sh
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{sH0BoB4ZUdejJFFw5Y39NXY6SKG.QXzIDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{sH0BoB4ZUdejJFFw5Y39NXY6SKG.QXzIDO0wiM1EjNwIzW}
```

### Notes:

Learned how bracket globbing ([]) matches exactly one character from a specified set, allowing fine-grained control over which filenames are expanded.

***

# Challenge 4: Matching paths with []

Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

## Solution:

Ran '/challenge/run /challenge/files/file_[bash]' to get the flag.

```sh
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{EJPh9nEzNJwx10P6x-q9QEICgGX.QX0IDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{EJPh9nEzNJwx10P6x-q9QEICgGX.QX0IDO0wiM1EjNwIzW}
```

### Notes:

Learned that globbing applies to entire paths, not just filenames, allowing bracket expressions to be used inside absolute paths.

***

# Challenge 5: Multiple globs

So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

```sh
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```

What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

## Solution:

Changed directory to '/challenge/files' then ran '/challenge/run' with argument p between ** so it gets all files with p as argument.

```sh
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{g8GRtPmR8nl2o3cqcbf7aQFtdef.0lM3kjNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{g8GRtPmR8nl2o3cqcbf7aQFtdef.0lM3kjNxwiM1EjNwIzW}
```

### Notes:

Understood that Bash allows multiple glob patterns within the same word, not just one at a time. Also reinforced that * matches any number of characters (including none), making it ideal for broadly capturing filenames based on a shared character.

***

# Challenge 6: Mixing globs

Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match only the files "challenging", "educational", and "pwning"!

HINT: Make sure to look at the names of the files in /challenge/files. Do you see any patterns that could help you make your glob?

## Solution:

Changed directory to '/challenge/files' and ran '/challenge/run' with argument '[cep]*' as it then gets the files that start with c, e or p which are the files we need.

```sh
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing    challenging  educational  great  incredible  kind      magical  optimistic  queenly  splendid   uplifting   wonderful  youthful
beautiful  delightful   fantastic    happy  jovial      laughing  nice     pwning      radiant  thrilling  victorious  xenial     zesty
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{ETax7dGpUBtLsUqxBp-qt0A36Ij.QX1IDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{ETax7dGpUBtLsUqxBp-qt0A36Ij.QX1IDO0wiM1EjNwIzW}
```

### Notes:

Learned that bracket expressions can be combined with * to form compact yet powerful globs, allowing multiple filename patterns to be matched using a single argument. This reinforced how thoughtful analysis of filename prefixes can simplify complex matching constraints while staying within strict character limits.

***

# Challenge 7: Exclusionary globbing

Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

## Solution:

Changed directory to '/challenge/files' and ran '/challenge/run' with argument '[pwn]*' so it runs all files without starting letters p,w and n.

```sh
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{o3ethbDgQkTm2E6vXzkbYYap3z4.QX2IDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{o3ethbDgQkTm2E6vXzkbYYap3z4.QX2IDO0wiM1EjNwIzW}
```

### Notes:

Learned that placing ^ (or !) as the first character inside [] inverts the match, allowing unwanted filenames to be excluded. This reinforced how bracket globbing matches exactly one character, and how combining it with * enables precise yet flexible filename selection during shell expansion.

***

# Challenge 8: Tab completion

As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

```sh
hacker@dojo:~$ ls /challenge
Dockerfile  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

## Solution:

Ran 'cat /challenge/pwncollege' which gave an error but when ran 'cat /challenge/pwn<TAB>', I got the flag.

```sh
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{spKAfs3SWThDsHCOCft4fZ-RMKl.0FN0EzNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{spKAfs3SWThDsHCOCft4fZ-RMKl.0FN0EzNxwiM1EjNwIzW}
```

### Notes:

Learned that tab completion expands filenames without executing glob patterns, making it a safer and more precise alternative to * when targeting specific files. This demonstrated how the shell’s auto-completion can bypass typing restrictions while preventing accidental matches to unintended files.

***

# Challenge 9: Multiple options for tab completion

Consider the following situation:

```sh
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

## Solution:

This one was tricky, so we use <TAB> instead of ls to get the file list, then to get a hidden file we had to use 'cat /challenge/files/p<TAB>' since multiple <TAB>s gave the file list. This revealed a hidden file called pwncollege-flag which when used as argument to cat gave us the flag.

```sh
hacker@globbing~multiple-options-for-tab-completion:~$ /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flamingo    pwncollege-hacking     
pwn-college            pwncollege-family      pwncollege-flyswatter  
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter  
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking     
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{oy_py3X8UIIhsTQRV2bFII1kmPX.0lN0EzNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{oy_py3X8UIIhsTQRV2bFII1kmPX.0lN0EzNxwiM1EjNwIzW}
```

### Notes:

Learned how bash handles ambiguous tab completions by completing up to the longest common prefix and listing all valid options when ambiguity remains.

***

# Challenge 10: Tab completion on commands

Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

## Solution:

Wrote 'pwncollege' and then used <TAB> to let the command auto-complete itself and then finally pressed Enter to get the flag.

```sh
hacker@globbing~tab-completion-on-commands:~$ pwncollege-15702 
Correct! Here is your flag:
pwn.college{QjFXuvTujh_jFzmcGes220DsyXa.0VN0EzNxwiM1EjNwIzW}
```

## Flag: 

```
pwn.college{QjFXuvTujh_jFzmcGes220DsyXa.0VN0EzNxwiM1EjNwIzW}
```

### Notes:

Learned that tab completion works for commands as well as files, enabling safe and accurate execution without needing to know or type the full command name.

***
