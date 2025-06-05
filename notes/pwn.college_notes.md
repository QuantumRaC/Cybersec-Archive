## Linux Luminarium

Digesting Documentation

4. Searching For Manuals
    - This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the man pages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right man page, read the man page manpage by doing: man man!

    HINT 1: man man teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use /challenge/challenge

    HINT 2: though the man page is randomly named, you still actually use /challenge/challenge to get the flag!
    - my solution:
   `man man` for manuals for `man`
   found out that `man -k [keyword]` and `man --apropos [keyword]` can be used to search for functions
    hacker@man~searching-for-manuals:/usr/share/man/man1$ man --apropos challenge
    vdtfxlwixj (1)       - print the flag!
    hacker@man~searching-for-manuals:/usr/share/man/man1$ man vdtfxlwixj
    hacker@man~searching-for-manuals:/usr/share/man/man1$ vdtfxlwixj --vdtfxl 884
    bash: vdtfxlwixj: command not found
    hacker@man~searching-for-manuals:/usr/share/man/man1$ man vdtfxlwixj
    hacker@man~searching-for-manuals:/usr/share/man/man1$ /challenge/challenge --vdtfxl 884
    Correct usage! Your flag: pwn.college{8B8vTGCL4dHYNY5tfL537I6xTlW.QX2EDO0wiNxQjMyEzW} 

5. Helpful Programs
   - Some programs don't have a man page, but might tell you how to run them if invoked with a special argument. Usually, this argument is --help, but it can often be -h or, in rare cases, -?, help, or other esoteric values like /? (though that latter is more frequently encountered on Windows).
   - In this level, you will practice reading a program's documentation with --help. Try it out!
   - my solution:
    hacker@man~helpful-programs:~$ /challenge/challenge --help
    usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

    optional arguments:
    -h, --help            show this help message and exit
    --fortune             read your fortune
    -v, --version         get the version number
    -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                            get the flag, if given the correct value
    -p, --print-value     print the value that will cause the -g option to give you the flag
    hacker@man~helpful-programs:~$ /challenge/challenge -g GIVE_THE_FLAG
    usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
    a challenge to make you ask for help: error: argument -g/--give-the-flag: invalid int value: 'GIVE_THE_FLAG'
    hacker@man~helpful-programs:~$ /challenge/challenge -p
    The secret value is: 534
    hacker@man~helpful-programs:~$ /challenge/challenge -g 534
    Correct usage! Your flag: pwn.college{Y5HukkQ3U4lCFidO2KZJwfd2fx-.QX3IDO0wiNxQjMyEzW}
    hacker@man~helpful-programs:~$ 

6. Help for Builtins
    - Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help, as so:
    hacker@dojo:~$ help
    You can get help on a specific one by passing it to the help builtin. Let's look at a builtin that we've already used earlier, cd!

    hacker@dojo:~$ help cd
    cd: cd [-L|[-P [-e]] [-@]] [dir]
        Change the shell working directory.
        
        Change the current directory to DIR.  The default DIR is the value of the
        HOME shell variable.
    ...
    Some good information! In this challenge, we'll practice using help to look up help for builtins. This challenge's challenge command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it!

    - my solution:
    hacker@man~help-for-builtins:~$ help
    GNU bash, version 5.2.37(1)-release (x86_64-pc-linux-gnu)
    These shell commands are defined internally.  Type `help' to see this list.
    Type `help name' to find out more about the function `name'.
    Use `info bash' to find out more about the shell in general.
    Use `man -k' or `info' to find out more about commands not in this list.

    A star (*) next to a name means that the command is disabled.

    job_spec [&]                                    history [-c] [-d offset] [n] or history -anr>
    (( expression ))                                if COMMANDS; then COMMANDS; [ elif COMMANDS;>
    . filename [arguments]                          jobs [-lnprs] [jobspec ...] or jobs -x comma>
    ...

    hacker@man~help-for-builtins:~$ help challenge
    challenge: challenge [--fortune] [--version] [--secret SECRET]
        This builtin command will read you the flag, given the right arguments!
        
        Options:
        --fortune         display a fortune
        --version         display the version
        --secret VALUE    prints the flag, if VALUE is correct

        You must be sure to provide the right value to --secret. That value
        is "4BUzxRSe".
    hacker@man~help-for-builtins:~$ challenge --secret 4BUzxRSe
    Correct! Here is your flag!
    pwn.college{4BUzxRSevc4nhnREtqOFFE5Fcs5.QX0ETO0wiNxQjMyEzW}

Practicing Piping
9. Filtering with grep -v

    The grep command has a very useful option: -v (invert match). While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern:

    hacker@dojo:~$ cat data.txt
    hello hackers!
    hello world!
    hacker@dojo:~$ cat data.txt | grep -v world
    hello hackers!
    hacker@dojo:~$
    Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somehwere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

    Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag

    - my solution:
    hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep pwn | grep -v DECOY
    pwn.college{AAbFMbUEBiAINIUAzcT6Ru4y5O8.0FOxEzNxwiNxQjMyEzW}

10. Duplicating piped data with tee
    When you pipe data from one command to another, you of course no longer see it on your screen. This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

    Luckily, there is a solution! The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line. For example:

    hacker@dojo:~$ echo hi | tee pwn college
    hi
    hacker@dojo:~$ cat pwn
    hi
    hacker@dojo:~$ cat college
    hi
    hacker@dojo:~$
    Now, you try it! This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you!
    - my solution:
    hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee intercept | /challenge/college
    Processing...
    The input to 'college' does not contain the correct secret code! This code 
    should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
    output of 'pwn' and figure out what the code needs to be.
    hacker@piping~duplicating-piped-data-with-tee:~$ cat intercept
    Usage: /challenge/pwn --secret [SECRET_ARG]

    SECRET_ARG should be "YXTXTQeZ"
    hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret YXTXTQeZ | tee intercept
    | /challenge/college
    Processing...
    WARNING: you are overwriting file intercept with tee's output...
    Correct! Passing secret value to /challenge/college...
    Great job! Here is your flag:
    pwn.college{YXTXTQeZlm1YDfbP2rcgr6KkQ2D.QXxITO0wiNxQjMyEzW}


11. Writing to multiple programs

    Luckily, Linux follows the philosophy that "everything is a file". That is, the system strives to provide file-like access to most resources, including the input and output of running programs! The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line (such as tee) and hook it up to the input or output side of a program!

    This is done using what's called Process Substitution. If you write an argument of >(rev), bash will run the rev command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:

    hacker@dojo:~$ echo >(rev)
    /dev/fd/63
    hacker@dojo:~$
    Where did /dev/fd/63 come from? bash replaced >(rev) with the path of the named pipe file that's hooked up to rev's input! While the command is running, writing to this file will pipe data to the standard input of the command. Typically, this is done using commands that take output files as arguments (like tee):

    hacker@dojo:~$ echo HACK | rev
    KCAH
    hacker@dojo:~$ echo HACK | tee >(rev)
    HACK
    KCAH
    Above, the following sequence of events took place:

    bash started up the rev command, hooking a named pipe (presumably /dev/fd/63) to rev's standard input
    bash started up the tee command, hooking a pipe to its standard input, and replacing the first argument to tee with /dev/fd/63. tee never even saw the argument >(rev); the shell substituted it before launching tee
    bash used the echo builtin to print HACK into tee's standard input
    tee read HACK, wrote it to standard output, and then wrote it to /dev/fd/63 (which is connected to rev's stdin)
    rev read HACK from its standard input, reversed it, and wrote KCAH to standard output
    Now it's your turn! In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands!

    - my solution:
    hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
    This secret data must directly and simultaneously make it to /challenge/the and 
    /challenge/planet. Don't try to copy-paste it; it changes too fast.
    24889312872449322275
    Congratulations, you have duplicated data into the input of two programs! Here 
    is your flag:
    pwn.college{QtqkWYGxqjPdJ0d5fq1Pk1arVdT.QXwgDN1wiNxQjMyEzW}

12. Split-piping stderr and stdout

    Now, let's put your knowledge together. You must master the ultimate piping task: redirect stdout to one program and stderr to another.

    The challenge here, of course, is that the | operator links the stdout of the left command with the stdin of the right command. Of course, you've used 2>&1 to redirect stderr into stdout and, thus, pipe stderr over, but this then mixes stderr and stdout. How to keep it unmixed?

    You will need to combine your knowledge of >(), 2>, and |. How to do it is a task I'll leave to you.

    In this challenge, you have:

    /challenge/hack: this produces data on stdout and stderr
    /challenge/the: you must redirect hack's stderr to this program
    /challenge/planet: you must redirect hack's stdout to this program
    Go get the flag!

    - my solution:

    hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/chal
    lenge/the)
    Congratulations, you have learned a redirection technique that even experts 
    struggle with! Here is your flag:
    pwn.college{QOVXXMJTSSdv27ALPDlQFxiBz1g.QXxQDM2wiNxQjMyEzW}
