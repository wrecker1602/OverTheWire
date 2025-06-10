# OverTheWire Natas
OverTheWire Natas walkthrough

After the Bandit adventure, it's time to continue with Natas and web stuff :).

Natas teaches the basics of serverside web-security.

Each level of natas consists of its own website located at http://natasX.natas.labs.overthewire.org, where X is the level number. There is no SSH login. To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.

Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. All passwords are also stored in /etc/natas_webpass/. E.g. the password for natas5 is stored in the file /etc/natas_webpass/natas5 and only readable by natas4 and natas5.

Start here:

Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org

When we log in with the credentials, we get presented with and hint on the page: "You can find the password for the next level on this page.
".
So when we inspect elements we can easily see the password for the next level:
```html
<div id="content">
You can find the password for the next level on this page.

<!--The password for natas1 is 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq -->
</div>
```

# Natas 1

You can find the password for the next level on this page, but rightclicking has been blocked!

Luckily we can still open the developers tools just fine in the browser itself :).

```html
<div id="content">
You can find the password for the
next level on this page, but rightclicking has been blocked!

<!--The password for natas2 is TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI -->
</div>
```

# Natas 2

There is nothing on this page 

```html
<div id="content">
There is nothing on this page
<img src="files/pixel.png">
</div>
```
But there is a file! I don't see anything special about the file directly though. We are in luck though, the directory containing the .png is open for the public (http://natas2.natas.labs.overthewire.org/files/) and there is a users.txt file in there.
```txt
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```

# Natas 3

There is nothing on this page

```html
<div id="content">
There is nothing on this page
<!-- No more information leaks!! Not even Google will find it this time... -->
</div>
```
That is interresting, google normally scrapes websites but checks robots.txt for useragents that aren't allowed to scrape and what they aren't allowed to scrape. So let's check it.
http://natas3.natas.labs.overthewire.org/robots.txt contains: 
```txt
User-agent: *
Disallow: /s3cr3t/
```
Let's check the dir, and it contains an users.txt!
```txt
natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```

# Natas 4 

Access disallowed. You are visiting from "http://natas4.natas.labs.overthewire.org/index.php" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/"

