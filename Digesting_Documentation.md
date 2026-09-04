
# Challenge 1: Learning from Documentation

The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the -a of ls -a in the hidden files challenge of the Basic Commands module: that -a was an argument that told ls to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ls with the -a argument was the correct way to use it in our scenario.

The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:

Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of --giveflag. Good luck!

Given that knowledge, go get the flag!

## Solution:

Ran '/challenge/challenge --giveflag' to get the flag as per the documentation.

```sh
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{EWc6hL0ktTci3TIptb4R4tw9PKJ.QX0ITO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{EWc6hL0ktTci3TIptb4R4tw9PKJ.QX0ITO0wiM1EjNwIzW}
```

### Notes:

Learnt how programs rely on command-line arguments, and how reading usage documentation helps identify the correct flags to pass (like --giveflag) to get the intended output.

***

# Challenge 2: Learning Complex Usage

While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the find level in Basic Commands. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for. Many other commands are analogous.

Here is this level's documentation for /challenge/challenge:

Welcome to the documentation for /challenge/challenge! This program prints arbitrary files to the terminal when given the --printfile argument. The argument to --printfile is the path of the file to read. For example, /challenge/challenge --printfile /etc/hostname will print the container's hostname!

Given that documentation, go get the flag!

## Solution:

The documentation says that '/challenge/challenge' accepts the '--printfile' argument, and that this argument itself expects a file path as its value which here after trial and error is '/flag'.

```sh
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{Qp4f6myGjYkXP-vzTNI6Io30bbV.QX1ITO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{Qp4f6myGjYkXP-vzTNI6Io30bbV.QX1ITO0wiM1EjNwIzW}
```

### Notes:

Learnt how certain commands accept arguments that themselves take additional parameters, and how documentation clarifies nested usage patterns like providing --printfile followed by a file path to retrieve specific content.

# Challenge 3: Reading Manuals

This level introduces the man command. man is short for manual, and will display (if available) the manual of the command you pass as an argument. For example, let's say we wanted to learn about the yes command (yes, this is a real command):

```sh
hacker@dojo:~$ man yes
```

This will display the manual page for yes, which will look something like this:

```
YES(1)                           User Commands                          YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit

AUTHOR
       Written by David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2020  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation <https://www.gnu.org/software/coreutils/yes>
       or available locally via: info '(coreutils) yes invocation'

GNU coreutils 8.32               February 2022                          YES(1)
```
The important sections are:

```
NAME(1)                           CATEGORY                          NAME(1)

NAME
	This gives the name (and short description) of the command or
	concept discussed by the page.

SYNOPSIS
	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

DESCRIPTION
	Details of the command or concept, with detailed descriptions
	of the various options.

SEE ALSO
	Other man pages or online resources that might be useful.

COLLECTION                        DATE                          NAME(1)
```

You can scroll around the manpage with your arrow keys and PgUp/PgDn. When you're done reading the manpage, you can hit q to quit.

Manpages are stored in a centralized database. If you're curious, this database lives in the /usr/share/man directory, but you never need to interact with it directly: you just query it using the man command. The arguments to the man command aren't file paths, but just the names of the entries themselves (e.g., you run man yes to look up the yes manpage, rather than man /usr/bin/yes, which would be the actual path to the yes program but would result in man displaying garbage).

The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for challenge!

## Solution:

'will cause the challenge to print the flag' is the keyphrase, we need to use 'man challenge' to get the manual for challenge which gives us the command and argument to get the flag i.e. '/challenge/challenge --kxagis 956'.

```sh
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                                      Challenge Commands                                     CHALL
ENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --kxagis NUM
              print the flag if NUM is 956

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                            May 2024                                          CHALLENGE
m(1)
hacker@man~reading-manuals:~$ /challenge/challenge --kxagis 956
Correct usage! Your flag: pwn.college{kxNaX9Bg5RisM6reWwVkPeasvRD.QX0EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{kxNaX9Bg5RisM6reWwVkPeasvRD.QX0EDO0wiM1EjNwIzW}
```

### Notes:

Learnt how manual (triggered by man) pages provide structured documentation for commands, including available arguments and how to navigate a manpage.

***

# Challenge 4: Searching Manuals

You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /. After searching, you can hit n to go to the next result and N to go to the previous result. Instead of /, you can use ? to search backwards!

Find the option that will give you the flag by reading the challenge man page.

## Solution:

Used 'man challenge' to get the challenge manuals, then used '/flag' to get argument that gives flag (which here was --rdl). Then ran '/challenge/challenge --rdl' to get the flag.

```sh
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --rdl
Initializing...
Correct usage! Your flag: pwn.college{EH2ZzrZLzUiHysske7H2xgiIyDw.QX1EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{EH2ZzrZLzUiHysske7H2xgiIyDw.QX1EDO0wiM1EjNwIzW}
```

### Notes:

Learnt how manual page search works and how / and n (or N) streamline looking for relevant information inside long documentation.

***

# Challenge 5: Searching for manuals

This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the manpages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right manpage, read the man page manpage by doing: man man!

HINT 1: man man teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use /challenge/challenge

HINT 2: though the manpage is randomly named, you still actually use /challenge/challenge to get the flag!

## Solution:

Used 'man man' to find -k argument which searches for manpages with keyword which here was challenge. So ran 'man -k challenge' to get 'tayqthwcow' which prints flag therefore did 'man tayqthwcow' to get its manpages which revealed when passed with '--tayqth 064' gives flag.

```sh
hacker@man~searching-for-manuals:~$ man man
man: can't resolve man7/groff_man.7
MAN(1)                                                             Manual pager utils
MAN(1)

NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man is the system's manual pager.  Each page argument given to man is normally the name of a program, utility or function.  The
manual page asso‐
       ciated  with  each  of  these arguments is then found and displayed.  A section, if provided, will direct man to look only in that s
ection of the
       manual.  The default action is to search in all of the available sections following a pre-defined order (see DEFAULTS),  and  to  show
 only  the
       first page found, even if page exists in several sections.

       The table below shows the section numbers of the manual followed by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions, e.g. /etc/passwd
       6   Games
       7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7), man-pages(7)
       8   System administration commands (usually only for root)
       9   Kernel routines [Non standard]

       A manual page consists of several sections.

       Conventional  section  names  include NAME, SYNOPSIS, CONFIGURATION, DESCRIPTION, OPTIONS, EXIT STATUS,
RETURN VALUE, ERRORS, ENVIRONMENT, FILES,
       VERSIONS, STANDARDS, NOTES, BUGS, EXAMPLE, AUTHORS, and SEE ALSO.

       The following conventions apply to the SYNOPSIS section and can be used as a guide in other sections.

       bold text          type exactly as shown.
       italic text        replace with appropriate argument.
       [-abc]             any or all arguments within [ ] are optional.
       -a|-b              options delimited by | cannot be used together.
       argument ...       argument is repeatable.
       [expression] ...   entire expression within [ ] is repeatable.

       Exact rendering may vary depending on the output device.  For instance, man will usually not be able to render italics when running in  a  termi‐
       nal, and will typically use underlined or coloured text instead.

       The  command  or function illustration is a pattern that should match all possible invocations.  In some cases it is advisable to illustrate sev‐
       eral exclusive invocations as is shown in the SYNOPSIS section of this manual page.

EXAMPLES
       man ls
           Display the manual page for the item (program) ls.

       man man.7
           Display the manual page for macro package man from section 7.  (This is an alternative spelling of "man 7 man"
.)

       man 'man(7)'
           Display the manual page for macro package man from section 7.  (This is another alternative spelling of "man 7 man
".  It may be  more  conve‐
           nient  when copying and pasting cross-references to manual pages.  Note that the parentheses must normally be quoted to protect them from the
           shell.)

       man -a intro
           Display, in succession, all of the available intro manual pages contained within the manual.  It is possible to quit between successive  d
is‐
           plays or skip any of them.

       man -t bash | lpr -Pps
           Format  the manual page for bash into the default troff or groff format and pipe it to the printer named ps.  The def
ault output for groff is
           usually PostScript.  man --help should advise as to which processor is bound to the -t option.

       man -l -Tdvi ./foo.1x.gz > ./foo.1x.dvi
           This command will decompress and format the nroff source manual page ./foo.1x.gz into a device independent (dvi) file.   The  redir
ection  is
           necessary  as  the  -T  flag causes output to be directed to stdout with no pager.  The output could be viewed with a program such
as xdvi or
           further processed into PostScript using a program such as dvips.

       man -k printf
           Search the short descriptions and manual page names for the keyword printf as regular expression.  Print  out  any  matches.   Equivalent
 to
           apropos printf.

       man -f smail
           Lookup the manual pages referenced by smail and print out the short descriptions of any found.  Equivalent to whatis smail
.

OVERVIEW
       Many  options are available to man in order to give as much flexibility as possible to the user.  Changes can be made to the search path, sect
ion
       order, output processor, and other behaviours and operations detailed below.

       If set, various environment variables are interrogated to determine the operation of man.  It is possible to set the "catch-all" variable $
MANOPT
       to any string in command line format, with the exception that any spaces used as part of an option's argument must  be  escaped  (preceded  by  a
       backslash).   man  will  parse $MANOPT prior to parsing its own command line.  Those options requiring an argument will be overridden b
y the same
       options found on the command line.  To reset all of the options set in $MANOPT, -D can be specified as the initial  command  line  opti
on.   This
       will allow man to "forget" about the options specified in $MANOPT, although they must still have been valid.

       Manual  pages  are normally stored in nroff(1) format under a directory such as /usr/share/man.  In some installations, there may also
be prefor‐
       matted cat pages to improve performance.  See manpath(5) for details of where these files are stored.

       This package supports manual pages in multiple languages, controlled by your locale.  If your system did not set this up for  you  automatical
ly,
       then  you may need to set $LC_MESSAGES, $LANG, or another system-dependent environment variable to indicate your preferred locale, usua
lly speci‐
       fied in the POSIX format:

hacker@man~searching-for-manuals:~$ man -k challenge
tayqthwcow (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man tayqthwcow

CHALLENGE(1)                                                       Challenge Commands                                                       CHALLE
NGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --tayqth NUM
              print the flag if NUM is 064

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                             May 2024                                                            CHALLENGE
(1)
hacker@man~searching-for-manuals:~$ /challenge/challenge --tayqth 064
Correct usage! Your flag: pwn.college{0At6FZAJBaNTyq4thwcQUK73DoE.QX2EDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{0At6FZAJBaNTyq4thwcQUK73DoE.QX2EDO0wiM1EjNwIzW}
```

### Notes:

Learnt how to search the man page database by content using man -K.

***

# Challenge 6: Helpful Programs

Some programs don't have a man page, but might tell you how to run them if invoked with a special argument. Usually, this argument is --help, but it can often be -h or, in rare cases, -?, help, or other esoteric values like /? (though that latter is more frequently encountered on Windows).

In this level, you will practice reading a program's documentation with --help. Try it out!

## Solution:

Using '/challenge/challenge --help' we found out '-p' gives secret number which when passed to '-g' gives the flag using '/challenge/challenge'.

```sh
hacker@man~helpful-programs:~$ challenge --help
bash: challenge: command not found
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

options:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -g
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: expected one argument
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 844
hacker@man~helpful-programs:~$ /challenge/challenge -g 844
Correct usage! Your flag: pwn.college{8PuBeXIkdgRPEf44-2pA_CJJjVn.QX3IDO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{8PuBeXIkdgRPEf44-2pA_CJJjVn.QX3IDO0wiM1EjNwIzW}
```

### Notes:

Learned how programs without manpages can still document their usage through built-in help options such as --help, -h, or similar flags, and how these help messages expose the required arguments to correctly use the program.

***

# Challenge 7: Help for Builtins

Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help, as so:

```sh
hacker@dojo:~$ help
```

You can get help on a specific one by passing it to the help builtin. Let's look at a builtin that we've already used earlier, cd!

```sh
hacker@dojo:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
    
    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
...
```

Some good information! In this challenge, we'll practice using help to look up help for builtins. This challenge's challenge command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it!

## Solution:

Ran 'help challenge' to get documentation for challenge, which gave us secret key to be passed to 'challenge --secret' to get the flag.

```sh
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "g3rrAFWx".
hacker@man~help-for-builtins:~$ challenge --secret g3rrAFWx
Correct! Here is your flag!
pwn.college{g3rrAFWxRx7PdXzi1DvlQZW59TB.QX0ETO0wiM1EjNwIzW}
```

## Flag: 

```
pwn.college{g3rrAFWxRx7PdXzi1DvlQZW59TB.QX0ETO0wiM1EjNwIzW}
```

### Notes:

Learnt that some commands in Linux are implemented as shell builtins, not external programs, and therefore must be inspected using the shell’s internal 'help' mechanism rather than man or program-level help flags.

***
