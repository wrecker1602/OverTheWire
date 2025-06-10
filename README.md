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

```bash
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ xxd -r data.txt > data.bin
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data.bin
data: gzip compressed data, was "data2.bin", last modified: Thu Apr 10 14:22:57 2025, max compression, from Unix, original size modulo 2^32 585
```

We can use xxd to look at the data.txt file and see it's hexdump, with the -r flag we can revert it into a binary, the "> data" puts the output in the file "data". Now let's start decompressing the file. 

```bash
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data.bin data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ gzip data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 9988
drwx------    2 bandit12 bandit12     4096 May 23 20:34 ./
drwxrwx-wt 4828 root     root     10211328 May 23 20:34 ../
-rw-rw-r--    1 bandit12 bandit12       25 May 23 20:34 data
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data
data: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data data.bz2
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ bzip2 -d data.bz2
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 9988
drwx------    2 bandit12 bandit12     4096 May 23 20:42 ./
drwxrwx-wt 4836 root     root     10211328 May 23 20:42 ../
-rw-rw-r--    1 bandit12 bandit12      443 May 23 20:40 data
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data
data: gzip compressed data, was "data4.bin", last modified: Thu Apr 10 14:22:57 2025, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ gzip -d data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ tar -xvf data.tar
data5.bin
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 10016
drwx------    2 bandit12 bandit12     4096 May 23 20:45 ./
drwxrwx-wt 4839 root     root     10211328 May 23 20:45 ../
-rw-r--r--    1 bandit12 bandit12    10240 Apr 10 14:22 data5.bin
-rw-rw-r--    1 bandit12 bandit12    20480 May 23 20:40 data.tar
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data5.bin data2.tar
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ tar -xvf data2.tar
data6.bin
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data6.bin data.bz2
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ bzip2 -d data.bz2
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 10028
drwx------    2 bandit12 bandit12     4096 May 23 20:47 ./
drwxrwx-wt 4839 root     root     10211328 May 23 20:47 ../
-rw-r--r--    1 bandit12 bandit12    10240 Apr 10 14:22 data
-rw-r--r--    1 bandit12 bandit12    10240 Apr 10 14:22 data2.tar
-rw-rw-r--    1 bandit12 bandit12    20480 May 23 20:40 data.tar
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data data3.tar
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ tar -xvf data3.tar
data8.bin
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Apr 10 14:22:57 2025, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ mv data8.bin data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ gzip -d data.gz
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ ll
total 10032
drwx------    2 bandit12 bandit12     4096 May 23 20:48 ./
drwxrwx-wt 4840 root     root     10211328 May 23 20:48 ../
-rw-r--r--    1 bandit12 bandit12       49 Apr 10 14:22 data
-rw-r--r--    1 bandit12 bandit12    10240 Apr 10 14:22 data2.tar
-rw-r--r--    1 bandit12 bandit12    10240 Apr 10 14:22 data3.tar
-rw-rw-r--    1 bandit12 bandit12    20480 May 23 20:40 data.tar
-rw-r-----    1 bandit12 bandit12     2646 May 23 20:28 data.txt
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ file data
data: ASCII text
bandit12@bandit:/tmp/tmp.yc3OUUhmS5$ cat data
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

After that lengty process, we got the password :).

# Level 13

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

Commands you may need to solve this level
ssh, telnet, nc, openssl, s_client, nmap

```bash
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

Now that we have the ssh key we can use this to connect to the next user. So lets copy this into a .key file and use it to authenticate to the next level :).

```bash
wrecker1602@wrecker:/localdir$ nano ssh.key

wrecker1602@wrecker:/localdir$ ssh -i ssh.key -p 2220 bandit14@bandit.labs.overthewire.org
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0777 for 'ssh.key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "ssh.key": bad permissions
bandit14@bandit.labs.overthewire.org's password:
```

The permissions of the ssh.key file we made is too open, so let's fix that real quick.

We can do that with the commands: 
```bash
wrecker1602@wrecker:/localdir$ mkdir ~/.ssh/id_rsa/
wrecker1602@wrecker:/localdir$ mv ssh.key ~/.ssh/id_rsa/ssh.key
wrecker1602@wrecker:/localdir$ chmod 600 ~/.ssh/id_rsa/ssh.key
wrecker1602@wrecker:/localdir$ ssh -i ~/.ssh/id_rsa/ssh.key -p 2220 bandit14@bandit.labs.overthewire.org
bandit14@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root root 4096 Apr 10 14:22 .
drwxr-xr-x 70 root root 4096 Apr 10 14:24 ..
-rw-r--r--  1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root root 3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root root  807 Mar 31  2024 .profile
drwxr-xr-x  2 root root 4096 Apr 10 14:22 .ssh
bandit14@bandit:~/.ssh$ cat  /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

And we are in.

# Level 14

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Commands you may need to solve this level
ssh, telnet, nc, openssl, s_client, nmap

```bash
bandit14@bandit:~/.ssh$ cat authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGSQ4TzdbZw5PshaEVz1o9ppCZAN2DO5cK/6mlkdr75u5KQ36CDS1yvsXDw0sZrn5TN5zasSDRaZ568HXcAihinQxnIROrjq36OT2m43BnAi31eAFm58a1kTBZsVbD+9Us3A5cF7hRZK0ZFbOA+kR5K/lNvVWMtkgF0amFMgrbYCbPpltOEyyIyfIlp8TAn9Pw9A7ebJL3W9QcS6g4wDOhQgPiQ3QwRnf5dqHIrQclWrrwqxU5t59cbW+8DcYAnb2TElqq9F+BiepmvJY3vDcIeM1Thz/YmSn6fwvRKfFo0D5ZgDuOI/JMXSKzy7MyVhDiXUvOH/z8ym+EJAXyvbZ3 rudy@localhost
```

We can see there is an authorised key, maybe we can try that on the port 30000.

After screwing around a bit I noticed that I didn't properly read the level description. So I read it again and and just used netcat to connect to localhost on port 30000, after putting the password of the current level in I got the new password I needed.

```bash
bandit14@bandit:~$ nc localhost 30000
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

# Level 15

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

Commands you may need to solve this level
ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

We can use openssl for the ssl/tls connection to port 30001 on localhost, so let's do so.

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 4332BD707D310F51A87146B626871EEE79B8464F4730127976FB870347D83702
    Session-ID-ctx:
    Resumption PSK: 21DE0296FCEE767E1620F23445608982FB3E113ECB6EA1889434052A78CF6AB32EE9079770371C97C6ABEA73EB1D301A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 0e f0 8e f1 8e 86 8d b1-e5 ea ae 09 1f c3 e0 85   ................
    0010 - 05 ac 31 db e6 be 77 cb-8b c2 06 be c8 59 30 dc   ..1...w......Y0.
    0020 - 73 20 4f 1a 56 58 1b b7-b2 e9 8d 0e f4 56 05 95   s O.VX.......V..
    0030 - ce d8 e8 5a 10 19 66 e0-f7 25 ba aa 92 1c 32 52   ...Z..f..%....2R
    0040 - 80 0b 72 18 41 b1 24 a5-b4 07 32 22 44 45 f4 ca   ..r.A.$...2"DE..
    0050 - 53 17 68 61 13 e1 e2 c7-e5 25 55 a7 1b 55 b6 62   S.ha.....%U..U.b
    0060 - be a1 0c 31 c8 c9 e2 a6-a0 2f 87 39 69 1b a6 53   ...1...../.9i..S
    0070 - 2b e6 24 87 1b 9a 04 22-08 2a ea df 30 04 1a 07   +.$....".*..0...
    0080 - b2 66 b5 46 1d 01 1e 65-de f9 6f 09 e5 da 09 dd   .f.F...e..o.....
    0090 - 12 1b 57 9e a1 cb eb 3c-ee 3c ce 4b af 62 47 7a   ..W....<.<.K.bGz
    00a0 - 61 c4 49 4d 44 67 4c 3d-a3 f0 cf 20 68 57 f7 b9   a.IMDgL=... hW..
    00b0 - 92 80 7c d3 2b 0b 50 28-97 cf 3b d5 3b 74 9b 30   ..|.+.P(..;.;t.0
    00c0 - a9 47 f7 85 31 5e 69 65-06 5e fd 44 f9 f8 8a e8   .G..1^ie.^.D....
    00d0 - 96 82 ef be 89 11 7c 6a-83 78 f4 f6 12 0e 54 b5   ......|j.x....T.

    Start Time: 1749512713
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 51D20F01932B17836820924912B39B90D16A00EFB21F8CB2275584FF27A10C5D
    Session-ID-ctx:
    Resumption PSK: BAC3DB92C3271776207A75F48DEAD9D9E65F349356769E5B1AB846CD4E3DA50F48881386DB96B7D863153B081EC87A25
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 0e f0 8e f1 8e 86 8d b1-e5 ea ae 09 1f c3 e0 85   ................
    0010 - ad b6 ab 0a 70 66 1a b9-b7 46 b1 26 81 48 73 51   ....pf...F.&.HsQ
    0020 - ce d3 6b d0 76 64 be 69-73 6f d1 ea 87 7c e7 43   ..k.vd.iso...|.C
    0030 - 77 fc e6 a5 7d 2e fe a8-f8 ee de a0 32 28 2a 3f   w...}.......2(*?
    0040 - a2 7c 92 13 d3 c4 30 9c-b3 40 bb 70 dc 62 61 ef   .|....0..@.p.ba.
    0050 - 11 34 4e 78 98 e7 9c 64-9d cc 34 d0 cd f8 4d d6   .4Nx...d..4...M.
    0060 - 91 39 60 14 c0 75 d9 33-38 7e 3e c7 05 77 1a e1   .9`..u.38~>..w..
    0070 - d6 50 0f e8 0d 31 3b d3-2f 13 8e 86 b3 7e 13 37   .P...1;./....~.7
    0080 - 1e 8f 9f 6d b2 e9 35 ce-69 21 05 66 d5 6f 24 ac   ...m..5.i!.f.o$.
    0090 - 7e d5 10 c2 36 ad f6 f7-2e 5f c0 36 92 57 36 28   ~...6...._.6.W6(
    00a0 - ec 4e 3e 27 75 5d fc f3-32 31 d2 e6 e9 25 3e 8f   .N>'u]..21...%>.
    00b0 - 94 22 ce 7e 23 86 ea 51-9f 2a 19 59 66 c6 66 50   .".~#..Q.*.Yf.fP
    00c0 - 6a a0 54 a3 e9 b2 c4 4e-4a 8b 7f 44 05 30 57 a2   j.T....NJ..D.0W.
    00d0 - da 89 30 d4 44 ce 0a 2f-89 20 ac 09 27 94 a4 8c   ..0.D../. ..'...

    Start Time: 1749512713
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
```

# Level 16

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

Commands you may need to solve this level
ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

Let's perform an nmap scan to see which ports are open for the ssl/tls connection.

```bash
bandit16@bandit:~$ nmap -sV -p 31000-32000 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-10 00:04 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.94SVN%T=SSL%I=7%D=6/10%Time=684776BE%P=x86_64-pc-linu
SF:x-gnu%r(GenericLines,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x2
SF:0current\x20password\.\n")%r(GetRequest,32,"Wrong!\x20Please\x20enter\x
SF:20the\x20correct\x20current\x20password\.\n")%r(HTTPOptions,32,"Wrong!\
SF:x20Please\x20enter\x20the\x20correct\x20current\x20password\.\n")%r(RTS
SF:PRequest,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20
SF:password\.\n")%r(Help,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x
SF:20current\x20password\.\n")%r(FourOhFourRequest,32,"Wrong!\x20Please\x2
SF:0enter\x20the\x20correct\x20current\x20password\.\n")%r(LPDString,32,"W
SF:rong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\.\n")
SF:%r(SIPOptions,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20curren
SF:t\x20password\.\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 150.32 seconds
```

We can see that the port 31518 and 31790 is accepting ssl connections. But since port 31518 just echo's it's probs the other one. So let's connect to that one.

When we however connect to that port we only get KEYUPDATE and nothing else. If we however use the -quiet flag with the openssl command, it does properly work and in return we get an ssh key.

```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

We can use this for the next level!

# Level 17

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

Commands you may need to solve this level
cat, grep, ls, diff

```bash
wrecker1602@wrecker:/localdir$ nano ssh2.key
wrecker1602@wrecker:/localdir$ mv ssh2.key ~/.ssh/id_rsa/ssh2.k
ey
wrecker1602@wrecker:/localdir$ chmod 600 ~/.ssh/id_rsa/ssh2.key
wrecker1602@wrecker:/localdir$ ssh -i ~/.ssh/id_rsa/ssh2.key -p2220 bandit17@bandit.labs.overthewire.org
```

Quite an easy one,

```bash
bandit17@bandit:~$ diff passwords.new passwords.old
42c42
< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
---
> C6XNBdYOkgt5ARXESMKWWOUwBeaIQZ0Y
```

# Level 18

Level Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Commands you may need to solve this level
ssh, ls, cat

We can't use ssh to login, but maybe we can use ssh to read the readme file without logging into the account but just using the credentials. So let's try that.

```bash
wrecker1602@wrecker:/localdir$ ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat ~/readme"
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

Load key "/home/wrecker1602/.ssh/id_rsa": Is a directory
bandit18@bandit.labs.overthewire.org's password: 
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

And we can!

# Level 19

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Let's try to do what the description tells us to.

```bash
bandit19@bandit:~$ ll
total 36
drwxr-xr-x  2 root     root      4096 Apr 10 14:23 ./
drwxr-xr-x 70 root     root      4096 Apr 10 14:24 ../
-rwsr-x---  1 bandit20 bandit19 14884 Apr 10 14:23 bandit20-do*
-rw-r--r--  1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root     root      3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root     root       807 Mar 31  2024 .profile
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

The binary runs with higher privs than the person executing it, that is why we can read the password file with a lower priv user.

# Level 20

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Commands you may need to solve this level
ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

```bash
bandit20@bandit:~$ ll
total 36
drwxr-xr-x  2 root     root      4096 Apr 10 14:23 ./
drwxr-xr-x 70 root     root      4096 Apr 10 14:24 ../
-rw-r--r--  1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root     root      3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root     root       807 Mar 31  2024 .profile
-rwsr-x---  1 bandit21 bandit20 15608 Apr 10 14:23 suconnect*
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```

This one was quite tricky for me since I didn't fully understand the description. they want you to setup an nc listener with the password of the last level to echo it. And then use the binary to connect to said netcat port. I used tmax to run the netcat listener in the background.

```bash
bandit20@bandit:~$ echo -n '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' | nc -lvp 1337
Listening on 0.0.0.0 1337
[detached (from session 2)]
bandit20@bandit:~$ ./suconnect 1337 
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
Connection received on localhost 33916
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

And we've got the password.

# Level 21

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Commands you may need to solve this level
cron, crontab, crontab(5) (use “man 5 crontab” to access this)

First we'll look at the cron jobs, after that we'll check the cronjob for the right bandit level, then we'll ofcourse read it.
```bash
bandit21@bandit:/etc/cron.d$ ll
total 48
drwxr-xr-x   2 root root  4096 Apr 10 14:24 ./
drwxr-xr-x 121 root root 12288 Apr 21 12:42 ../
-rw-r--r--   1 root root   123 Apr 10 14:16 clean_tmp
-rw-r--r--   1 root root   120 Apr 10 14:23 cronjob_bandit22
-rw-r--r--   1 root root   122 Apr 10 14:23 cronjob_bandit23
-rw-r--r--   1 root root   120 Apr 10 14:23 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-rwx------   1 root root    52 Apr 10 14:24 otw-tmp-dir*
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```
It seems that the password is right in the tmp folder with that file name :).

# Level 22

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Commands you may need to solve this level
cron, crontab, crontab(5) (use “man 5 crontab” to access this)

Let's read the correct cron job again.
```bash
bandit22@bandit:~$ ls /etc/cron.d/
clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  otw-tmp-dir  sysstat
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
The script seems to get the current user (for the case of this level: bandit22) and then gets the hash for the string: "I am user $myname ". The password file for that user then gets copied into a tmp file with the name of the md5 hash of said string.

```bash
bandit22@bandit:~$ whoami
bandit22
bandit22@bandit:~$ echo I am user bandit23 | md5sum
8ca319486bfbbc3663ea0fbe81326349  -
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
But we ofcourse need the get the password of the user bandit23 and not bandit22. So we use the same logic in the script and get the correct password.

# Level 23

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

Commands you may need to solve this level
chmod, cron, crontab, crontab(5) (use “man 5 crontab” to access this)

You know the drill.

```bash
bandit23@bandit:~$ ls /etc/cron.d/
clean_tmp  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  e2scrub_all  otw-tmp-dir  sysstat
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
This script runs all the files in the the folder: "/var/spool/bandit23/foo" as long as the owner of the script is: "bandit23". So lets create a simple bash script that will get the password file of the user bandit24.

The script I made:
```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/12345.txt
```
After much struggle with the output folder (dumb me didn't realise that the /home/bandit23 folder was not writable to) I got the script to work.

```bash
bandit23@bandit:~$ nano /var/spool/bandit24/foo/bash.sh
bandit23@bandit:~$ chmod +x /var/spool/bandit24/foo/bash.sh
bandit23@bandit:~$ ls -l /var/spool/bandit24/foo/bash.sh
-rwxrwxr-x 1 bandit23 bandit23 60 Jun 10 02:25 /var/spool/bandit24/foo/bash.sh
bandit23@bandit:~$ cat /tmp/12345.txt
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

# Level 24