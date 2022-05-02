# How do you securely store passwords in a database?

## Table of contents

1. [Introduction](#introduction)
2. [Storing passwords](#storing-passwords)
    - [Hashing](#hashing)
    - [Salting](#salting)
    - [Peppering](#peppering)
    - [Encryption](#encryption)
3. [Combatting brute force attacks](#combatting-brute-force-attacks)
    
<br>    
<hr>

## Introduction

< Short introduction about password security >

<br>    
<hr>

## Storing passwords

Storing passwords in plaintext is obviously a no-go. If anyone got access to the login table in your database, they would instantly know everyone's login. Naturally, you could just make your database very secure, but there's only so much you can do. You can protect against SQL-injection, but you can't do much about vulnerabilities within your database engine, rogue employees or an unsuspecting employee falling for a phishing mail. Just ask a company called RockYou, which suffered a database-breach due to an unpatched SQL vulerability. Their passwords were stored in plaintext, and as a result, over 32 million passwords were leaked. <sup>[[RockYou hack: from bad to worse]](https://techcrunch.com/2009/12/14/rockyou-hack-security-myspace-facebook-passwords/)</sup>

So, even if a hacker were to get access to your database, you should ensure that they can't do anything with the passwords. This brings us to:

<br>    
<hr>

## Hashing

Hashing is a one-way algorithm that converts a readable, plaintext string into an unreadable representation of said string. There are many hashing algorithms out there, like the popular MD5, SHA-1 or the SHA-2 family. While these are still widely used, they are not meant for storing passwords. MD5 and SHA-1 have both been cryptographically broken <sup> [[MD5]](https://en.wikipedia.org/wiki/MD5) [[SHA-1]](https://en.wikipedia.org/wiki/SHA-1)</sup> while all of them are made to be fast (which may seem like a good thing, but password hashing algorithms should be slow). For these reasons, these types of hashing algorithms should only be used for their intended goal, verifying the integrity of files. There are some hashing algorithms made with the specific goal of hashing passwords, like Argon2. Argon2 won the [password hashing competition](https://www.password-hashing.net/) and enjoys a lot of praise in online discussions and articles. After comparing it to other password specific hashing algorithms I found that Argon2 is infact one of the best solutions out there currently, although it is likely this will change in a few years time.

However, this is not entirely secure yet. Hackers can use a rainbow table to quickly get most of the passwords from a database. A rainbow table is an enormous file containing billions of combinations of plaintext passwords along with their hashed representation. While these tables can take extremely long to initially generate, it would allow hackers to extract millions of hashed passwords from a database in mere seconds.

To combat rainbow tables, we can make use of:

<br>    
<hr>

## Salting

We can add a unique, randomly generated string to the hash. We store this salt along with the hashed password in the database. Now whenever we convert a password into its hashed variant, we first add this salt to the front or the end of the password. This takes rainbow tables out of the equation. It also ensures that even when 2 users have the same password, they will still have different hashes.

<br>    
<hr>

## Peppering

Alongside the salt, we can also choose to add a pepper. A pepper is virtually the same as a salt, the only 2 differences being that a pepper is stored as a secret in the application instead of in the database, and that a pepper is not unique, so every hash will have the same pepper. The advantage to having a pepper in addition to a salt is that the pepper will remain secret even if a hacker has complete access to the database. (Assuming the hacker does not also have access to the application).

<br>    
<hr>


## Encryption

An alternative to hashing is encryption. The upside to encryption is that you can retrieve a password from the encrypted value, the downside to encryption is that a hacker can retrieve a password from the encrypted value (assuming they know the encryption algorithm and key).

For this reason, it's *almost* always better to hash passwords instead of encrypting them. The one reason for using encryption is if your application **really** needs to be able to retrieve a user's password, for example a password manager.

<br>    
<hr>


## Combatting brute force attacks

In a brute force attack a hacker tries every possible password combination until they find the correct one. To shorten this process, hackers will often use dictionary attacks, using a literal dictionary of all words in the English alphabet or using a big file with common passwords. 

As the developer there is not much you can do to stop these types of attacks, but you can make it take so long that it just is not worth it. For starters, you can hash a password multiple times to increase the computation time. Ofcourse, you can't make it take too long, as regular users will suffer from that. 

**Other countermeasures include:** 
- Temporarily locking a user's account if there are a lot of failed login attempts in a short period of time, but this allows hackers to launch a DoS attack by locking out every user's account.
- Automatically temporarily blocking the IP of a suspected brute force attacker, but the hacker can circumvent this by constantly switching IP. This also has the risk of entire office buildings being blocked because one person thought it was funny to spam the login form.

**These countermeasures are not worth the trouble they may cause, so it's better to implement these instead:**
- Add a Captcha to the login form to block bots.
- Block a device/browser specifically when it is suspected of brute forcing.

<br>

**But the number one way to stop hackers from gaining access to your user's passwords using a brute force attack is:**
- Making sure your users use unique and difficult passwords.

