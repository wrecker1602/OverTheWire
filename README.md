# OverTheWire
OverTheWire walkthrough

I decided to sharpen my basic linux knowledge to finally do OverTheWire, these are just my personal notes of the levels so I might actually learn something :). 
If you somehow stumble upon this repo and use it to look for tips on how to solve levels, keep in mind that the passwords rotate so they will probs not work for you.

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

```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If 
```

And there is the password for the next level. 

# Level 1 

The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find

Helpful Reading Material
Google Search for “dashed filename”
Advanced Bash-scripting Guide - Chapter 3 - Special Characters

When connected to Bandit1 we see this when using ll:
```bash
bandit1@bandit:~$ ll
total 24
-rw-r-----  1 bandit2 bandit1   33 Apr 10 14:23 -
drwxr-xr-x  2 root    root    4096 Apr 10 14:23 ./
drwxr-xr-x 70 root    root    4096 Apr 10 14:24 ../
-rw-r--r--  1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root    root    3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root    root     807 Mar 31  2024 .profile 
```

We can use the simple cat command on the "-" file. But if we define the current working directory before the "-" file, we can cat it :).

```bash 
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

# Level 2

The password for the next level is stored in a file called spaces in this filename located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find

Helpful Reading Material
Google Search for “spaces in filename”

```bash
bandit2@bandit:~$ ll
total 24
drwxr-xr-x  2 root    root    4096 Apr 10 14:23 ./
drwxr-xr-x 70 root    root    4096 Apr 10 14:24 ../
-rw-r--r--  1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root    root    3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root    root     807 Mar 31  2024 .profile
-rw-r-----  1 bandit3 bandit2   33 Apr 10 14:23 spaces in this filename
```

We can very simpely get the contents of the file using quotes.

```bash
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

# Level 3

The password for the next level is stored in a hidden file in the inhere directory.

Commands you may need to solve this level
ls , cd , cat , file , du , find

Let's go to the "inhere" directory and then use ll again to find hidden files. Then ofcourse cat the hidden file.

```bash
bandit3@bandit:~$ ll
total 24
drwxr-xr-x  3 root root 4096 Apr 10 14:23 ./
drwxr-xr-x 70 root root 4096 Apr 10 14:24 ../
-rw-r--r--  1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root root 3771 Mar 31  2024 .bashrc
drwxr-xr-x  2 root root 4096 Apr 10 14:23 inhere/
-rw-r--r--  1 root root  807 Mar 31  2024 .profile
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ll
total 12
drwxr-xr-x 2 root    root    4096 Apr 10 14:23 ./
drwxr-xr-x 3 root    root    4096 Apr 10 14:23 ../
-rw-r----- 1 bandit4 bandit3   33 Apr 10 14:23 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

# Level 4 

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Commands you may need to solve this level
ls , cd , cat , file , du , find

Let's go in the inhere dir again, when using ll we see a multitude of files, we again have to define the working directory otherwise we get an error: 

```bash 
cat: invalid option -- 'f'
Try 'cat --help' for more information."
```

The files are all the same size, but when trying to read them they mostly give random nonsense. So after catting the files we see one with an readable string.

```bash
bandit4@bandit:~/inhere$ ll
total 48
drwxr-xr-x 2 root    root    4096 Apr 10 14:23 ./
drwxr-xr-x 3 root    root    4096 Apr 10 14:23 ../
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file00
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file01
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file02
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file03
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file04
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file05
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file06
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file07
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file08
-rw-r----- 1 bandit5 bandit4   33 Apr 10 14:23 -file09
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

# Level 5

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable
Commands you may need to solve this level
ls , cd , cat , file , du , find

We need to find the file in the inhere folder, luckily we know that the file is an 1033 bytes in size. This will help us tremendously with the find command.

```bash
bandit5@bandit:~$ find -size 1033c
./inhere/maybehere07/.file2
```

We need to use the "c" after the size to define that we are looking for bytes. Let's cat our password file.

```bash
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

# Level 6

