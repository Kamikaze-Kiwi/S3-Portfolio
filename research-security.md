# How do you securely store passwords in a database?

## Table of contents

1. [Introduction](#introduction)
2. [What are the most common methods for securing passwords?](#what-are-the-most-common-methods-for-securing-passwords)
    - [Hashing](#hashing)
    - [Salting](#salting)
    - [Peppering](#peppering)
    - [Encryption](#encryption)
3. [How can we combat brute force attacks?](#how-can-we-combat-brute-force-attacks)
    - [How does brute forcing work?](#how-does-brute-forcing-work)
    - [How can we make it take longer for a hacker to attempt a password?](#how-can-we-make-it-take-longer-for-a-hacker-to-attempt-a-password)
    - [How can we increase the amount of possible password combinations the hacker will need to try?](#how-can-we-increase-the-amount-of-possible-password-combinations-the-hacker-will-need-to-try)
4. [At what point will the user not want to bother with the password requirements anymore?](#at-what-point-will-the-user-not-want-to-bother-with-the-password-requirements-anymore)
5. [Conclusion](#conclusion)

<br>    
<hr>

## Introduction

Having an extremely secure authentication system is extremely important. I could just use one of the many great authentication systems out there like Auth0 or oAuth2, however I want to know what goes on behind the scenes. Last semester I already made an authentication system, but I chose not to invest more than 10 minutes in the security. I hashed the password with Sha256 and that was it. When I pasted some of the hashes into Google, I could immediately see what the original password was, and something's telling me that's not quite as safe as it should be.

To ensure that the methods I will use to handle the storing of passwords are ***really*** secure, we will assume that the hacker knows everything about my system and has access to the source code.

<br>    
<hr>

## What are the most common methods for securing passwords?

Storing passwords in plaintext is obviously a no-go. If anyone got access to the login table in your database, they would instantly know everyone's login. Naturally, you could just make your database very secure, but there's only so much you can do. You can protect against SQL-injection, but you can't do much about vulnerabilities within your database engine, rogue employees or an unsuspecting employee falling for a phishing mail. Just ask a company called RockYou, which suffered a database-breach due to an unpatched SQL vulerability. Their passwords were stored in plaintext, and as a result, over 32 million passwords were leaked. <sup>[[RockYou hack: from bad to worse]](https://techcrunch.com/2009/12/14/rockyou-hack-security-myspace-facebook-passwords/)</sup>

So we have to do something with the password to make it unreadable.

<br>    
<hr>

## Hashing

Hashing is a one-way algorithm that converts a readable, plaintext string into an unreadable representation of said string. There are many hashing algorithms out there, like the popular MD5, SHA-1 or the SHA-2 family. While these are still widely used, they are not meant for storing passwords. MD5 and SHA-1 have both been cryptographically broken <sup> [[MD5]](https://en.wikipedia.org/wiki/MD5) [[SHA-1]](https://en.wikipedia.org/wiki/SHA-1)</sup> while all of them are made to be fast (which may seem like a good thing, but password hashing algorithms should be slow, I will return to this later). For these reasons, these types of hashing algorithms should only be used for their intended goal, verifying the integrity of files. There are some hashing algorithms made with the specific goal of hashing passwords, like Argon2. Argon2 won the [password hashing competition](https://www.password-hashing.net/) and enjoys a lot of praise in online discussions and articles. After comparing it to other password specific hashing algorithms I found that Argon2 is infact one of the best solutions out there currently, although it is likely this will change in a few years time, as better algorithms are constantly being developed.

There are 2 main libraries in Java for using Argon2. Argon2-jvm and the built in Argon2 from Spring security. As I am using spring for my project anyway, I decided to go with the Spring security solution.

#

| **User** | **Password (Not stored)** | **Hash**         |
|----------|---------------------------|------------------|
| Jim      | Password123               | ca8b9d3867664f22 |
| Tim      | Password123               | ca8b9d3867664f22 |
| Bob      | 23k4gu28kj14#@uy!         | f36988f65cacd2b3 |
| John     | Oof                       | 3c7022f8fad45921 |

^ What the database would look like now. note how the hash is always the same length no matter the length of the password. Also note that Jim and Tim, who have the same password, have the same hash. The second row is not stored. While you can't see the password in the blink of an eye, it's still very easy to retrieve the passwords. The easiest way would be to use a rainbow table (assuming one exists). A rainbow table is an enormous file containing every possible (plaintext) password along with their hashed representation. This would allow the hacker to get every password nearly instantly.

<br>    
<hr>

## Salting

A salt is a randomly generated string added to the password before it is hashed. This salt is then also stored in the database along with the hashed password. This makes rainbow tables completely useless. An added bonus is that if multiple users have the same password, they will still have a different hash.

#

| **User** | **Password (Not stored)** | **Hash**         | **Salt**         |
|----------|---------------------------|------------------|------------------|
| Jim      | Password123               | 28dfe5cd7788a848 | 0HlZLASHl3GWBsUa |
| Tim      | Password123               | 7d5d0d11d9e15d19 | n68yVxfJpW1rR4vz |
| Bob      | 23k4gu28kj14#@uy!         | ab25635f7254b7f1 | nm68iO9ycJi9fbDl |
| John     | Oof                       | 0940c9263442c338 | dw5VSheLlSqPXVh4 |

^ What the database would look like now. Note that Jim and Tim now have different hashes, even though they have the same password. Now it is only possible to crack the passwords from this database by brute-forcing it. A hacker can test every possible password using the salt of one of the users, until the generated hash matches the hash in the database. John's password would be cracked within seconds, Jim and Tim's passwords will take a little longer and John's password will either never be cracked if the hacker did not include special characters in the brute force or after a decently long (but not crazy) amount of time. I will look into combatting brute force attacks [later](#combatting-brute-force-attacks).

<br>    
<hr>

## Peppering

Alongside the salt, it's also possible to add a pepper. A pepper is virtually the same as a salt, the only 2 differences being that a pepper is stored as a secret in the application instead of in the database, and that a pepper is not unique, so every hash will have the same pepper. The advantage to having a pepper in addition to a salt is that the pepper will remain secret even if a hacker has complete access to the database. (Assuming the hacker does not also have access to the application). However, for this research we are assuming that the hacker has complete access to the system, which includes this pepper. Adding a pepper will literally only take one line of code, so it's still worth the effort.

<br>    
<hr>


## Encryption

An alternative to hashing is encryption. The upside to encryption is that you can retrieve a password from the encrypted value, the downside to encryption is that a hacker can retrieve a password from the encrypted value (assuming they know the encryption algorithm and key).

For this reason, it's ***almost*** always better to hash passwords instead of encrypting them. The one reason for using encryption is if your application **really** needs to be able to retrieve a user's password, for example a password manager. In any other case you should always refrain from using encryption for your passwords.

<br>    
<hr>


## How can we combat brute force attacks?

## How does brute forcing work?
There are two ways hackers use brute force attacks. In the first one the hacker tries every possible password combination possible. This means the hacker will try every combination of all letters, uppercase letters, numbers, special characters ETC. This process takes extremely long, but it will eventually crack every single password in the system. Another way to do a brute force attack is also called a dictionary attack. With a dictionary attack, the hacker will only try certain passwords instead of trying every possible combination. To choose which passwords to try, the hacker might use a list of the most common passwords or all the passwords in previous password leaks. Alternatively, the hacker can use a program that attempts all the words in the (for example) English language, along with some variations of those words, like with numbers at the end.

## How can we make it take longer for a hacker to attempt a password?

To make it take longer for a hacker to attempt each password, we can increase the time it takes to compile the hash. We are already doing this by using a hashing algorithm that takes relatively long, but this is not enough to stop brute force hackers, especially as hardware gets faster and cheaper. To make it take even longer, we can repeat the hashing process multiple times, so after hashing the password, we will hash this hash again, and we will continue doing this until the hashing process takes long enough. If a hashing function normally takes about 0.1 seconds to execute, that means a hacker can test 10 passwords per second. If I do it with 10 iterations instead, the hacker can only test 1 password per second. The more iterations I do, the safer the passwords will be. But I have to find a balance between blocking hackers and giving the users a fast-working application. I personally went with 10 iterations as I found that it takes about a 800 ms (on my hardware) which seems like a good compromise. When hardware gets better in the future I can always increase the iterations.

## How can we increase the amount of possible password combinations the hacker will need to try?

Besides increasing the time it takes to try a single password, we can increase the amount of passwords the hacker will need to try. If our program only requires letters and numbers, the hacker will probably decide not to include special characters in their brute force attack, which decreases the amount of possible password combinations drastically. By enforcing the users to create stronger passwords. I can force them to be a certain length, require capital and lowercase letters, require a number, require a special character, etc. I can also check if the user's entered password is within a list of the *n* most common passwords, although this is redundant if I am already forcing the usage of a special character, as the top 10000 most common passwords don't contain a single special character anyway. It's important to not go overboard with the password requirements however. This could mean users won't be able to remember their passwords, which could push users to either do the bare minimum for their password (like 'Password123!', which has a uppercase letter, lowercase letters, numbers and a special character, but is stil a very bad password). Users might also decide to come up with a good password, but store it themselves in an unsecure way. 

| ![test](https://cloudnine.com/wp-content/uploads/2020/02/CrackPassword2.png) |
| :--: |
| _^ In this table you can see the approximate time it would take for a brute force hacker to crack your password. It obviously depends on the hardware and on how long it takes to crack one password, but this does show how the time it takes to crack a password grows exponentially as the requirements increase._ |

## At what point will the user not want to bother with the password requirements anymore?


# Conclusion

After applying all these measures, our passwords are now completely safe. Not even the developer that implemented this account system will be able to retrieve the passwords. The only option that's left to retrieve the passwords now is to brute force it.

