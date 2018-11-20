# LEVEL GOAL

# HINTS

# SOLUTION

Code:
```
import sys
sys.path.append('/home/nikhilh/')
from time import sleep

from pwn import *
from cipher_systems.caesar_cipher.break_caesar_cipher import CaesarCracker

context.log_file = 'level6.log'
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
                  str((ord(C2[index]) - ord(C1[index])) % 26))

log.debug("Checking shift values: P1")
log.debug("P1: " + str(P1))
log.debug("C1: " + str(C1))

if log.debug:
    for index in range(len(C1)):
        log.debug(str(C1[index]) + " - " + str(P1[index]) + " = " + \
                 str((ord(C1[index]) - ord(P1[index])) % 26))

log.debug("Checking shift values: P2")
log.debug("P1: " + str(P2))
log.debug("C1: " + str(C2))

shift_indices = []
for index in range(len(C1)):
    shift_indices.append((ord(C2[index]) - ord(P2[index])) % 26)
    log.debug(str(C2[index]) + " - " + str(P2[index]) + " = " + \
             str((ord(C2[index]) - ord(P2[index])) % 26))

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
[+] Starting remote process '/bin/sh' on krypton.labs.overthewire.org: pid 35
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
