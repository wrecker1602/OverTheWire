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

The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size
Commands you may need to solve this level
ls , cd , cat , file , du , find , grep

We will need to find another file, but as we can predict with the information we have been given, we won't be able to find the file with only the find command with the -size syntax. So well need to add other options to the find command. 

```bash
bandit6@bandit:~$ find .-path / -group bandit6 -user bandit7 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

We define the path in the root dir because we'll need to search the whole system, then we define the group, user and size. And we add "2>/dev/null" at the end because otherwise we'll be spammed to death with folders we don't have permission to. With this command we found the password to let's cat it.

```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

# Level 7

The password for the next level is stored in the file data.txt next to the word millionth

Commands you may need to solve this level
man, grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

We know that the password is stored next to the word "millionth" in the data.txt file. We'll need to grep for that word in the text file to find the password.

```bash
bandit7@bandit:~$ grep millionth data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

# Level 8

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

Helpful Reading Material
Piping and Redirection

We know that the password is hidden in the data.txt file again and is the only string that is in there once. So we'll need to use the uniq and sort commands to sort the file for unique strings.

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

first we need to sort the data file, because uniq can only filter out on strings that are the same and adjecent to eachother. Then we use uniq -u to filter out the double strings.

# Level 9 

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

When trying to cat the data.txt file there is a lot of nonsense we can't read in there. So we can use strings to try and check for any readable strings.

```bash
bandit9@bandit:~$ strings -n 10 data.txt
========== the
========== password{k
=========== is
_$DM[q2 RO-;
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

We know we can expect a lot of nonsense of small random strings that can fill up the screen quite fast, so that's why we use -n 10, to filter out strings shorter than 10 chars. 

# Level 10

The password for the next level is stored in the file data.txt, which contains base64 encoded data

Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

Helpful Reading Material
Base64 on Wikipedia

Looking at the info the level gives us, we know that the string in the data.txt file is base64 encoded, so lets base64 decode the context of the file.

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

# Level 11

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

Helpful Reading Material
Rot13 on Wikipedia

This is a simple encryption, rot13 changes the position of a letter by 13 spaces, a -> n. So let's rotate the chars to their correct position. We can use an online site to do it for us, or use the "tr" command to rotate the chars.

```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

With the: 'A-Za-z' part of the command, we define the characters we want to rotate. With the 'N-ZA-Mn-za-m' part, we define that we want to rotate the characters 13 places.

# Level 12

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

Helpful Reading Material
Hex dump on Wikipedia

Let go to the /tmp dir and make a new folder there to do our stuff in.

```bash
bandit12@bandit:~$ cd /tmp
bandit12@bandit:/tmp$ mktemp -d
/tmp/tmp.yc3OUUhmS5
bandit12@bandit:/tmp$ cd tmp.yc3OUUhmS5
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ cp ~/data.txt .
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 9984
drwx------    2 bandit12 bandit12     4096 May 23 20:28 ./
drwxrwx-wt 4821 root     root     10211328 May 23 20:28 ../
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
```

Here we go to the tmp folder, make a new tmp folder, get in it, and copy the data.txt file into the dir we're in (. part of the command). Let's start decompress the file.

