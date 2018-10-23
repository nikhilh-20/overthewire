# LEVEL GOAL

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

# SOLUTION

`nikhilh@ubuntu:~/projects/overthewire-bandit/bandit15$ ssh -p 2220 bandit15@bandit.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit15@bandit.labs.overthewire.org's password: 
               
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

`bandit15@bandit:~$ cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -ign_eof`

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

`    Session-ID: 2C7C8FAC4D3BC038930456490FCB5A6F65EFB07F644029A7AB9890E2DE2CB8B1`

`    Session-ID-ctx: `

`    Master-Key: 1C36AA00F0B3B837EA8B99B4CC70CCC1C095386A29573E56A4A6790000E562FF0A31A74FDC5005DBFCAF1D4500A39676`

`    Key-Arg   : None`

`    PSK identity: None`

`    PSK identity hint: None`

`    SRP username: None`

`    TLS session ticket lifetime hint: 7200 (seconds)`

`    TLS session ticket:`

`    0000 - 08 f0 15 a5 d6 6f a0 e8-06 d6 bb a4 0c 33 eb 04   .....o.......3..`

`    0010 - f9 f3 79 a5 36 b8 40 1a-68 62 35 4f fc f9 78 ff   ..y.6.@.hb5O..x.`

`    0020 - 5e 9b 00 d5 db 03 bb ac-47 17 cf f1 a4 cd ae e3   ^.......G.......`

`    0030 - e4 9f fb ff 63 63 10 ee-95 d3 9f 27 76 de f7 bd   ....cc.....'v...`

`    0040 - 2b 4b 85 ce 42 f1 03 bc-10 00 ac 71 85 30 35 92   +K..B......q.05.`

`    0050 - a8 e4 86 77 ea e3 8f dd-43 eb 03 a0 99 1c 04 e5   ...w....C.......`

`    0060 - d7 a2 57 42 92 be c4 62-69 1b 55 bd 99 96 b1 99   ..WB...bi.U.....`

`    0070 - e9 e1 44 c6 49 a7 c3 62-47 45 93 5e 6e 70 42 f9   ..D.I..bGE.^npB.`

`    0080 - 5f 9f 46 77 3d 2e d0 92-af eb 51 36 89 91 0b 25   _.Fw=.....Q6...%`

`    0090 - 9d 7f db e2 74 de a3 68-ec 7c 4a c4 36 69 ff 50   ....t..h.|J.6i.P`

`    Start Time: 1536009069`

`    Timeout   : 300 (sec)`

`    Verify return code: 18 (self signed certificate)`

`---`

`Correct!`

`cluFn7wTiGryunymYOu4RcffSxQluehd`

`closed`
