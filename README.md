# OverTheWire
OverTheWire walkthrough

I decided to sharpen my basic linux knowledge to finally do OverTheWire, these are just my personal notes of the levels so I might actually learn something :). 

# Level 0

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Commands you may need to solve this level
ls , cd , cat , file , du , find

TIP: Create a file for notes and passwords on your local machine!

Passwords for levels are not saved automatically. If you do not save them yourself, you will need to start over from bandit0.

Passwords also occasionally change. It is recommended to take notes on how to solve each challenge. As levels get more challenging, detailed notes are useful to return to where you left off, reference for later problems, or help others after you’ve completed the challenge.

Should be easy enough, use the command "ssh -p 2220 bandit0@bandit.labs.overthewire.org" with the password "bandit0" and you're in.
We look around using "ls" and read the readme.

```bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If ```bash

And there is the password for the next level. 

# Level 1 

The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find

Helpful Reading Material
Google Search for “dashed filename”
Advanced Bash-scripting Guide - Chapter 3 - Special Characters

When connected to Bandit1 we see this when using ll:
``` bandit1@bandit:~$ ll
total 24
-rw-r-----  1 bandit2 bandit1   33 Apr 10 14:23 -
drwxr-xr-x  2 root    root    4096 Apr 10 14:23 ./
drwxr-xr-x 70 root    root    4096 Apr 10 14:24 ../
-rw-r--r--  1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root    root    3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root    root     807 Mar 31  2024 .profile ```bash

We can use the simple cat command on the "-" file. But if we define the current working directory before the "-" file, we can cat it :).

``` bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx ```bash

