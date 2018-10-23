# Leviathan 4

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

```
leviathan4@leviathan:~$ ls -la
total 24
drwxr-xr-x  3 root root       4096 Oct  7 22:31 .
drwxr-xr-x 10 root root       4096 Oct  7 22:31 ..
-rw-r--r--  1 root root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root root       3526 May 15  2017 .bashrc
-rw-r--r--  1 root root        675 May 15  2017 .profile
dr-xr-x---  2 root leviathan4 4096 Oct  7 22:31 .trash

leviathan4@leviathan:~$ cd .trash

leviathan4@leviathan:~/.trash$ ls
bin

leviathan4@leviathan:~/.trash$ ./bin
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010 

leviathan4@leviathan:~/.trash$ ltrace ./bin
__libc_start_main(0x80484bb, 1, 0xbffff774, 0x80485c0 <unfinished ...>
fopen("/etc/leviathan_pass/leviathan5", "r")                              = 0
+++ exited (status 255) +++
```

The binary translates to: `Tith4cokei`

## FLAG

Tith4cokei
