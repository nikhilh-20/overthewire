# LEVEL GOAL

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

# SOLUTION

`nikhilh@ubuntu:~/projects/overthewire-bandit/bandit12$ ssh -p 2220 bandit12@bandit.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit12@bandit.labs.overthewire.org's password: 
               
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

`bandit12@bandit:~$ ls`

`data.txt`

`bandit12@bandit:~$ cat data.txt`


`00000000: 1f8b 0808 ecf2 445a 0203 6461 7461 322e  ......DZ..data2.`

`00000010: 6269 6e00 0149 02b6 fd42 5a68 3931 4159  bin..I...BZh91AY`

`00000020: 2653 5930 3e1b 4000 0014 ffff dde3 2b6d  &SY0>.@.......+m`

`00000030: afff dd1e dfd7 ffbf bdfb 3f67 bfff ffff  ..........?g....`

`00000040: bde5 bfff aff7 bfdb e5ff ffef b001 39b0  ..............9.`

`00000050: 480d 3400 0068 0068 1a00 0000 01a3 4000  H.4..h.h......@.`

`00000060: 0001 a643 4d34 0000 d00d 0698 800d 1934  ...CM4.........4`

`00000070: d0c4 d034 1a36 a343 646a 1c9a 3206 9a00  ...4.6.Cdj..2...`

`00000080: 3406 8000 068d 064f 51a3 4000 000f 5000  4......OQ.@...P.`

`00000090: 6868 0034 d308 0da4 6990 1a03 4000 6869  hh.4....i...@.hi`

`000000a0: a0d0 00d3 2341 94d0 0006 8006 8034 1a34  ....#A.......4.4`

`000000b0: 00d0 d000 0310 d068 3400 001e 900d 1a19  .......h4.......`

`000000c0: 0062 68d3 4680 640f 48d0 d320 0068 621a  .bh.F.d.H.. .hb.`

`000000d0: 0543 0116 180c 6232 a7d7 82c8 7bd4 2374  .C....b2....{.#t`

`000000e0: 1de5 e375 b7b9 0b78 2d37 bd61 5cdf 40da  ...u...x-7.a\.@.`

`000000f0: b8e5 3258 213d e4bb ecb2 8d51 84f9 3bd0  ..2X!=.....Q..;.`

`00000100: b1c9 ef2a bcff 45cc 1f1c 0028 1cfe 8784  ...*..E....(....`

`00000110: 78a9 7611 0a81 c4d5 cb26 4b80 7888 c9bc  x.v......&K.x...`

`00000120: 2b3e a351 59ae c1fd 36c8 286e d6c3 bb2b  +>.QY...6.(n...+`

`00000130: b280 d19b 70b3 190a 0204 4603 9f79 e2b8  ....p.....F..y..`

`00000140: cf1b 8330 fcad 3780 86c2 5c3d 5bc9 4631  ...0..7...\=[.F1`

`00000150: 3718 5e2e a88c 34e6 8461 35ad c14f 6fd4  7.^...4..a5..Oo.`

`00000160: 31dd a5cc 5223 545e e01d ff23 cde3 22cc  1...R#T^...#..".`

`00000170: 22fa a62b e27a dfa5 d4f0 c326 28ef a4b3  "..+.z.....&(...`

`00000180: adc5 149c 1c27 dbc4 97b9 6342 487e bfe3  .....'....cBH~..`

`00000190: 02ee d63e 3379 8ebc d559 c670 7987 da1d  ...>3y...Y.py...`

`000001a0: 4c4b 5ec4 9965 075b 9d0b 08ee df17 d07c  LK^..e.[.......|`

`000001b0: ea9a 5fbf 43e7 d405 5239 1437 0c8a 34cd  .._.C...R9.7..4.`

`000001c0: be6f a949 b061 68e8 6ba5 c9ba 4112 0819  .o.I.ah.k...A...`

`000001d0: 7cb9 a3c8 bff1 0895 1819 8f80 407e dc32  |...........@~.2`

`000001e0: 9269 ca68 3f58 bb30 cd9b fcd6 0006 1224  .i.h?X.0.......$`

`000001f0: 177b fe66 c676 01f0 a5bc 9131 6746 cc85  .{.f.v.....1gF..`

`00000200: 1a39 e46f 6b9a 7bd4 694b e999 c300 b57e  .9.ok.{.iK.....~`

`00000210: 9b0a 1229 fac1 cc0c 24fb a905 a06a b8cf  ...)....$....j..`

`00000220: cb56 2a73 6016 6950 8208 5785 af54 0d42  .V*s`.iP..W..T.B`

`00000230: 754e 5a48 8835 2b47 aa9b c45e 4ca8 a7a0  uNZH.5+G...^L...`

`00000240: 61dd e070 7717 9346 5f14 d808 8263 7746  a..pw..F_....cwF`

`00000250: 5100 3af8 fa20 ff8b b922 9c28 4818 1f0d  Q.:.. ...".(H...`

`00000260: a000 e793 1e61 4902 0000                 .....aI...`


`bandit12@bandit:~$ mkdir /tmp/kenshin12`

`bandit12@bandit:~$ cp data.txt /tmp/kenshin12`

`bandit12@bandit:~$ cd /tmp/kenshin12`

`bandit12@bandit:/tmp/kenshin12$ ls`


`data.txt`

`bandit12@bandit:/tmp/kenshin12$ xxd -r data.txt > data`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data  data.txt`

`bandit12@bandit:/tmp/kenshin12$ rm data.txt`

`bandit12@bandit:/tmp/kenshin12$ file data`


`data: gzip compressed data, was "data2.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix`

`bandit12@bandit:/tmp/kenshin12$ mv data data.gz`

`bandit12@bandit:/tmp/kenshin12$ gzip -d data.gz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data`

`bandit12@bandit:/tmp/kenshin12$ file data`

`data: bzip2 compressed data, block size = 900k`

`bandit12@bandit:/tmp/kenshin12$ mv data data.bz`

`bandit12@bandit:/tmp/kenshin12$ bzip2 -d data.bz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data`

`bandit12@bandit:/tmp/kenshin12$ file data`

`data: gzip compressed data, was "data4.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix`

`bandit12@bandit:/tmp/kenshin12$ mv data data.gz`

`bandit12@bandit:/tmp/kenshin12$ gzip -d data.gz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data`

`bandit12@bandit:/tmp/kenshin12$ file data`

`data: POSIX tar archive (GNU)`

`bandit12@bandit:/tmp/kenshin12$ mv data data.tgz`

`bandit12@bandit:/tmp/kenshin12$ tar -xf data.tgz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data.tgz  data5.bin`

`bandit12@bandit:/tmp/kenshin12$ file data5.bin`

`data5.bin: POSIX tar archive (GNU)`

`bandit12@bandit:/tmp/kenshin12$ mv data5.bin data5.tgz`

`bandit12@bandit:/tmp/kenshin12$ rm data.tgz`

`bandit12@bandit:/tmp/kenshin12$ tar -xf data5.tgz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data5.tgz  data6.bin`

`bandit12@bandit:/tmp/kenshin12$ rm data5.tgz`

`bandit12@bandit:/tmp/kenshin12$ file data6.bin`

`data6.bin: bzip2 compressed data, block size = 900k`

`bandit12@bandit:/tmp/kenshin12$ mv data6.bin data.bz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data.bz`

`bandit12@bandit:/tmp/kenshin12$ bzip2 -d data.bz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data`

`bandit12@bandit:/tmp/kenshin12$ file data`

`data: POSIX tar archive (GNU)`

`bandit12@bandit:/tmp/kenshin12$ mv data data.tgz`

`bandit12@bandit:/tmp/kenshin12$ tar -xf data.tgz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data.tgz  data8.bin`

`bandit12@bandit:/tmp/kenshin12$ rm data.tgz`

`bandit12@bandit:/tmp/kenshin12$ file data8.bin`

`data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix`

`bandit12@bandit:/tmp/kenshin12$ mv data8.bin data.gz`

`bandit12@bandit:/tmp/kenshin12$ gzip -d data.gz`

`bandit12@bandit:/tmp/kenshin12$ ls`

`data`

`bandit12@bandit:/tmp/kenshin12$ file data`

`data: ASCII text`

`bandit12@bandit:/tmp/kenshin12$ cat data`

`The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`
