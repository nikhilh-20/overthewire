# LEVEL GOAL

Hopefully by now its obvious that encryption using repeating keys is a bad idea. Frequency analysis can destroy repeating/fixed key substitution crypto.

A feature of good crypto is random ciphertext. A good cipher must not reveal any clues about the plaintext. Since natural language plaintext (in this case, English) contains patterns, it is left up to the encryption key or the encryption algorithm to add the ‘randomness’.

Modern ciphers are similar to older plain substitution ciphers, but improve the ‘random’ nature of the key.

An example of an older cipher using a complex, random, large key is a vigniere using a key of the same size of the plaintext. For example, imagine you and your confident have agreed on a key using the book ‘A Tale of Two Cities’ as your key, in 256 byte blocks.

The cipher works as such:

Each plaintext message is broken into 256 byte blocks. For each block of plaintext, a corresponding 256 byte block from the book is used as the key, starting from the first chapter, and progressing. No part of the book is ever re-used as key. The use of a key of the same length as the plaintext, and only using it once is called a “One Time Pad”.

Look in the krypton6 directory. You will find a file called ‘plain1’, a 256 byte block. You will also see a file ‘key1’, the first 256 bytes of ‘A Tale of Two Cities’. The file ‘cipher1’ is the cipher text of plain1. As you can see (and try) it is very difficult to break the cipher without the key knowledge.

If the encryption is truly random letters, and only used once, then it is impossible to break. A truly random “One Time Pad” key cannot be broken. Consider intercepting a ciphertext message of 1000 bytes. One could brute force for the key, but due to the random key nature, you would produce every single valid 1000 letter plaintext as well. Who is to know which is the real plaintext?!?

Choosing keys that are the same size as the plaintext is impractical. Therefore, other methods must be used to obscure ciphertext against frequency analysis in a simple substitution cipher. The impracticality of an ‘infinite’ key means that the randomness, or entropy, of the encryption is introduced via the method.

We have seen the method of ‘substitution’. Even in modern crypto, substitution is a valid technique. Another technique is ‘transposition’, or swapping of bytes.

Modern ciphers break into two types; symmetric and asymmetric.

Symmetric ciphers come in two flavours: block and stream.

Until now, we have been playing with classical ciphers, approximating ‘block’ ciphers. A block cipher is done in fixed size blocks (suprise!). For example, in the previous paragraphs we discussed breaking text and keys into 256 byte blocks, and working on those blocks. Block ciphers use a fixed key to perform substituion and transposition ciphers on each block discretely.

Its time to employ a stream cipher. A stream cipher attempts to create an on-the-fly ‘random’ keystream to encrypt the incoming plaintext one byte at a time. Typically, the ‘random’ key byte is xor’d with the plaintext to produce the ciphertext. If the random keystream can be replicated at the recieving end, then a further xor will produce the plaintext once again.

From this example forward, we will be working with bytes, not ASCII text, so a hex editor/dumper like hexdump is a necessity. Now is the right time to start to learn to use tools like cryptool.

In this example, the keyfile is in your directory, however it is not readable by you. The binary ‘encrypt6’ is also available. It will read the keyfile and encrypt any message you desire, using the key AND a ‘random’ number. You get to perform a ‘known ciphertext’ attack by introducing plaintext of your choice. The challenge here is not simple, but the ‘random’ number generator is weak.

As stated, it is now that we suggest you begin to use public tools, like cryptool, to help in your analysis. You will most likely need a hint to get going. See ‘HINT1’ if you need a kicktstart.

If you have further difficulty, there is a hint in ‘HINT2’.

The password for level 7 (krypton7) is encrypted with ‘encrypt6’.

# HINTS

None

# SOLUTION

Code:
```
import sys
sys.path.append('/home/nikhilh/')
from time import sleep

from pwn import *
from cipher_systems.caesar_cipher.break_caesar_cipher import CaesarCracker

plaintext = ""

remote_ssh = ssh("krypton6", "krypton.labs.overthewire.org", port=2222, password="RANDOM")
io = remote_ssh.process('sh', shell=True)

io.sendline('cd /krypton/krypton6/')
log.info('Switched to krypton6 directory')

io.sendline('mkdir /tmp/level6/')
log.info("Created /tmp/level6/ directory")

krypton7 = remote_ssh.download_data('/krypton/krypton6/krypton7')
pad_len = len(krypton7)

cmd = "python -c 'print (\"A\"*" + str(pad_len) + ")' > /tmp/level6/P1"
io.sendline(cmd)
io.sendline('./encrypt6 /tmp/level6/P1 /tmp/level6/C1')
log.info("Encrypted test input 1")

cmd = "python -c 'print (\"B\"*" + str(pad_len) + ")' > /tmp/level6/P2"
io.sendline(cmd)
io.sendline('./encrypt6 /tmp/level6/P2 /tmp/level6/C2')
log.info("Encrypted test input 2")

P1 = remote_ssh.download_data('/tmp/level6/P1')
P2 = remote_ssh.download_data('/tmp/level6/P2')
C1 = remote_ssh.download_data('/tmp/level6/C1')
C2 = remote_ssh.download_data('/tmp/level6/C2')

log.info("Checking differential analysis")
log.debug("C1: " + str(C1))
log.debug("C2: " + str(C2))

if log.debug:
    for index in range(len(C1)):
        log.debug(str(C2[index]) + " - " + str(C1[index]) + " = " + \
                  str(ord(C2[index]) - ord(C1[index])))

log.debug("Checking shift values: P1")
log.debug("P1: " + str(P1))
log.debug("C1: " + str(C1))

if log.debug:
    for index in range(len(C1)):
        log.debug(str(C1[index]) + " - " + str(P1[index]) + " = " + \
                 str(ord(C1[index]) - ord(P1[index])))

log.debug("Checking shift values: P2")
log.debug("P1: " + str(P2))
log.debug("C1: " + str(C2))

shift_indices = []
for index in range(len(C1)):
    shift_indices.append((ord(C2[index]) - ord(P2[index])))
    log.debug(str(C2[index]) + " - " + str(P2[index]) + " = " + \
             str(ord(C2[index]) - ord(P2[index])))

log.debug("Shift indices: " + str(shift_indices))

log.info("Shifting krypton7 file contents")
log.debug("krypton7: " + str(krypton7))
for index, value in enumerate(shift_indices):
    if value >= 13:
        value -= 26
    diff = chr(ord(krypton7[index]) - value)
    plaintext += diff
    log.debug(str(krypton7[index]) + " is shifted by " + str(value) + " places to " + str(diff))
    
log.info("Plaintext: " + str(plaintext))

io.sendline('rm -rf /tmp/level6/')
log.info("Deleted /tmp/level6/ directory")

remote_ssh.close()
```

Output:
```
nikhilh@ubuntu:~/overthewire/krypton/level6$ python auth.py 
[+] Connecting to krypton.labs.overthewire.org on port 2222: Done
[*] krypton6@krypton.labs.overthewire.org:
    Distro    Ubuntu 14.04
    OS:       linux
    Arch:     amd64
    Version:  4.4.0
    ASLR:     Disabled
    Note:     Susceptible to ASLR ulimit trick (CVE-2016-3672)
[+] Starting remote process '/bin/sh' on krypton.labs.overthewire.org: pid 34
[*] Switched to krypton6 directory
[*] Created /tmp/level6/ directory
[+] Downloading '/krypton/krypton6/krypton7': Found '/krypton/krypton6/krypton7' in ssh cache
[*] Encrypted test input 1
[*] Encrypted test input 2
[+] Downloading '/tmp/level6/P1': Found '/tmp/level6/P1' in ssh cache
[+] Downloading '/tmp/level6/P2': Found '/tmp/level6/P2' in ssh cache
[+] Downloading '/tmp/level6/C1': Found '/tmp/level6/C1' in ssh cache
[+] Downloading '/tmp/level6/C2': Found '/tmp/level6/C2' in ssh cache
[*] Checking differential analysis
[*] Shifting krypton7 file contents
[*] Plaintext: LFSRISNOTRANDOM
[*] Deleted /tmp/level6/ directory
[*] Closed connection to 'krypton.labs.overthewire.org'
```

# FLAG

LFSRISNOTRANDOM
