# LEVEL GOAL

The password for level 3 is in the file krypton3. It is in 5 letter group ciphertext. It is encrypted with a Caesar Cipher. Without any further information, this cipher text may be difficult to break. You do not have direct access to the key, however you do have access to a program that will encrypt anything you wish to give it using the key. If you think logically, this is completely easy.

One shot can solve it!

Have fun.

# HINTS

ROT13 is a simple substitution cipher.

Substitution ciphers are a simple replacement algorithm. In this example of a substitution cipher, we will explore a ‘monoalphebetic’ cipher. Monoalphebetic means, literally, “one alphabet” and you will see why.

This level contains an old form of cipher called a ‘Caesar Cipher’. A Caesar cipher shifts the alphabet by a set number.

# SOLUTION

Code:
```
import sys
sys.path.append('/home/nikhilh/')

from pwn import *
from cipher_systems.caesar_cipher.break_caesar_cipher import CaesarCracker

remote_ssh = ssh("krypton2", "krypton.labs.overthewire.org", port=2222, password="ROTTEN")
ciphertext = remote_ssh.download_data("/krypton/krypton2/krypton3")

cipher_obj = CaesarCracker()
plaintext = cipher_obj.crack(ciphertext)
print (plaintext)

remote_ssh.close()
```

Output:
```
nikhilh@ubuntu:~/overthewire/krypton/level2$ python auth.py 
[+] Connecting to krypton.labs.overthewire.org on port 2222: Done
[*] krypton1@krypton.labs.overthewire.org:
    Distro    Ubuntu 14.04
    OS:       linux
    Arch:     amd64
    Version:  4.4.0
    ASLR:     Disabled
    Note:     Susceptible to ASLR ulimit trick (CVE-2016-3672)
[+] Downloading '/krypton/krypton2/krypton3': Found '/krypton/krypton2/krypton3' in ssh cache
INFO: 2018-11-19 18:40:16 Cracking Caesar Cipher...
INFO: 2018-11-19 18:40:16 Decrypting...
INFO: 2018-11-19 18:40:16 Encrypting...

...
...

INFO: 2018-11-19 18:40:16 Decrypting...
INFO: 2018-11-19 18:40:16 Encrypting...
['OMQEMDUEQMEK\n', 'NLPDLCTDPLDJ\n', 'MKOCKBSCOKCI\n', 'LJNBJARBNJBH\n', 'KIMAIZQAMIAG\n', 'JHLZHYPZLHZF\n', 'IGKYGXOYKGYE\n', 'HFJXFWNXJFXD\n', 'GEIWEVMWIEWC\n', 'FDHVDULVHDVB\n', 'ECGUCTKUGCUA\n', 'DBFTBSJTFBTZ\n', 'CAESARISEASY\n', 'BZDRZQHRDZRX\n', 'AYCQYPGQCYQW\n', 'ZXBPXOFPBXPV\n', 'YWAOWNEOAWOU\n', 'XVZNVMDNZVNT\n', 'WUYMULCMYUMS\n', 'VTXLTKBLXTLR\n', 'USWKSJAKWSKQ\n', 'TRVJRIZJVRJP\n', 'SQUIQHYIUQIO\n', 'RPTHPGXHTPHN\n', 'QOSGOFWGSOGM\n', 'PNRFNEVFRNFL\n']
DEBUG: 2018-11-19 18:40:16 EOF in transport thread
[*] Closed connection to 'krypton.labs.overthewire.org'
INFO: 2018-11-19 18:41:28 Closed connection to 'krypton.labs.overthewire.org'
```

# FLAG

CAESARISEASY
