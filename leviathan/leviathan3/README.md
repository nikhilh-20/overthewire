# Leviathan 3

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

```
nikhilh@ubuntu:~$ ssh -p 2223 leviathan3@leviathan.labs.overthewire.org

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
leviathan3@leviathan.labs.overthewire.org's password: 
...
...

leviathan3@leviathan:~$ ls
level3

leviathan3@leviathan:~$ ./level3
Enter the password> 1234
bzzzzzzzzap. WRONG

leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x565557b4, 1, 0xffffd754, 0x56555870 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                    = -1
printf("Enter the password> ")                                                                                                = 20
fgets(Enter the password> kakaka
"kakaka\n", 256, 0xf7fc55a0)                                                                                            = 0xffffd560
strcmp("kakaka\n", "snlprintf\n")                                                                                             = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                                                                                                    = 19
+++ exited (status 0) +++

leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x565557b4, 1, 0xffffd754, 0x56555870 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                    = -1
printf("Enter the password> ")                                                                                                = 20
fgets(Enter the password> nikel
"nikel\n", 256, 0xf7fc55a0)                                                                                             = 0xffffd560
strcmp("nikel\n", "snlprintf\n")                                                                                              = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                                                                                                    = 19
+++ exited (status 0) +++

leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x565557b4, 1, 0xffffd754, 0x56555870 <unfinished ...>
strcmp("h0no33", "kakaka")                                                                                                    = -1
printf("Enter the password> ")                                                                                                = 20
fgets(Enter the password> snlprintf
"snlprintf\n", 256, 0xf7fc55a0)                                                                                         = 0xffffd560
strcmp("snlprintf\n", "snlprintf\n")                                                                                          = 0
puts("[You've got shell]!"[You've got shell]!
)                                                                                                   = 20
geteuid()                                                                                                                     = 12003
geteuid()                                                                                                                     = 12003
setreuid(12003, 12003)                                                                                                        = 0
system("/bin/sh"$ whoami
leviathan3
$ ./level3
Enter the password> snlprintf
[You've got shell]!
$ whoami
leviathan4
$ cat /etc/leviathan_pass/leviathan4
vuH0coox6m
$ exit
$ exit
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                                                                        = 0
+++ exited (status 0) +++
```

## FLAG

vuH0coox6m
