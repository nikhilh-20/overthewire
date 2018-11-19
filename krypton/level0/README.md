# LEVEL GOAL

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

S1JZUFRPTklTR1JFQVQ=

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2222. You can find the files for other levels in /krypton/

# HINTS

None

# SOLUTION

Code:
```
from pwn import *
print (b64d('S1JZUFRPTklTR1JFQVQ='))
```

Output:
```
nikhilh@ubuntu:~/overthewire/krypton/level1$ python auth.py 
KRYPTONISGREAT
```

# FLAG

KRYPTONISGREAT
