# Leviathan0

## LEVEL GOAL

There is no information for this level, intentionally.

## SOLUTION

```
nikhilh@ubuntu:~$ ssh -p 2223 leviathan0@leviathan.labs.overthewire.org

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
leviathan0@leviathan.labs.overthewire.org's password: 
...
...

leviathan0@leviathan:~$ ls -la

total 24

drwxr-xr-x  3 root       root       4096 May 10 18:27 .
drwxr-xr-x 10 root       root       4096 May 10 18:27 ..
drwxr-x---  2 leviathan1 leviathan0 4096 May 10 18:27 .backup
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-rw-r--r--  1 root       root        675 May 15  2017 .profile

leviathan0@leviathan:~$ cd .backup/

leviathan0@leviathan:~/.backup$ ls

bookmarks.html

leviathan0@leviathan:~/.backup$ cat bookmarks.html | grep password

<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

## FLAG

rioGegei8m
