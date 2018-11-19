# LEVEL GOAL

The password for level 2 is in the file ‘krypton2’. It is ‘encrypted’ using a simple rotation. It is also in non-standard ciphertext format. When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns. This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!

# HINTS

None

# SOLUTION

Code:
```
import string
from pwn import *

rot13 = string.maketrans("ABCDEFGHIJKLMabcdefghijklmNOPQRSTUVWXYZnopqrstuvwxyz", \
                         "NOPQRSTUVWXYZnopqrstuvwxyzABCDEFGHIJKLMabcdefghijklm")

remote_ssh = ssh('krypton1', 'krypton.labs.overthewire.org', port=2222, password='KRYPTONISGREAT')
ciphertext = remote_ssh.download_data('/krypton/krypton1/krypton2')

print(ciphertext)
rot13 = string.maketrans("ABCDEFGHIJKLMabcdefghijklmNOPQRSTUVWXYZnopqrstuvwxyz", \
                         "NOPQRSTUVWXYZnopqrstuvwxyzABCDEFGHIJKLMabcdefghijklm")
print (string.translate(ciphertext, rot13))
```

Output:
```
nikhilh@ubuntu:~/overthewire/krypton/level1$ python auth.py 
[+] Connecting to krypton.labs.overthewire.org on port 2222: Done
[*] krypton1@krypton.labs.overthewire.org:
    Distro    Ubuntu 14.04
    OS:       linux
    Arch:     amd64
    Version:  4.4.0
    ASLR:     Disabled
    Note:     Susceptible to ASLR ulimit trick (CVE-2016-3672)
[+] Downloading '/krypton/krypton1/krypton2': Found '/krypton/krypton1/krypton2' in ssh cache
YRIRY GJB CNFFJBEQ EBGGRA

LEVEL TWO PASSWORD ROTTEN
```

# FLAG

ROTTEN
