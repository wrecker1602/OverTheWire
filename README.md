# OverTheWire
OverTheWire walkthrough

I decided to sharpen my basic linux knowledge to finally do OverTheWire, these are just my personal notes of the levels so I might actually learn something :). 

# Level 0

```The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.```

Should be easy enough, use the command ```ssh -p 2220 bandit0@bandit.labs.overthewire.org``` with the password ```bandit0``` and you're in.
We look around using "ls" and read the readme.

```bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If```

And there is the password for the next level. 
