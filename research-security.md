# How do you securely store passwords in a database?

## Table of contents

1. [Introduction](#introduction)
2. [Storing passwords](#storing-passwords)
    - [Hashing](#hashing)
    - [Salting](#salting)
    - [Peppering](#peppering)
    - [Multiple iterations](#multiple-iterations)
    - [Encryption](#encryption)
    
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

However, this is not entirely secure yet. Let's say you got a hashed password from a database, and you know which hashing algorithm was used (for example, you can find the hashing algorithm by creating an account yourself and using your plaintext password in the most popular hashing algorithms until you find the one that matches the hash belonging to your login in the database). You could now use a dictionary attack (for example by using every English word or by using every password from the RockYou leak) to find which plaintext password belongs to the hash you are trying to crack. 

To prevent this, we can make use of:

<br>    
<hr>

## Salting

We can add a unique, randomly generated string to the hash. 
< Explain salting further >

<br>    
<hr>

## Peppering

Alongside the salt, we can also choose to add a pepper. A pepper is virtually the same as a salt, the only 2 differences being that a pepper is stored in the application instead of in the database, and that a pepper is not unique, so every hash will have the same pepper.
< Explain peppering further >

<br>    
<hr>

## Multiple iterations

Even with all these security measures in place, a hacker can still simply brute force their way to getting the passwords. To combat this, you can hash the hash multiple times. This increases the amount of times it takes to computate the hash which means brute forcing takes much, much longer.
< Explain the use of multiple iterations further >

<br>    
<hr>

## Encryption

< Explain encryption and why it's not the right choice for most applications >

<br>    
<hr>

