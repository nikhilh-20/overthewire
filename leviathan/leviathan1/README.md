# Leviathan1

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

```
nikhilh@ubuntu:~$ ssh -p 2223 leviathan1@leviathan.labs.overthewire.org

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
leviathan1@leviathan.labs.overthewire.org's password: 
...
...

leviathan1@leviathan:~$ ls
check

leviathan1@leviathan:~$ ltrace ./check
__libc_start_main(0x565556c0, 1, 0xffffd754, 0x565557a0 <unfinished ...>
printf("password: ")                                                                                                          = 10
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700password: something
)                                                                       = 115
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700)                                                                       = 111
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700)                                                                       = 109
strcmp("som", "sex")                                                                                                          = 1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)                                                                                         = 29
+++ exited (status 0) +++

leviathan1@leviathan:~$ ./check
password: sex
$ whoami
leviathan2
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
```

## FLAG

ougahZi8Ta
