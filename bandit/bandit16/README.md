# LEVEL GOAL

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

# SOLUTION

`nikhilh@ubuntu:~/projects/overthewire-bandit/bandit16$ ssh -p 2220 bandit16@bandit.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit16@bandit.labs.overthewire.org's password: 
               
      ,----..            ,----,          .---. 
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' ' 
  |   :  | ; | ' ;    |.';  ; ;   \  \;      : 
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ; 
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"  
     \   \ .'        ;   |.'       \   \ ;     
  www. `---` ver     '---' he       '---" ire.org     
               
              
Welcome to OverTheWire!

If you find any problems, please report them to Steven or morla on
irc.overthewire.org.

--[ Playing the games ]--

  This machine might hold several wargames. 
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.

  Write-access to homedirectories is disabled. It is advised to create a
  working directory with a hard-to-guess name in /tmp/.  You can use the
  command "mktemp -d" in order to generate a random and hard to guess
  directory in /tmp/.  Read-access to both /tmp/ and /proc/ is disabled
  so that users can not snoop on eachother. Files and directories with 
  easily guessable or short names will be periodically deleted!
	
  Please play nice:
      
    * don't leave orphan processes running
    * don't leave exploit-files laying around
    * don't annoy other players
    * don't post passwords or spoilers
    * again, DONT POST SPOILERS! 
      This includes writeups of your solution on your blog or website!

--[ Tips ]--

  This machine has a 64bit processor and many security-features enabled
  by default, although ASLR has been switched off.  The following
  compiler flags might be interesting:

    -m32                    compile for 32bit
    -fno-stack-protector    disable ProPolice
    -Wl,-z,norelro          disable relro 

  In addition, the execstack tool can be used to flag the stack as
  executable on ELF binaries.

  Finally, network-access is limited for most levels by a local
  firewall.

--[ Tools ]--

 For your convenience we have installed a few usefull tools which you can find
 in the following locations:

    * peda (https://github.com/longld/peda.git) in /usr/local/peda/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /usr/local/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)
    * checksec.sh (http://www.trapkit.de/tools/checksec.html) in /usr/local/bin/checksec.sh

--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us through IRC on
  irc.overthewire.org #wargames.

  Enjoy your stay!

`bandit16@bandit:~$ nmap -p 31000-32000 localhost`

`Starting Nmap 7.01 ( https://nmap.org ) at 2018-09-03 23:14 CEST`

`Nmap scan report for localhost (127.0.0.1)`

`Host is up (0.00051s latency).`

`Other addresses for localhost (not scanned): ::1`

`Not shown: 996 closed ports`

`PORT      STATE SERVICE`

`31046/tcp open  unknown`

`31518/tcp open  unknown`

`31691/tcp open  unknown`

`31790/tcp open  unknown`

`31960/tcp open  unknown`

`Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds`

`bandit16@bandit:~$ cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31790 -ign_eof`

`CONNECTED(00000003)`

`depth=0 CN = bandit`

`verify error:num=18:self signed certificate`

`verify return:1`

`depth=0 CN = bandit`

`verify return:1`

`---`

`Certificate chain`

` 0 s:/CN=bandit`

`   i:/CN=bandit`

`---`

`Server certificate`

`-----BEGIN CERTIFICATE-----`

`MIICsjCCAZqgAwIBAgIJAKZI1xYeoXFuMA0GCSqGSIb3DQEBCwUAMBExDzANBgNV`

`BAMMBmJhbmRpdDAeFw0xNzEyMjgxMzIzNDBaFw0yNzEyMjYxMzIzNDBaMBExDzAN`

`BgNVBAMMBmJhbmRpdDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOcX`

`ruVcnQUBeHJeNpSYayQExCJmcHzSCktnOnF/H4efWzxvLRWt5z4gYaKvTC9ixLrb`

`K7a255GEaUbP/NVFpB/sn56uJc1ijz8u0hWQ3DwVe5ZrHUkNzAuvC2OeQgh2HanV`

`5LwB1nmRZn90PG1puKxktMjXsGY7f9Yvx1/yVnZqu2Ev2uDA0RXij/T+hEqgDMI7`

`y4ZFmuYD8z4b2kAUwj7RHh9LUKXKQlO+Pn8hchdR/4IK+Xc4+GFOin0XdQdUJaBD`

`8quOUma424ejF5aB6QCSE82MmHlLBO2tzC9yKv8L8w+fUeQFECH1WfPC56GcAq3U`

`IvgdjGrU/7EKN5XkONcCAwEAAaMNMAswCQYDVR0TBAIwADANBgkqhkiG9w0BAQsF`

`AAOCAQEAnrOty7WAOpDGhuu0V8FqPoKNwFrqGuQCTeqhQ9LP0bFNhuH34pZ0JFsH`

`L+Y/q4Um7+66mNJUFpMDykm51xLY2Y4oDNCzugy+fm5Q0EWKRwrq+hIM+5hs0RdC`

`nARP+719ddmUiXF7r7IVP2gK+xqpa8+YcYnLuoXEtpKkrrQCCUiqabltU5yRMR77`

`3wqB54txrB4IhwnXqpO23kTuRNrkG+JqDUkaVpvct+FAdT3PODMONP/oHII3SH9i`

`ar/rI9k+4hjlg4NqOoduxX9M+iLJ0Zgj6HAg3EQVn4NHsgmuTgmknbhqTU3o4IwB`

`XFnxdxVy0ImGYtvmnZDQCGivDok6jA==`

`-----END CERTIFICATE-----`

`subject=/CN=bandit`

`issuer=/CN=bandit`

`---`

`No client certificate CA names sent`

`---`

`SSL handshake has read 1015 bytes and written 631 bytes`

`---`

`New, TLSv1/SSLv3, Cipher is AES128-SHA`

`Server public key is 2048 bit`

`Secure Renegotiation IS supported`

`Compression: NONE`

`Expansion: NONE`

`No ALPN negotiated`

`SSL-Session:`

`    Protocol  : TLSv1`

`    Cipher    : AES128-SHA`

`    Session-ID: 980525228F041ADC8EF5DCB3AAF432393F1F7B0B3D95EE1C857964749B0CE943`

`    Session-ID-ctx: `

`    Master-Key: 551CE6559F4A5A2A921FBFCAA468463B64AD3473C0880998CBE7DA2E79251171F6F50F07E6333A6E0E316593DB5C4446`

`    Key-Arg   : None`

`    PSK identity: None`

`    PSK identity hint: None`

`    SRP username: None`

`    TLS session ticket lifetime hint: 7200 (seconds)`

`    TLS session ticket:`

`    0000 - aa 3d 08 f7 55 9a 83 cb-75 cb f1 ae ef 7b e3 4c   .=..U...u....{.L`

`    0010 - 49 b7 2e 92 00 11 62 01-5b bc ac 85 58 b4 1a dc   I.....b.[...X...`

`    0020 - 40 7a d2 a0 c7 1e 5b 2f-bb 03 af 4f eb 7c 35 13   @z....[/...O.|5.`

`    0030 - ab 77 96 0e f5 8a e1 e9-58 f2 e5 fe 01 c9 47 61   .w......X.....Ga`

`    0040 - 5b 35 57 d3 3c e3 88 d8-5c d7 fa 96 56 a7 2d 06   [5W.<...\...V.-.`

`    0050 - 49 a5 a6 4f 97 61 e8 6e-26 38 a8 af 7d ee 25 50   I..O.a.n&8..}.%P`

`    0060 - 8c f2 4d b3 bb 22 41 ac-64 18 62 43 28 74 64 d1   ..M.."A.d.bC(td.`

`    0070 - 9a 9a 2f 03 f2 71 81 3e-c0 36 c3 33 4b c7 70 46   ../..q.>.6.3K.pF`

`    0080 - 51 03 e3 55 04 16 12 52-41 b9 a8 60 11 93 39 4a   Q..U...RA..`..9J`

`    0090 - d1 b1 da fd 76 eb d9 04-e9 04 22 4b d6 a8 e5 ae   ....v....."K....`



`    Start Time: 1536009304`

`    Timeout   : 300 (sec)`

`    Verify return code: 18 (self signed certificate)`

`---`

`Correct!`

`-----BEGIN RSA PRIVATE KEY-----`

`MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ`

`imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ`

`Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu`

`DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW`

`JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX`

`x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD`

`KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl`

`J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd`

`d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC`

`YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A`

`vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama`

`+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT`

`8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx`

`SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd`

`HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt`

`SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A`

`R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi`

`Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg`

`R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu`

`L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni`

`blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU`

`YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM`

`77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b`

`dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3`

`vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=`

`-----END RSA PRIVATE KEY-----`

`closed`
