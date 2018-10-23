# LEVEL GOAL

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

S1JZUFRPTklTR1JFQVQ=

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2222. You can find the files for other levels in /krypton/

# SOLUTION

```
nikhilh@ubuntu:~/krypton/level0$ echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
KRYPTONISGREAT
```

# FLAG

KRYPTONISGREAT
